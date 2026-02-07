# PREMIERE — QA Plan

**Game:** PREMIERE (Management Sim / TV Network Tycoon)
**Platform:** PC (Steam), Steam Deck
**QA Lead:** CRASH
**Version:** 1.0 Pre-Production QA Strategy
**Last Updated:** 2026-02-07

---

## 0. CRASH's Note

I've read your pitch. I've read your GDD. I've read your narrative bible and your tech architecture. You want to ship a management sim where the player drags show cards around a scheduling grid and feels like a network executive. You want the ratings to feel meaningful, the cancellations to sting, and the whole thing to run on a potato.

Here's what I know: you're building a data-heavy simulation with 200+ entities, 12 seasons of compounding choices, procedurally generated content, and a drag-and-drop UI that needs to recalculate adjacency in real-time without dropping frames. You've got persistent AI relationships, a complex economy model, and save files that will bloat to 700KB of JSON. You're targeting 60 FPS on minimum spec hardware from 2016.

This is how things break. Every input permutation. Every edge case. Every frame drop during a drag. Every save file corruption when a showrunner's loyalty hits -101 and the serializer chokes. Every moment where the player stares at The Board and thinks "I have no idea why that show just tanked."

I'm not here to tell you what works. I'm here to tell you what breaks, where it breaks, and what happens when a player does the one thing you didn't think to test. Let me show you exactly how we're going to find every crack in this thing before a single player does.

What's the first rule? Test the worst case, not the best case.

What's the second rule? If it can be saved mid-action, it will corrupt.

What's the third rule? The player will cancel the Emmy-winning show by accident and blame us.

Let's find the breaks.

-- CRASH

---

## 1. Testing Strategy Overview

### 1.1 Testing Philosophy

PREMIERE is a **systems-driven strategy game** where success depends on:
1. **Clarity** — The player must understand why things happen
2. **Feedback** — Actions must have visible, immediate consequences
3. **Consistency** — Systems must behave predictably within their rules
4. **Stability** — Save files, simulations, and UI interactions must never corrupt or crash

**What this means for QA:**
- We test for **legibility** as much as correctness (can the player read The Board at a glance?)
- We test for **ripple effects** across interconnected systems (moving a show affects ratings, which affects talent loyalty, which affects pilot quality)
- We test for **data integrity** over 30+ hour campaigns (save files must survive 12 seasons x 35 weeks)
- We test **edge cases of player cruelty** (what if they cancel every show? What if they refuse every talent negotiation? What if they schedule reality TV exclusively?)

### 1.2 Quality Gates (Ship Criteria)

The game does NOT ship until these conditions are met:

| Gate | Criteria | Verification Method |
|---|---|---|
| **Core Loop Stable** | Player can drag a card, place it, and see adjacency updates without frame drops (60 FPS on rec spec, 30 FPS on min spec) | Performance profiling, 20 testers |
| **Save/Load Reliable** | 100 consecutive save/load cycles with no corruption | Automated stress test |
| **Simulation Deterministic** | Same input produces same ratings output (within noise tolerance) | Automated validation |
| **Balance Coherent** | No single strategy dominates >70% win rate across 50 test playthroughs | Data analysis of playtests |
| **UI Readable** | 80% of blind testers can identify their strongest/weakest night within 5 seconds | Usability testing |
| **No Critical Bugs** | Zero P0 (crash/corruption), Zero P1 (blocks progression) bugs in final RC | Bug tracker validation |

**We do not negotiate on these gates.** If any gate fails at RC stage, we delay.

---

## 2. Test Plan by Feature Area

### 2.1 THE BOARD (Scheduling System)

**What we're testing:** The 7x3 drag-and-drop scheduling grid — the game's core interaction.

#### Test Cases: Basic Functionality

| TC ID | Test Case | Steps | Expected Result | Priority |
|---|---|---|---|---|
| BRD-001 | Drag card from bench to empty slot | 1. Start new game<br>2. Click and hold show card in bench<br>3. Drag to Monday 8 PM slot<br>4. Release | Card snaps to slot, shows "placed" state, stats recalculate | P0 |
| BRD-002 | Drag card to occupied slot | 1. Place card in Monday 8 PM<br>2. Drag different card to same slot<br>3. Release | Original card returns to bench, new card takes slot | P0 |
| BRD-003 | Drag card from slot to slot | 1. Place card in Monday 8 PM<br>2. Drag to Tuesday 9 PM<br>3. Release | Card moves, Monday 8 PM now empty, adjacency recalcs both nights | P0 |
| BRD-004 | Swap two cards | 1. Place Card A in Monday 8 PM<br>2. Place Card B in Monday 9 PM<br>3. Drag Card A to Monday 9 PM | Card A and Card B swap positions | P1 |
| BRD-005 | Cancel drag mid-action | 1. Start dragging a card<br>2. Press ESC or drag outside valid zone<br>3. Release | Card returns to original position with elastic tween | P1 |
| BRD-006 | Place 21 cards (full grid) | 1. Fill all 21 slots with unique shows<br>2. Verify no empty slots<br>3. Try to place 22nd card | All slots filled, 22nd card stays in bench (or replaces a slotted card if dragged to one) | P1 |

#### Test Cases: Adjacency & Lead-In Calculations

| TC ID | Test Case | Steps | Expected Result | Priority |
|---|---|---|---|---|
| BRD-101 | Lead-in bonus visible | 1. Place broad comedy (12M viewers, 65% F18-49) at Monday 8 PM<br>2. Place legal drama (55% F18-49) at Monday 9 PM<br>3. Observe 9 PM slot stats | Legal drama shows lead-in bonus ~+7M viewers, green compatibility arrow | P0 |
| BRD-102 | Lead-in bonus recalculates on upstream change | 1. Set up lead-in chain (8 PM -> 9 PM -> 10 PM)<br>2. Remove 8 PM show<br>3. Observe 9 PM and 10 PM stats | Both slots' lead-in bonuses drop, expected viewership decreases | P0 |
| BRD-103 | Demographic mismatch reduces lead-in | 1. Place M18-49 action show at 8 PM<br>2. Place F18-49 drama at 9 PM<br>3. Observe compatibility | Yellow/red compatibility arrow, reduced lead-in bonus (<50% of 8 PM audience) | P1 |
| BRD-104 | Timeslot decay factor applied | 1. Place 12M viewer show at 8 PM<br>2. Place identical demo show at 9 PM<br>3. Place identical demo show at 10 PM<br>4. Compare lead-in values | 9 PM gets ~85% flow (10.2M), 10 PM gets ~75% flow (9M) | P1 |
| BRD-105 | Cascading recalculation performance | 1. Fill Monday 8 PM, 9 PM, 10 PM with strong lead-in chain<br>2. Remove 8 PM card while profiler running<br>3. Measure recalculation time | Recalc completes in <5ms, no frame drop | P0 |

#### Test Cases: Competitive Display

| TC ID | Test Case | Steps | Expected Result | Priority |
|---|---|---|---|---|
| BRD-201 | Rival schedules visible | 1. Place show in Thursday 9 PM<br>2. Check competitive display panel | Shows what AmeriNet, Crowne, Pacific are airing in Thursday 9 PM with threat level | P1 |
| BRD-202 | Threat indicator accuracy | 1. Schedule weak show (5M floor) vs. strong rival (15M ceiling)<br>2. Check threat indicator | Red threat indicator, high competitive drain estimate | P1 |
| BRD-203 | Counterprogramming opportunity visible | 1. All rivals schedule M18-49 shows at Thursday 9 PM<br>2. Place F18-49 show in same slot<br>3. Check display | Lower threat indicator, "counterprogramming opportunity" tooltip | P2 |

#### Edge Cases (The Evil Path)

| TC ID | Test Case | Steps | Expected Result | Priority |
|---|---|---|---|---|
| BRD-901 | Drag card during simulation | 1. Lock schedule, begin week simulation<br>2. Attempt to drag card during simulation<br>3. Observe | Cards are locked/non-interactive during simulation, or action queues for after sim | P0 |
| BRD-902 | Drag 50 cards rapidly | 1. Drag a card back and forth between two slots 50 times in 10 seconds<br>2. Monitor framerate | No frame drops, no UI corruption, no NaN values in stats | P1 |
| BRD-903 | Alt-tab during drag | 1. Begin dragging card<br>2. Alt-tab to another window<br>3. Return to game | Card returns to original position, no ghost cards, no hung state | P1 |
| BRD-904 | Save mid-drag | 1. Begin dragging card (hold mouse button)<br>2. Press save hotkey (S) while dragging<br>3. Release mouse<br>4. Load save | Card is in saved state (original position), drag state not persisted | P0 |
| BRD-905 | Multi-monitor edge case | 1. Drag card to edge of screen on multi-monitor setup<br>2. Cursor leaves window bounds<br>3. Release outside game window | Card returns to original position, no crash | P2 |
| BRD-906 | Spam click cards | 1. Click 20 different cards rapidly in 2 seconds<br>2. Observe | No double-selection, no UI hang, last clicked card is selected | P1 |
| BRD-907 | Empty grid simulation | 1. Remove all shows from grid<br>2. Lock schedule, simulate week<br>3. Observe | Week simulates (zero revenue, network president warning), no crash | P2 |
| BRD-908 | 21 identical shows | 1. Clone one show 21 times (via save file edit or debug command)<br>2. Place all in grid<br>3. Simulate week | Each slot calculates independently, no ID collision bugs | P2 |

---

### 2.2 THE PILOT PIPELINE (Development System)

**What we're testing:** Procedural show generation, greenlight decisions, pilot development tracking.

#### Test Cases: Show Generation

| TC ID | Test Case | Steps | Expected Result | Priority |
|---|---|---|---|---|
| PP-001 | Pilot pool generates correctly | 1. Start Season 1<br>2. Open pilot pool<br>3. Count pilots | 25-40 pilots, all have unique IDs, titles, premises, stats | P0 |
| PP-002 | Stat ranges within bounds | 1. Generate 100 pilots (via debug command or 4 seasons)<br>2. Export stats to CSV<br>3. Validate ranges | QC: 40-95, QF: 15-60, AF: 2-18M, AC: 4-20M, CPE: 300K-4M | P1 |
| PP-003 | No duplicate titles in pool | 1. Generate pilot pool<br>2. Check for exact duplicate titles | All titles unique (premise can be similar, title must differ) | P1 |
| PP-004 | Genre distribution matches config | 1. Generate 10 pilot pools (10 seasons)<br>2. Count genre occurrences<br>3. Compare to GenreTemplate weights | Distribution within 15% of configured weights | P2 |
| PP-005 | Showrunner attachment affects QC | 1. Generate pilot with high TL showrunner (85+)<br>2. Generate pilot with low TL showrunner (40-)<br>3. Compare QC values | High TL pilot has +15 to +30 QC bonus on average | P1 |

#### Test Cases: Greenlight & Development

| TC ID | Test Case | Steps | Expected Result | Priority |
|---|---|---|---|---|
| PP-101 | Greenlight within budget | 1. Start season with $35M dev budget<br>2. Greenlight 8 pilots averaging $4M each<br>3. Check budget | Budget deducted correctly, shows enter development track | P0 |
| PP-102 | Greenlight over budget blocked | 1. Greenlight pilots totaling $34M<br>2. Attempt to greenlight $5M pilot<br>3. Observe | "Insufficient budget" warning, greenlight blocked | P1 |
| PP-103 | Development stages progress | 1. Greenlight pilot<br>2. Simulate 4 weeks<br>3. Check pilot status | Pilot progresses: "In Production" -> "Rough Cut" -> "Test Screening" -> "Ready for Schedule" | P1 |
| PP-104 | Pilot fails in development | 1. Greenlight high-risk (Risk 4-5) pilot<br>2. Simulate development (4 weeks)<br>3. Check for failure event | 10-20% chance pilot fails ("showrunner creative differences", pilot never airs), budget spent | P2 |
| PP-105 | Test audience score appears | 1. Complete pilot development<br>2. Check pilot card for test score<br>3. Compare to actual QR | Test score visible (1-100), may diverge from actual QR by +/- 15 points | P2 |

#### Edge Cases

| TC ID | Test Case | Steps | Expected Result | Priority |
|---|---|---|---|---|
| PP-901 | Greenlight zero pilots | 1. Start season<br>2. Skip greenlighting any pilots<br>3. Progress to midseason | Network president warning, "no new shows in pipeline" event, able to continue | P2 |
| PP-902 | Greenlight all 40 pilots | 1. Modify budget to $500M via debug<br>2. Greenlight all pilots in pool<br>3. Simulate | All enter development, some fail, player has 30+ shows to schedule (chaos, but functional) | P2 |
| PP-903 | Premise generation repetition test | 1. Generate 500 pilots (via debug fast-forward)<br>2. Check for exact duplicate premises<br>3. Count unique vs. similar | No exact duplicates, at least 70% feel distinct (subjective but log similar premises) | P1 |
| PP-904 | Showrunner loyalty affects pilot quality | 1. Burn loyalty with showrunner (cancel their show)<br>2. Check if they bring pilots to player next season<br>3. If yes, compare QC to baseline | Low-loyalty showrunners bring lower-QC pilots or refuse to pitch to player | P2 |
| PP-905 | Genre freshness degrades over time | 1. Greenlight 10 procedural crime shows over 3 seasons<br>2. Check genre freshness score<br>3. Generate new procedural pilots | QC ceiling drops due to saturation (Genre Freshness modifier applies) | P2 |

---

### 2.3 THE RATINGS ENGINE (Simulation & Competition)

**What we're testing:** Weekly viewership simulation, rival network AI, audience behavior modeling.

#### Test Cases: Viewership Calculation

| TC ID | Test Case | Steps | Expected Result | Priority |
|---|---|---|---|---|
| RE-001 | Organic audience calculated correctly | 1. Place show (QR 80, AF 5M, AC 12M, SP 5) in Monday 8 PM<br>2. Simulate week 1 (no lead-in)<br>3. Check viewership | Viewership between AF and AC, skewed toward AC due to high QR, star bonus ~+2.5M | P0 |
| RE-002 | Loyalty curve applies | 1. Place new show (week 1)<br>2. Simulate 15 weeks with consistent QR 75<br>3. Track viewership week-over-week | Viewership rises over weeks 1-12, plateaus around week 12-15 (loyalty curve) | P1 |
| RE-003 | Quality drop causes loyalty decay | 1. Show at loyalty 0.8 after 15 weeks<br>2. Drop QR by 15 points (simulate showrunner departure)<br>3. Simulate 5 more weeks | Loyalty decays ~0.03/week, viewership drops gradually | P2 |
| RE-004 | Marketing boost applies | 1. Place show with Heavy Marketing ($4M)<br>2. Simulate premiere week<br>3. Compare to same show with no marketing | +25% premiere viewers, +8% ongoing for 4 weeks | P1 |
| RE-005 | Competitive drain calculated | 1. Schedule 5M expected show vs. rival's 15M flagship<br>2. Simulate week<br>3. Check actual vs. expected viewership | Actual viewership below expected due to competitive drain | P1 |

#### Test Cases: Seasonal Modifiers

| TC ID | Test Case | Steps | Expected Result | Priority |
|---|---|---|---|---|
| RE-101 | September premiere boost | 1. Schedule new show in Week 1 (Sept)<br>2. Simulate week<br>3. Compare to baseline | +15% viewership from seasonal modifier | P2 |
| RE-102 | November sweeps boost | 1. Simulate to Week 10 (November sweeps)<br>2. Check viewership for all shows<br>3. Compare to Week 9 | +20% viewership across the board | P1 |
| RE-103 | Holiday lull penalty | 1. Simulate to Week 14 (December)<br>2. Check viewership<br>3. Compare to November | -30% viewership (holiday drop) | P2 |
| RE-104 | May sweeps + finale spike | 1. Simulate to Week 35 (May sweeps)<br>2. Schedule season finale<br>3. Check viewership | +25% sweeps + +30% finale = ~+55% combined (multiplicative, not additive) | P2 |

#### Test Cases: Rival Network AI

| TC ID | Test Case | Steps | Expected Result | Priority |
|---|---|---|---|---|
| RE-201 | AmeriNet clones player hits | 1. Launch high-rated procedural (12M+ viewers)<br>2. Sustain for 2 seasons<br>3. Check AmeriNet's pilots Season 3 | 50% chance AmeriNet greenlights similar genre/subgenre show | P2 |
| RE-202 | Crowne Broadcasting poaches talent | 1. Build high-loyalty (60+) showrunner with high TL (80+)<br>2. Simulate 5 seasons<br>3. Check for poaching event | Crowne attempts poaching offer at least once | P2 |
| RE-203 | Pacific Television counterprograms sweeps | 1. Identify player's strongest timeslot<br>2. Enter November sweeps (Week 10)<br>3. Check Pacific's schedule | Pacific schedules event programming or stunt show against player's flagship | P2 |
| RE-204 | AI difficulty scales over time | 1. Play Seasons 1-2, note rival schedules<br>2. Play Seasons 6-8, compare<br>3. Analyze rival decision quality | Early seasons: suboptimal scheduling. Late seasons: optimal lead-in chains, counterprogramming | P2 |

#### Test Cases: DVR Mechanics (Late-Game)

| TC ID | Test Case | Steps | Expected Result | Priority |
|---|---|---|---|---|
| RE-301 | DVR adoption reduces live ratings | 1. Fast-forward to Season 6 (2005, 15% DVR adoption)<br>2. Compare live vs. total viewership<br>3. Check serialized drama (high DVR propensity) | Live viewership ~85% of total, DVR adds +15% in Live+3 metric | P1 |
| RE-302 | Live+7 metric unlocks Season 9 | 1. Fast-forward to Season 9 (2008, 40% DVR adoption)<br>2. Check if Live+7 appears in ratings report<br>3. Compare CPM for live vs. Live+7 | Live+7 visible, CPM ~80% of live CPM but higher total revenue for high-DVR shows | P1 |
| RE-303 | Reality shows resist DVR time-shift | 1. Schedule reality show (DVR propensity 0.1)<br>2. Compare live vs. total in high-DVR era (Season 10)<br>3. Check delta | Reality show: 95% live viewership, minimal DVR boost | P2 |

#### Edge Cases

| TC ID | Test Case | Steps | Expected Result | Priority |
|---|---|---|---|---|
| RE-901 | All networks schedule same timeslot empty | 1. Clear Thursday 9 PM on all 4 networks<br>2. Simulate week<br>3. Observe | No crash, zero viewership for that slot, audience redistributes to other slots or doesn't watch TV | P2 |
| RE-902 | Simulation determinism test | 1. Save game before week simulation<br>2. Simulate week, note results<br>3. Load save, simulate again<br>4. Compare | Identical results (within RNG noise tolerance <1%) | P0 |
| RE-903 | Extreme stat edge case (QR 100, AF 0) | 1. Via debug, create show with QR 100, AF 0M, AC 20M<br>2. Simulate week<br>3. Check for NaN or crash | Viewership calculates correctly (~19-20M), no crash | P1 |
| RE-904 | 100-week simulation stress test | 1. Set up typical schedule<br>2. Run 100-week simulation via debug fast-forward<br>3. Monitor performance and stability | Simulation completes, no memory leaks, no performance degradation | P1 |
| RE-905 | Rival network bankruptcy | 1. Via debug, set rival network budget to -$50M<br>2. Simulate season<br>3. Observe rival behavior | Rival either goes bankrupt (ceases operations) or system prevents negative budget | P2 |

---

### 2.4 THE TALENT WEB (Relationship System)

**What we're testing:** Showrunner/actor AI, loyalty tracking, contract negotiations, talent events.

#### Test Cases: Loyalty Mechanics

| TC ID | Test Case | Steps | Expected Result | Priority |
|---|---|---|---|---|
| TW-001 | Greenlight increases loyalty | 1. Showrunner starts at loyalty 0<br>2. Greenlight their pilot<br>3. Check loyalty | Loyalty +10 to +15 | P1 |
| TW-002 | Cancellation damages loyalty | 1. Cancel show with 8M viewers (high-rated)<br>2. Check showrunner loyalty<br>3. Observe | Loyalty -20 to -30 (betrayal) | P1 |
| TW-003 | Justified cancellation less damaging | 1. Cancel show with 2M viewers (well below slot average)<br>2. Check showrunner loyalty<br>3. Compare to high-rated cancellation | Loyalty -5 (justified), less damage than betrayal cancel | P2 |
| TW-004 | Timeslot move affects loyalty | 1. Move show from Thursday 9 PM to Friday 9 PM<br>2. Check showrunner loyalty and ego<br>3. Observe | High ego (70+): loyalty -15 to -25. Low ego: loyalty -5 | P1 |
| TW-005 | Emmy win boosts loyalty | 1. Win Emmy for showrunner's show<br>2. Check loyalty<br>3. Observe | Loyalty +20 | P2 |

#### Test Cases: Talent Events

| TC ID | Test Case | Steps | Expected Result | Priority |
|---|---|---|---|---|
| TW-101 | Creative revolt triggers on timeslot move | 1. Move high-ego (75+) showrunner's show to worse slot<br>2. Simulate 1-2 weeks<br>3. Check inbox | 25% chance "Creative Revolt" event fires within 2 weeks | P1 |
| TW-102 | Poaching event at low loyalty | 1. Burn showrunner loyalty to -40<br>2. Simulate 5 weeks<br>3. Check for poaching offer | Rival network offers deal, player can counter or lose showrunner | P1 |
| TW-103 | Passion project pitch at high loyalty | 1. Build showrunner loyalty to 65+<br>2. Maintain for 3 seasons<br>3. Check for pitch event | Showrunner offers high-QC pilot at discount, 10% chance per season | P2 |
| TW-104 | Actor scandal (high volatility) | 1. Cast actor with volatility 9<br>2. Simulate 10 weeks<br>3. Check for scandal event | ~30% chance scandal fires (DUI, tabloid incident) | P2 |
| TW-105 | Contract expiration negotiation | 1. Actor contract expires (4 weeks warning)<br>2. Receive negotiation event<br>3. Choose response (pay, recast, write off) | Each choice has expected consequence (budget cost, QR drop, cast change) | P1 |

#### Test Cases: Event Choices & Consequences

| TC ID | Test Case | Steps | Expected Result | Priority |
|---|---|---|---|---|
| TW-201 | Creative revolt: restore timeslot | 1. Trigger creative revolt<br>2. Choose "restore timeslot"<br>3. Observe | Show moved back, loyalty +10, strategic position lost | P2 |
| TW-202 | Creative revolt: call bluff | 1. Trigger creative revolt<br>2. Choose "call bluff"<br>3. Observe | 40% chance they quit (QR -12 to -20), 60% they stay (loyalty -15) | P2 |
| TW-203 | Actor scandal: fire immediately | 1. Trigger scandal<br>2. Choose "fire actor"<br>3. Observe | Show QR -10, recasting takes 4 weeks, viewership dip | P2 |
| TW-204 | Contract holdout: recast | 1. Actor demands 3x salary<br>2. Choose "recast"<br>3. Observe consequences | QR -10, viewership -15% for 6 weeks, new actor hired | P2 |

#### Edge Cases

| TC ID | Test Case | Steps | Expected Result | Priority |
|---|---|---|---|---|
| TW-901 | Showrunner at loyalty -100 | 1. Cancel 3 shows from same showrunner<br>2. Drive loyalty to -100<br>3. Attempt to greenlight their pilot next season | Showrunner refuses to work with player, pilots go to rivals | P2 |
| TW-902 | Showrunner at loyalty +100 | 1. Build loyalty to +100 via Emmy wins, greenlights, support<br>2. Offer low-ball contract<br>3. Observe | Showrunner accepts out of loyalty (override normal refusal logic) | P2 |
| TW-903 | Multiple events fire same week | 1. Trigger conditions for 5+ events simultaneously<br>2. Simulate week<br>3. Check inbox | Events prioritized (urgent first), player not overwhelmed (cap at 5 per week) | P1 |
| TW-904 | All actors on one show have expired contracts | 1. Set up show where all 3 cast contracts expire same week<br>2. Simulate<br>3. Handle negotiations | Each actor negotiates independently, player can lose entire cast (show collapses) | P2 |
| TW-905 | Showrunner poached mid-development | 1. Greenlight pilot<br>2. During 4-week development, trigger poaching<br>3. Lose showrunner | Pilot development fails or gets reassigned to backup showrunner (QR penalty) | P2 |
| TW-906 | Recursive event triggers | 1. Fire actor (event A)<br>2. Actor firing causes showrunner revolt (event B)<br>3. Showrunner revolt causes network president warning (event C)<br>4. Observe | Events chain correctly without stack overflow or infinite loop | P1 |

---

### 2.5 THE LEDGER (Economy System)

**What we're testing:** Budget allocation, revenue calculation, profit/loss tracking, financial warnings.

#### Test Cases: Revenue Calculation

| TC ID | Test Case | Steps | Expected Result | Priority |
|---|---|---|---|---|
| LED-001 | Ad revenue for 18-49 demo | 1. Show pulls 5M viewers, 70% in 18-49 demo<br>2. Simulate week<br>3. Check revenue | ~3.5M weighted viewers x $25 CPM x 32 ad slots = ~$2.8M revenue | P1 |
| LED-002 | CPM modifier for brand safety | 1. Show marked "Controversial" pulls 5M viewers<br>2. Check revenue vs. "Mainstream" show with same viewership<br>3. Compare | Controversial: -30% CPM, ~$1.96M revenue (vs. $2.8M baseline) | P2 |
| LED-003 | Prestige CPM boost from Emmys | 1. Win 3 Emmys<br>2. Check network prestige rating<br>3. Calculate CPM boost | Prestige rating increases, CPM +15% (3 Emmys x 5% each) | P2 |
| LED-004 | Sweeps CPM boost | 1. Simulate to November sweeps (Week 10)<br>2. Check ad revenue for same show vs. October<br>3. Compare | CPM +20% during sweeps, revenue boost | P2 |

#### Test Cases: Budget Management

| TC ID | Test Case | Steps | Expected Result | Priority |
|---|---|---|---|---|
| LED-101 | Budget allocation at season start | 1. Start Season 2 with $180M total budget<br>2. Allocate: $35M dev, $30M marketing, $95M talent, $20M ops<br>3. Validate | Total = $180M, allocations lock for season | P1 |
| LED-102 | Over-allocation blocked | 1. Attempt to allocate $200M across categories<br>2. Observe | Warning: "Budget exceeds available funds", allocation blocked | P1 |
| LED-103 | Profit/loss tracked correctly | 1. Simulate full season<br>2. Check end-of-season financial report<br>3. Validate math | Revenue (ad + syndication) - Costs (dev + marketing + talent + production + ops) = Net Profit | P1 |
| LED-104 | Next season budget scales with performance | 1. Season 1 net profit: +$30M<br>2. Check Season 2 starting budget<br>3. Validate formula | Season 2 budget = (Season 1 revenue x 0.85) + $60M baseline | P2 |

#### Test Cases: Financial Warnings

| TC ID | Test Case | Steps | Expected Result | Priority |
|---|---|---|---|---|
| LED-201 | Development budget depleted | 1. Greenlight pilots until dev budget <20%<br>2. Observe | Warning: "Low development budget — cannot greenlight more pilots" | P2 |
| LED-202 | Season ends in loss | 1. Run high-cost, low-revenue season (prestige shows, low ratings)<br>2. Check annual review<br>3. Observe | Net loss reported, network president warning, budget cut for next season | P2 |
| LED-203 | Three consecutive declining seasons | 1. Via debug, force 3 seasons of declining revenue<br>2. Check Season 4 start<br>3. Observe | Firing warning: "Board expects improvement or leadership change" | P2 |
| LED-204 | Bankruptcy threshold (-$20M) | 1. Via debug, run season to -$25M net loss<br>2. Observe | Game over: "Network bankruptcy — you have been removed from your position" | P2 |

#### Edge Cases

| TC ID | Test Case | Steps | Expected Result | Priority |
|---|---|---|---|---|
| LED-901 | Zero revenue season | 1. Remove all shows from grid<br>2. Simulate full season with empty schedule<br>3. Check financials | Zero ad revenue, fixed costs still apply, massive net loss, firing warning | P2 |
| LED-902 | Maximum revenue optimization | 1. Fill grid with optimal shows (high 18-49 demo, low cost)<br>2. Win sweeps every month<br>3. Check profit margin | System supports 60-80% profit margin without overflow errors | P1 |
| LED-903 | Marketing spend carries over mid-season | 1. Apply Event Launch marketing ($8M) to show<br>2. Show gets cancelled Week 8<br>3. Check if marketing refunded | Marketing cost sunk (not refunded), player loses $8M on cancelled show | P2 |
| LED-904 | Syndication revenue calculation | 1. Complete show after 7 seasons (150+ episodes)<br>2. Check syndication revenue in Season 8<br>3. Validate | Show generates passive revenue based on episode count x cultural footprint score | P2 |
| LED-905 | CPM overflow with 10 Emmys | 1. Win 10 Emmys (via debug)<br>2. Check prestige CPM boost<br>3. Validate | CPM boost caps at +25% (not +50%), prevents balance break | P2 |

---

### 2.6 SAVE SYSTEM

**What we're testing:** Save/load reliability, data integrity, corruption resistance, migration.

#### Test Cases: Basic Save/Load

| TC ID | Test Case | Steps | Expected Result | Priority |
|---|---|---|---|---|
| SAV-001 | Save game mid-season | 1. Play to Season 3, Week 12<br>2. Press Save (hotkey S)<br>3. Check save file exists | Save file created in persistentDataPath, ~500-700KB JSON | P0 |
| SAV-002 | Load saved game | 1. Load save from SAV-001<br>2. Verify game state<br>3. Continue playing | Season, week, budget, shows, talent, schedules all restored correctly | P0 |
| SAV-003 | Autosave at end of week | 1. Simulate week<br>2. Check for autosave file<br>3. Observe | Autosave created, 3 rotating slots (autosave_1, autosave_2, autosave_3) | P1 |
| SAV-004 | Autosave before major decision | 1. Open talent negotiation event<br>2. Check for autosave trigger<br>3. Observe | Autosave created before player makes choice | P1 |
| SAV-005 | Manual save slots (3 slots) | 1. Create Save 1, Save 2, Save 3<br>2. Load each<br>3. Overwrite Save 2 | All 3 slots work independently, no cross-contamination | P1 |

#### Test Cases: Data Integrity

| TC ID | Test Case | Steps | Expected Result | Priority |
|---|---|---|---|---|
| SAV-101 | 100 consecutive save/load cycles | 1. Automate save/load loop 100 times<br>2. Validate game state after each load<br>3. Check for corruption | Zero corruption, zero data loss | P0 |
| SAV-102 | Save with 200 shows in history | 1. Play to Season 10 (200+ shows across active/cancelled/completed)<br>2. Save game<br>3. Load and verify | All 200 shows restore with correct stats, history, relationships | P1 |
| SAV-103 | Save/load talent loyalty states | 1. Build loyalty to +75 with Showrunner A, -50 with Showrunner B<br>2. Save, load<br>3. Verify | Loyalty values restore exactly | P1 |
| SAV-104 | Save/load rival network schedules | 1. Mid-season, note all 3 rival schedules<br>2. Save, load<br>3. Compare | Rival schedules identical post-load | P1 |
| SAV-105 | Save/load event history | 1. Make 20 event choices (track decisions)<br>2. Save, load<br>3. Check legacy score calculation | Event history preserved, legacy score correct | P2 |

#### Test Cases: Save File Corruption Resistance

| TC ID | Test Case | Steps | Expected Result | Priority |
|---|---|---|---|---|
| SAV-201 | Load corrupted JSON (missing bracket) | 1. Manually remove closing `}` from save file<br>2. Attempt to load<br>3. Observe | Error message: "Save file corrupted", fallback to backup autosave | P1 |
| SAV-202 | Load save with missing field | 1. Delete `networkState.budget` field from JSON<br>2. Load save<br>3. Observe | Deserialization fills missing field with default value, warning logged | P2 |
| SAV-203 | Load save from future version | 1. Edit save file version to "2.0.0"<br>2. Load in v1.0 build<br>3. Observe | Warning: "Save from newer version, may not load correctly", attempt load or reject | P2 |
| SAV-204 | Load save from older version | 1. Simulate v0.9 save file format<br>2. Load in v1.0 build<br>3. Observe | Migration system runs, save converted to v1.0 format, data preserved | P1 |

#### Edge Cases

| TC ID | Test Case | Steps | Expected Result | Priority |
|---|---|---|---|---|
| SAV-901 | Save during week simulation | 1. Lock schedule, begin simulation<br>2. Press save during simulation<br>3. Observe | Save queued until simulation completes, or blocked with message "Cannot save during simulation" | P1 |
| SAV-902 | Save with NaN values in stats | 1. Via debug, inject NaN into show's viewership stat<br>2. Attempt save<br>3. Observe | Validation catches NaN, replaces with 0 or last valid value, logs error | P1 |
| SAV-903 | Load save, modify, save again | 1. Load save<br>2. Make changes (move 3 shows, cancel 1 show)<br>3. Save over original file<br>4. Load again | Changes persist, no data corruption | P1 |
| SAV-904 | Disk full during save | 1. Simulate low disk space (via test environment)<br>2. Attempt save<br>3. Observe | Error: "Insufficient disk space", save aborts, previous save intact | P2 |
| SAV-905 | Save file size stress test | 1. Play to Season 12 (400+ shows, 420 weeks of data)<br>2. Save<br>3. Check file size | Save file <2MB, loads in <3 seconds | P1 |
| SAV-906 | Cloud save sync (Steam) | 1. Save on PC A<br>2. Load on PC B via Steam Cloud<br>3. Verify | Save syncs correctly, playable on both machines | P2 |

---

### 2.7 UI / UX TESTING

**What we're testing:** Readability, usability, accessibility, performance, layout at various resolutions.

#### Test Cases: Readability (The 5-Second Test)

| TC ID | Test Case | Steps | Expected Result | Priority |
|---|---|---|---|---|
| UI-001 | Identify strongest night in 5 seconds | 1. Show tester a mid-season schedule screenshot<br>2. Ask: "Which night is performing best?"<br>3. Time response | 80% of testers answer correctly in <5 seconds | P0 |
| UI-002 | Identify weakest show in 5 seconds | 1. Show tester The Board with ratings overlays<br>2. Ask: "Which show is underperforming?"<br>3. Time response | 75% of testers answer correctly in <5 seconds | P0 |
| UI-003 | Identify lead-in relationship | 1. Show tester Monday schedule with compatibility arrows<br>2. Ask: "Which shows have strong lead-in flow?"<br>3. Observe | 70% of testers identify green arrows = strong lead-in | P1 |
| UI-004 | Read card stats at a glance | 1. Place show card in slot<br>2. Ask tester: "What's the quality rating and cost?"<br>3. Time response | Tester reads QR and CPE in <2 seconds without hover | P1 |

#### Test Cases: Usability

| TC ID | Test Case | Steps | Expected Result | Priority |
|---|---|---|---|---|
| UI-101 | First-time player completes tutorial | 1. Give new player tutorial prompt<br>2. Observe without assistance<br>3. Time to completion | Player places first 5 shows correctly within 5 minutes | P1 |
| UI-102 | Ratings reveal is not tedious | 1. Simulate week<br>2. Present ratings<br>3. Survey player | Player rates reveal as "interesting" or "informative", not "tedious" or "too long" | P1 |
| UI-103 | Event inbox is manageable | 1. Fire 5 events in one week<br>2. Player triages inbox<br>3. Observe | Player resolves all 5 events in <3 minutes, doesn't feel overwhelmed | P1 |
| UI-104 | Tooltip clarity | 1. Hover over adjacency stat<br>2. Read tooltip<br>3. Ask player to explain | Player accurately explains lead-in bonus concept | P2 |

#### Test Cases: Resolution & Layout

| TC ID | Test Case | Steps | Expected Result | Priority |
|---|---|---|---|---|
| UI-201 | 1280x720 minimum resolution | 1. Set resolution to 1280x720<br>2. Check UI layout<br>3. Verify readability | All text readable, no UI clipping, cards fit grid | P1 |
| UI-202 | 1920x1080 recommended resolution | 1. Set resolution to 1920x1080<br>2. Check UI layout<br>3. Verify | Optimal layout, card text crisp, comfortable spacing | P0 |
| UI-203 | 4K resolution (3840x2160) | 1. Set resolution to 4K<br>2. Check scaling<br>3. Verify | UI scales correctly, no blurry text, cards proportional | P2 |
| UI-204 | Ultrawide (21:9) support | 1. Set resolution to 2560x1080<br>2. Check layout<br>3. Verify | UI adapts to ultrawide, no stretching, board centered | P2 |
| UI-205 | Steam Deck (1280x800) | 1. Launch on Deck<br>2. Check layout<br>3. Verify readability at 7 inches | Text readable (min 14pt), buttons thumb-friendly (48x48px), layout fits | P1 |

#### Test Cases: Performance (UI Rendering)

| TC ID | Test Case | Steps | Expected Result | Priority |
|---|---|---|---|---|
| UI-301 | 60 FPS on recommended spec | 1. Run game on rec spec (i5-9400, 8GB RAM)<br>2. Profile during card drag<br>3. Check framerate | Solid 60 FPS, no drops below 58 FPS | P0 |
| UI-302 | 30 FPS on minimum spec | 1. Run game on min spec (i5-6500, 4GB RAM, integrated GPU)<br>2. Profile during week simulation<br>3. Check framerate | Stable 30 FPS, no drops below 28 FPS | P0 |
| UI-303 | No frame drops during stat update | 1. Drag card, trigger full grid recalc<br>2. Profile with Unity Profiler<br>3. Check frame time | Recalc completes in <5ms, no visible stutter | P0 |
| UI-304 | Smooth animations (card placement) | 1. Place card in slot<br>2. Observe snap animation<br>3. Check smoothness | Elastic ease animation (0.2s), 60 FPS throughout | P1 |

#### Edge Cases

| TC ID | Test Case | Steps | Expected Result | Priority |
|---|---|---|---|---|
| UI-901 | Text scaling for accessibility | 1. Enable large text mode (if supported)<br>2. Check layout<br>3. Verify | Text scales to 125%, layout adjusts, no clipping | P2 |
| UI-902 | Colorblind mode | 1. Enable colorblind filter (if supported)<br>2. Check lead-in arrows and threat indicators<br>3. Verify | Green/red replaced with symbols or alternative colors | P2 |
| UI-903 | UI at 200% OS scaling (Windows) | 1. Set Windows display scaling to 200%<br>2. Launch game<br>3. Check UI | Game respects OS scaling, UI renders correctly | P2 |
| UI-904 | Card spam (50 cards in bench) | 1. Via debug, add 50 show cards to bench<br>2. Check layout<br>3. Scroll bench | Bench scrolls correctly, no overlap, performance stable | P2 |
| UI-905 | Long show title overflow | 1. Create show with 60-character title<br>2. Place in slot<br>3. Observe | Title truncates with "..." or wraps to two lines, no overflow | P2 |

---

### 2.8 CROSS-SYSTEM INTEGRATION

**What we're testing:** Ripple effects, feedback loops, emergent interactions between systems.

#### Test Cases: System Interactions

| TC ID | Test Case | Steps | Expected Result | Priority |
|---|---|---|---|---|
| INT-001 | Board -> Ratings -> Talent pipeline | 1. Move show to worse slot (Board)<br>2. Simulate week, show tanks (Ratings)<br>3. Check showrunner reaction (Talent)<br>4. Observe | Showrunner loyalty drops, may trigger creative revolt event | P1 |
| INT-002 | Ratings -> Ledger -> Pipeline | 1. Run high-rated season (Ratings)<br>2. Check budget increase (Ledger)<br>3. Greenlight more pilots next season (Pipeline)<br>4. Observe | Profit increases budget, enabling more development spend | P1 |
| INT-003 | Talent -> Pipeline -> Board | 1. Burn showrunner loyalty to -50 (Talent)<br>2. Check next season's pilot pool (Pipeline)<br>3. Observe | Hostile showrunner brings lower-QC pilots or refuses to pitch | P2 |
| INT-004 | Prestige flywheel (Emmy -> Talent -> Pipeline) | 1. Win Emmy (Ratings)<br>2. Check showrunner pool next season (Talent)<br>3. Check pilot QC distribution (Pipeline)<br>4. Observe | Better showrunners attracted, higher average QC in pool | P2 |
| INT-005 | Cost spiral (Hit -> Talent -> Ledger) | 1. Run hit show 3 seasons (Ratings)<br>2. Actors demand raises (Talent)<br>3. CPE increases (Ledger)<br>4. Check margins | Show profitability declines as talent costs rise | P2 |

#### Test Cases: Feedback Loops

| TC ID | Test Case | Steps | Expected Result | Priority |
|---|---|---|---|---|
| INT-101 | Negative feedback: genre saturation | 1. Greenlight 8 procedurals Season 1<br>2. Continue for 3 seasons<br>3. Check new procedural QC ceilings<br>4. Observe | Genre freshness drops, new procedurals have -10 to -20 QC penalty | P2 |
| INT-102 | Positive feedback: ratings snowball | 1. Build strong Thursday night lead-in chain<br>2. Maintain for 2 seasons<br>3. Check advertiser confidence and budget<br>4. Observe | Dominant night -> higher revenue -> bigger marketing budget -> stronger dominance | P2 |
| INT-103 | Negative feedback: talent cost spiral | 1. Run 5 hit shows simultaneously<br>2. All stars demand raises<br>3. Check budget strain<br>4. Observe | Hit shows become expensive, force budget trade-offs, prevent runaway dominance | P2 |

#### Edge Cases (Emergent Behavior)

| TC ID | Test Case | Steps | Expected Result | Priority |
|---|---|---|---|---|
| INT-901 | The Shield Maneuver | 1. Schedule cheap reality show vs. rival's flagship<br>2. Schedule prestige drama in protected slot<br>3. Simulate season<br>4. Analyze | Reality show absorbs competitive fire, prestige drama performs well, strategy viable | P2 |
| INT-902 | The Kingmaker Play | 1. Greenlight rookie showrunner (TL 50)<br>2. Support over 3 seasons (loyalty +80)<br>3. Check TL growth and pilot QC<br>4. Observe | Showrunner TL grows to 85+, brings passion project with QC 90+ | P2 |
| INT-903 | The Poison Pill | 1. Let rival poach high-volatility (9) actor<br>2. Track rival's show with that actor<br>3. Wait for scandal<br>4. Observe | Actor scandal damages rival's show, strategic sabotage viable | P2 |
| INT-904 | The DVR Gambit | 1. In Season 9, schedule serialized drama in death slot<br>2. Accept low live ratings<br>3. Check Live+7 metrics<br>4. Observe | DVR audience reveals true popularity, advertiser CPM adjusts, strategy viable | P2 |
| INT-905 | The Prestige Trap | 1. Chase Emmy wins for 5 seasons (all prestige dramas)<br>2. Check budget and ratings vs. populist rival<br>3. Analyze | Player wins Emmys but loses ratings war, budget shrinks, trap sprung | P2 |

---

## 3. Platform-Specific Testing

### 3.1 PC (Steam) Testing

| TC ID | Test Case | Steps | Expected Result | Priority |
|---|---|---|---|---|
| PC-001 | Steam Cloud save sync | 1. Save on PC A, upload to Steam Cloud<br>2. Load on PC B<br>3. Verify sync | Save transfers correctly, playable on both | P1 |
| PC-002 | Steam achievements unlock | 1. Meet achievement criteria (e.g., "Win 10 Emmys")<br>2. Check Steam overlay<br>3. Verify | Achievement unlocks, visible in Steam profile | P2 |
| PC-003 | Steam overlay compatibility | 1. Open Steam overlay (Shift+Tab) during gameplay<br>2. Check for crashes or hangs<br>3. Observe | Overlay opens/closes smoothly, game pauses, no crash | P1 |
| PC-004 | Hotkey conflicts | 1. Set custom Steam hotkeys<br>2. Play game, use in-game hotkeys<br>3. Check for conflicts | Game hotkeys don't conflict with Steam hotkeys | P2 |
| PC-005 | Windows/macOS/Linux parity | 1. Test same save file on all 3 OS<br>2. Compare behavior<br>3. Verify | Identical behavior across platforms, save file portable | P1 |

### 3.2 Steam Deck Testing

| TC ID | Test Case | Steps | Expected Result | Priority |
|---|---|---|---|---|
| DECK-001 | Controller input mapping | 1. Launch on Deck in gaming mode<br>2. Test all controller inputs<br>3. Verify | A/B/X/Y, sticks, triggers all mapped correctly | P1 |
| DECK-002 | Touchscreen drag-and-drop | 1. Use touchscreen to drag cards<br>2. Place in slots<br>3. Observe | Native touch input works, feels responsive | P0 |
| DECK-003 | Text readability at 7 inches | 1. Check card text, tooltips, UI labels<br>2. Verify min font size 14pt<br>3. Read from 18 inches away | All text readable without squinting | P1 |
| DECK-004 | 60 FPS at 800p | 1. Run performance test on Deck<br>2. Profile during gameplay<br>3. Check framerate | Stable 60 FPS at 1280x800 | P1 |
| DECK-005 | Battery life test | 1. Play on Deck (full charge)<br>2. Track battery drain over 1 hour<br>3. Estimate total | 4+ hours battery life (low-demand 2D game) | P2 |
| DECK-006 | Suspend/resume | 1. Play game on Deck<br>2. Press power (suspend)<br>3. Resume after 10 minutes<br>4. Verify | Game resumes correctly, no state loss | P1 |

---

## 4. Progression & Balance Testing

### 4.1 Full Career Playthrough

| TC ID | Test Case | Steps | Expected Result | Priority |
|---|---|---|---|---|
| BAL-001 | Complete 12-season career | 1. Play from 2000 to 2012<br>2. Track time, decisions, outcomes<br>3. Reach endgame | Campaign completable in 25-40 hours, feels coherent start to finish | P0 |
| BAL-002 | Prestige strategy viable | 1. Play focusing on Emmy wins, auteur showrunners, quality dramas<br>2. Track network identity and budget<br>3. Reach Season 12 | Prestige network survives, lower revenue but sustainable, Emmy wins compensate | P1 |
| BAL-003 | Populist strategy viable | 1. Play focusing on ratings, reality TV, broad procedurals<br>2. Track network identity and budget<br>3. Reach Season 12 | Populist network thrives, high revenue, low prestige, sustainable | P1 |
| BAL-004 | Mixed strategy optimal | 1. Play balancing prestige and populist shows<br>2. Compare outcomes to pure strategies<br>3. Analyze | Mixed strategy achieves higher overall scores across identity axes | P1 |
| BAL-005 | Writers' strike impact | 1. Play through Seasons 7-8 (2007-2008 strike)<br>2. Track disruption to scripted pipeline<br>3. Observe adaptation | Strike devastates scripted-only networks, reality-balanced networks survive, feels impactful | P1 |

### 4.2 Balance Edge Cases

| TC ID | Test Case | Steps | Expected Result | Priority |
|---|---|---|---|---|
| BAL-901 | Zero-prestige run | 1. Never greenlight quality dramas, only cheap reality<br>2. Track network identity and showrunner pool<br>3. Reach Season 6 | Network suffers in late game (talent pool shallow, critics hostile), challenging but viable | P2 |
| BAL-902 | Zero-reality run | 1. Never greenlight reality TV, only scripted<br>2. Survive writers' strike<br>3. Track outcomes | Strike is devastating, player must adapt or fail, intentional challenge | P2 |
| BAL-903 | Max-difficulty run (all rivals optimal) | 1. Play with AI difficulty set to Season 12 logic from start<br>2. Compete for 12 seasons<br>3. Track win rate | Challenging but beatable, skilled player can succeed ~40-50% of time | P2 |
| BAL-904 | Speedrun (fastest to 10 Emmys) | 1. Optimize for Emmy wins only<br>2. Track time to 10 Emmys<br>3. Analyze | Achievable in 4-6 seasons with optimal strategy | P2 |

---

## 5. Stress Testing & Stability

### 5.1 Performance Stress Tests

| TC ID | Test Case | Steps | Expected Result | Priority |
|---|---|---|---|---|
| STR-001 | 1000-week simulation | 1. Via debug, simulate 1000 weeks continuously<br>2. Monitor memory usage, CPU usage<br>3. Check for leaks | No memory leaks, performance stable, completes without crash | P1 |
| STR-002 | Save file bloat test | 1. Play to Season 12 (max content)<br>2. Save every week (420 saves)<br>3. Check file sizes | Save files remain <2MB, load times <3 seconds | P1 |
| STR-003 | Pathological AI schedule | 1. Force all 3 rivals to schedule 21 high-rated shows<br>2. Simulate season<br>3. Monitor performance | Simulation handles extreme competition without crash or slowdown | P2 |
| STR-004 | 500 talent entities | 1. Via debug, generate 500 showrunners + actors<br>2. Simulate season with event rolls<br>3. Monitor performance | System handles large talent pool, event rolls complete in <100ms/week | P2 |

### 5.2 Stability Stress Tests

| TC ID | Test Case | Steps | Expected Result | Priority |
|---|---|---|---|---|
| STR-101 | Repeated save/load during gameplay | 1. Play normally, save/load every 30 seconds for 10 minutes<br>2. Observe<br>3. Check stability | No crashes, no corruption, gameplay unaffected | P1 |
| STR-102 | Rapid input spam | 1. Click/drag 100 times in 5 seconds<br>2. Observe UI and simulation<br>3. Check for crashes | UI remains responsive, no crashes, input queue handled correctly | P1 |
| STR-103 | Alt-tab spam | 1. Alt-tab in/out of game 20 times in 30 seconds<br>2. Check for crashes or hangs<br>3. Observe | Game suspends/resumes correctly, no loss of state | P1 |
| STR-104 | Minimize to tray for 24 hours | 1. Minimize game<br>2. Leave for 24 hours<br>3. Restore and check | Game resumes correctly, no memory leak, state preserved | P2 |

---

## 6. Bug Severity Classification

### Priority Definitions

| Severity | Definition | Examples | Response Time |
|---|---|---|---|---|
| **P0 (Critical)** | Crash, data loss, blocks progression, corrupts save | Game crashes on save, infinite loop in simulation, save file unloadable | Fix immediately, block release |
| **P1 (High)** | Major functionality broken, severe balance issue, progression impeded | Drag-and-drop doesn't work, ratings calculation wrong, firing triggers incorrectly | Fix within 1 week, high priority |
| **P2 (Medium)** | Feature works but has issues, minor balance problems, polish issues | Tooltip text wrong, animation jittery, AI makes suboptimal choice | Fix within 2 weeks, medium priority |
| **P3 (Low)** | Cosmetic, quality-of-life, edge case that rarely occurs | Typo in text, icon misaligned, rare scenario has no feedback | Fix when time allows, backlog |

### Bug Triage Rules

1. **Any P0 bug blocks release.** No exceptions.
2. **P1 bugs must be fixed or waived by design lead before RC.**
3. **P2 bugs are evaluated case-by-case for release.**
4. **P3 bugs are backlogged for post-launch patches.**

---

## 7. Test Environments & Tools

### 7.1 Test Hardware

| Spec Tier | CPU | RAM | GPU | Purpose |
|---|---|---|---|---|
| **Minimum** | Intel i5-6500 | 4GB | Intel HD 530 | Validate min spec performance (30 FPS target) |
| **Recommended** | Intel i5-9400 | 8GB | GTX 1050 | Validate rec spec performance (60 FPS target) |
| **High-End** | Ryzen 7 5800X | 16GB | RTX 3060 | Stress testing, future-proofing |
| **Steam Deck** | Custom AMD APU | 16GB | RDNA 2 | Deck-specific testing (60 FPS @ 800p) |

### 7.2 Test Tools

| Tool | Purpose | Usage |
|---|---|---|
| **Unity Profiler** | Performance profiling (frame time, memory, GC) | Run during drag-and-drop, simulation, UI updates |
| **Debug Console** | In-game commands (fast-forward, spawn shows, modify budgets) | Trigger edge cases, stress test systems |
| **Save File Editor** | Manually edit JSON saves for edge case testing | Inject NaN values, corrupt data, test migration |
| **Automated Test Suite** | Unit tests for simulation math, serialization | Run pre-commit, validate formulas |
| **Bug Tracker (Jira/GitHub)** | Log bugs, track repro steps, assign priority | Central bug database |
| **Playtester Survey Tool** | Collect qualitative feedback (readability, engagement) | Google Forms or Typeform |

### 7.3 Automated Testing

**What we automate:**
- **Unit tests** for ratings formulas, adjacency calculations, economy math
- **Save/load stress test** (100 cycles, validate checksums)
- **Simulation determinism test** (same input = same output)
- **Performance regression test** (flag if frame time exceeds budget)

**What we DON'T automate (manual testing required):**
- Subjective readability ("Can you identify your weakest night in 5 seconds?")
- Emotional impact ("Did the cancellation sting?")
- AI believability ("Do rival networks feel smart?")
- Balance feel ("Is prestige vs. populist balanced?")

---

## 8. QA Milestones

### Milestone 1: Prototype (Month 3)

**Test Focus:** Core loop (The Board)

**Test Cases:** BRD-001 to BRD-006, BRD-101 to BRD-105, UI-001 to UI-004

**Success Criteria:**
- Drag-and-drop feels responsive (zero frame drops)
- Adjacency math is correct and visible
- 5-second readability test: 80% pass rate

**Deliverable:** Playtest report with performance profile, readability survey results

---

### Milestone 2: Vertical Slice (Month 6)

**Test Focus:** One full season playable

**Test Cases:** All BRD, RE-001 to RE-005, PP-001 to PP-105, SAV-001 to SAV-005, UI-101 to UI-205

**Success Criteria:**
- Full season completable (2-4 hours)
- Save/load works 100% reliably
- Week simulation <200ms
- Player wants to play Season 2 immediately

**Deliverable:** Vertical slice playtest report, balance data analysis, bug log

---

### Milestone 3: Full Feature (Month 12)

**Test Focus:** All systems online, 3-season playthrough

**Test Cases:** All test cases in sections 2.1-2.7, INT-001 to INT-005, BAL-001 to BAL-005

**Success Criteria:**
- 3-season playthrough completable (6-12 hours)
- All 5 core systems integrated and stable
- Competitor AI makes believable decisions
- No P0 or P1 bugs

**Deliverable:** Full feature playtest report (10+ testers), balance pass recommendations, bug triage

---

### Milestone 4: Content Complete (Month 16)

**Test Focus:** Full 12-season career, balance tuning, stress testing

**Test Cases:** All BAL tests, all STR tests, platform-specific (PC, DECK)

**Success Criteria:**
- 12-season career completable (25-40 hours)
- Multiple strategies viable
- Zero P0 bugs, <5 P1 bugs
- Performance meets targets on min/rec spec

**Deliverable:** Balance report, stress test results, platform compatibility matrix

---

### Milestone 5: Release Candidate (Month 18-20)

**Test Focus:** Final bug sweep, polish, quality gates

**Test Cases:** All test cases (regression pass), edge cases, platform-specific

**Success Criteria:**
- **All 6 quality gates pass** (see section 1.2)
- Zero P0, zero P1 bugs
- 60 FPS on rec spec, 30 FPS on min spec
- Steam Deck verified

**Deliverable:** RC sign-off, final bug report, launch readiness checklist

---

## 9. Risk Assessment (QA Perspective)

### High-Risk Areas

| Risk | Severity | Mitigation | Owner |
|---|---|---|---|
| **UI performance during drag drops frames** | Critical | Profile early (week 2), throttle recalcs if needed, validate on min spec | Engineering |
| **Save file corruption in long campaigns** | Critical | 100-cycle stress test, JSON validation, 3 autosave slots, cloud backup | Engineering |
| **Procedural generation feels repetitive by Season 8** | High | Generate 500 pilots, survey for "sameyness", add weird pilot roll | Design + QA |
| **Ratings engine is opaque to players** | High | Usability testing, tooltip clarity, advisor mode as fallback | Design + QA |
| **Late-game DVR shift feels unfair** | Medium | Playtest Seasons 8-12 specifically, industry memos to explain shift | Design |

### Testing Bottlenecks

1. **Manual playtesting is slow.** 12-season campaign = 30 hours per tester. Budget for 10+ testers in parallel.
2. **Balance tuning requires data.** Can't balance until we have 20+ full playthroughs. Plan for balance pass at Month 14-16.
3. **Edge case discovery is emergent.** Players will break the game in ways we can't predict. Plan for bug fix sprints post-alpha.

---

## 10. Post-Launch QA Strategy

### Patch 1.1 (Month 1 Post-Launch)

**Focus:** Critical bug fixes, balance hotfixes

**Monitoring:**
- Player crash reports (Steam, in-game telemetry)
- Save file corruption reports
- Balance complaints (forums, Reddit, Discord)

**Response:**
- Hotfix P0 bugs within 48 hours
- Balance patch within 2 weeks based on aggregate data
- Add optional Advisor Mode if ratings confusion is widespread

### Patch 1.2 (Month 3 Post-Launch)

**Focus:** Quality-of-life improvements

**Features:**
- Fast-forward button (skip low-event weeks)
- Rewind to last season (undo regret)
- More granular stat tooltips
- Additional achievements

**Testing:** Full regression pass (all test cases), focus on new features

---

## 11. Final QA Checklist (Pre-Launch)

**Before the game ships, CRASH signs off on:**

- [ ] **All 6 quality gates passed** (see section 1.2)
- [ ] **Zero P0 bugs** (crash, corruption, progression-blocking)
- [ ] **Zero P1 bugs** or all P1 bugs explicitly waived by design lead
- [ ] **100-cycle save/load stress test passed** (zero corruption)
- [ ] **Performance targets met** (60 FPS rec spec, 30 FPS min spec)
- [ ] **Steam Deck verified** (controller + touch work, 60 FPS @ 800p, battery >4 hours)
- [ ] **Full 12-season playthrough completed** by at least 3 testers
- [ ] **Balance confirmed** (prestige and populist strategies both viable)
- [ ] **UI readability validated** (80% pass 5-second test)
- [ ] **Automated test suite green** (unit tests, determinism tests)
- [ ] **Platform parity confirmed** (Win/Mac/Linux, save portability)
- [ ] **Steam integration tested** (Cloud saves, achievements, overlay)
- [ ] **Day-one patch pipeline ready** (hotfix process validated)

---

## 12. Closing Note

You're building a game where the player makes a hundred decisions a season, compounds them over twelve seasons, and walks away with a legacy they judge themselves. That's 1,200+ decisions, and if any one of them feels arbitrary, unclear, or broken, the whole thing collapses.

I'm not here to tell you the game is good. I'm here to tell you the game is **stable, legible, and fair.** That when a show tanks, the player knows why. That when a save file loads, it loads correctly. That when a showrunner quits, it's because the player burned them, not because a loyalty variable overflowed.

Every test case in this document is a question: What breaks here? What confuses the player here? What happens when they do the worst possible thing here?

We find those breaks. We log them. We fix them. And then we ship a game where the player's only enemy is their own choices, not our bugs.

Define "works."

-- CRASH

---

**Document Version:** 1.0
**Last Updated:** 2026-02-07
**Next Review:** After Prototype Milestone (Month 3)
