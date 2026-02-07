# PREMIERE -- Level Design Document

**Designed by GRID, Level Designer**
**Status: Complete Level Design v1.0**
**Core Spatial Metaphor: The Board as Battleground**

---

## GRID's Note

Let me be clear about what "level design" means when your entire game is a scheduling board.

Most people think level design is about corridors and cover placement. That's true if you're making a shooter. PREMIERE is a management sim where the player never leaves their corner office. The "level" is THE BOARD -- that 7x3 grid of primetime slots under fluorescent light. But that grid is as much a spatial design challenge as any FPS arena. Where does the player LOOK? What's the critical path? How do we pace tension across 35 weeks? How do we breadcrumb mastery from Season 1 to Season 12?

This document treats PREMIERE's progression like I'd treat a 12-level campaign. Each season is a level. Each era shift is a world transition. Each sweeps month is a boss fight. The Board is the map. The rival networks are the terrain. The player's eye movement across the grid is navigation. And every placement decision is a door you can't walk back through.

Where does the player LOOK first? At the Thursday 9 PM slot -- it's always been television's crown jewel, and the player knows it even if they don't know why. That's your spawn point. The rest of the grid unfolds from there.

What's the pacing? The loop operates at four timescales. The 30-second loop (card placement) is tactical -- room-to-room combat. The 5-minute loop (weekly resolution) is encounter-level -- clear this room, loot the rewards, take the wounds. The season loop is level-length -- navigate from entrance to exit, boss fight at the end. The meta loop is campaign-length -- twelve levels that tell one escalating story.

Let's design the map.

---

## 1. THE BOARD AS SPATIAL DESIGN

### 1.1 The Grid Layout

```
                  THE BOARD -- PRIMETIME SCHEDULING GRID

        MON     TUE     WED     THU     FRI     SAT     SUN
    +-------+-------+-------+-------+-------+-------+-------+
8PM |       |       |       |       |       |       |       |
    |       |       |       |       |       |       |       |
    +-------+-------+-------+-------+-------+-------+-------+
9PM |       |       |       |       |       |       |       |
    |       |       |       |       |       |       |       |
    +-------+-------+-------+-------+-------+-------+-------+
10PM|       |       |       |       |       |       |       |
    |       |       |       |       |       |       |       |
    +-------+-------+-------+-------+-------+-------+-------+

    BENCH AREA (holding zone for unscheduled shows)
    +-----------------------------------------------+
    |  [Show Card] [Show Card] [Show Card] ...     |
    +-----------------------------------------------+
```

This is not just a grid. This is a tactical map with hot zones, dead zones, kill zones, and safe zones.

### 1.2 Territorial Value Map

The grid has inherent strategic geography. Not all slots are created equal.

**Premium Real Estate (High Value, High Competition):**
- **Thursday 9 PM** -- The crown jewel. Historically the highest-value advertising slot in television. This is the hill you fight for. Every rival network stacks their flagship here.
- **Thursday 8 PM** -- The throne room's anteroom. Critical for lead-in flow to the 9 PM slot.
- **Sunday 9 PM** -- Prestige slot. Lower total viewers than Thursday but higher cultural cachet. Where you put the Emmy bait.

**Competitive Battlegrounds (Medium Value, Variable Competition):**
- **Monday-Wednesday 8-9 PM** -- Workweek primetime. Strong volume, fierce competition. The scheduling equivalent of urban warfare -- every block contested.
- **Tuesday 10 PM** -- The "cable drama" slot on broadcast. Lower viewership ceiling but advertiser-friendly for serialized storytelling.

**Danger Zones (Low Value, Strategic Sacrifices):**
- **Friday 8-10 PM** -- "The Friday death slot." Younger demographics abandon broadcast on Fridays. This is where shows go to die -- OR where you counterprogramm with older-skewing procedurals that survive because the competition expects you to surrender.
- **Saturday primetime** -- Almost un-schedulable for scripted content. Sports, movies, event programming only. The wasteland.

**The Final Hour:**
- **All 10 PM slots (Mon-Sun)** -- The "adult" hour. Lower total viewers but higher 18-49 concentration. Lead-in decay is brutal (75% retention from 9 PM). This is where you put expensive shows with narrow audiences OR cheap procedurals that grind out margin.

### 1.3 Flow Architecture

The Board is not a collection of individual slots. It is a series of FLOWS. The player's spatial task is to build pipelines.

**Example flow diagram for a Thursday night lineup:**

```
8 PM: Broad Comedy (18M ceiling, wide demo appeal)
    |
    | LEAD-IN FLOW: 12M viewers × 0.72 demo overlap × 0.85 decay = 7.3M bonus
    v
9 PM: Ensemble Drama (12M ceiling, 18-49 female skew)
    |
    | LEAD-IN FLOW: 10M viewers × 0.68 demo overlap × 0.75 decay = 5.1M bonus
    v
10 PM: Edgy Thriller (8M ceiling, narrow 18-34 skew)
```

The player SEES this flow as colored connection lines between cards when they place them. Green lines = strong flow (70%+ retention). Yellow = moderate (50-69%). Red = weak (<50%). The visual goal: turn the entire Board into a web of green lines.

Mastery is when the player stops thinking about individual shows and starts thinking about NIGHTS as single units. "Thursday is my prestige pipeline. Monday is my volume play. Friday is my sacrifice to protect Wednesday."

### 1.4 Sightlines and Attention Flow

Where does the player's eye go when they open The Board?

**Heatmap of player attention (predicted):**
1. **Thursday 9 PM** (primary focus -- the win condition)
2. **Their weakest night** (the problem demanding attention)
3. **Bubble shows** (highlighted in yellow -- renewal/cancellation decision pending)
4. **The bench area** (new shows waiting for placement)
5. **Rival schedules panel** (the competitive landscape)

The UI must support this attention hierarchy. Most important information is LARGEST and CENTRAL. Details are available on hover/click but not visible by default. If the player has to squint, the level design has failed.

**Critical spatial rule:** The player must be able to answer three questions within 5 seconds of looking at The Board:
1. What's my strongest night?
2. What's my weakest night?
3. Where is my biggest competitive threat?

If those three questions take longer than 5 seconds, the visual hierarchy is broken.

---

## 2. SEASON STRUCTURE AS LEVEL PROGRESSION

Each season is a discrete level with a defined entrance, arc, and exit.

### 2.1 Season Anatomy (The 35-Week Map)

Think of each season as a linear level with five distinct zones, each with its own pacing, pressure, and strategic demands.

```
    TENSION CURVE -- SINGLE SEASON (35 WEEKS)

Tension
  |
  |                      SWEEPS              SWEEPS           SWEEPS
  |                        ▲                   ▲                ▲
  |                       ███                 ███              ███
  |                      █████               █████            █████
  |        ████         ███████      ███    ███████          ███████
  |       ██████       █████████    █████  █████████        █████████
  |      ████████     ███████████  ███████████████████      ███████████
  |  ████████████████████████████████████████████████████████████████████
  |__________________________________________________________________
     Sep   Oct   Nov   Dec   Jan   Feb   Mar   Apr   May

     FALL  FALL   NOV  HOLIDAY MID-  FEB   SPRING GRIND  MAY
     PREM  SETTLE SWEEP LULL   SEASON SWEEP             SWEEP/
                                                         FINALE
```

Each zone is a different level design challenge.

---

### ZONE 1: FALL PREMIERE (Weeks 1-4)

**Purpose:** Tutorial + First Blood. The player learns (or re-learns) the core loop while experiencing the highest-stakes launch of the year.

**Emotional Beat:** Excitement. Optimism. "This is the year everything works."

**Pacing:** FAST. New shows are launching 3-5 per week. Overnights arrive every morning. The inbox floods with reactions -- critical reviews, advertiser responses, showrunner check-ins. The player is drinking from a firehose.

**Strategic Focus:** First impressions. New shows get enormous marketing pushes (budgets already spent pre-season). The player's job is NOT to fix problems yet -- it's to WATCH and LEARN which shows are working and which are bleeding out.

**Flow Diagram (Player Journey):**

```
START (Week 1)
    |
    v
Lock fall schedule (inherited from upfront pitch in previous May)
    |
    v
PREMIERE WEEK -- all new shows launch
    |
    v
Overnights arrive -- some shows HIT, some MISS, most are UNCERTAIN
    |
    v
Week 2-4: Watch the numbers stabilize (or not)
    |
    v
First decision point: Do you move a struggling show? Or give it time?
    |
    v
ZONE EXIT: Week 4 ends. You now have DATA. The tutorial is over. The game begins.
```

**Breadcrumbing (Teaching Flow):**
- Week 1: The player is TOLD which shows are "most important" via marketing spend allocation (already locked in). This teaches priority.
- Week 2: The player SEES lead-in effects when the 8 PM show's performance affects the 9 PM show's numbers. This teaches adjacency.
- Week 3: A showrunner calls complaining about a timeslot. This teaches that cards are people.
- Week 4: A rival network makes a schedule change mid-month. This teaches that the landscape is dynamic.

**Difficulty Modifier:**
- **Season 1:** The player's fall lineup is half-filled by the previous executive. The "tutorial level" has training wheels -- some decisions are already made. The player fills gaps and observes.
- **Season 2+:** The player owns the entire fall lineup. No safety net. The tutorial level becomes a pressure test.

**Encounter Breakdown:**

| Event | Timing | Player Choice | Stakes |
|---|---|---|---|
| **Opening Night Overnights** | Week 1, Day 2 | Observe only (no choice yet) | First data. Sets expectations. |
| **Showrunner Ego Event** | Week 2 | Respond to complaint OR ignore | Loyalty shift (-5 to +5) |
| **Advertiser Reaction** | Week 3 | Defend a controversial show OR pull back | Revenue vs. creative integrity |
| **Bubble Show Identified** | Week 4 | Early cancel OR give it time | Budget pressure vs. patience |

**Exit Condition:** Week 4 ends. The player locks their schedule for October OR makes their first major move (swap a show to a new slot). The Fall Premiere zone closes. The Fall Settling zone opens.

---

### ZONE 2: FALL SETTLING (Weeks 5-9)

**Purpose:** The strategic layer emerges. The player stops reacting and starts PLANNING.

**Emotional Beat:** Focus. Control. "I'm starting to see the shape of this."

**Pacing:** MEDIUM. The flood of Week 1 data has slowed to a steady stream. The player has breathing room to think 2-3 weeks ahead instead of surviving day-to-day.

**Strategic Focus:** Optimization. The player identifies their hits and begins building flow architecture around them. Struggling shows get one last chance or get axed. The bench area starts filling with midseason replacements in development.

**Flow Diagram:**

```
Week 5
    |
    v
First REAL schedule adjustment (player-initiated move, not a reaction)
    |
    v
Week 6-7: Watch the results of the adjustment
    |
    v
Week 8: First cancellation decision (struggling show has 4 weeks of data -- enough to judge)
    |
    v
Week 9: Pre-sweeps prep -- lock your best lineup before November
    |
    v
ZONE EXIT: November Sweeps approach. The player enters the first BOSS FIGHT.
```

**Breadcrumbing:**
- Week 5: The UI highlights a poorly-performing show and suggests (via Jordan Park memo) moving it OR cancelling it. This teaches active management.
- Week 6: A rival network's schedule change creates an OPENING -- a weak timeslot the player can exploit. This teaches opportunism.
- Week 8: The first cancellation screen appears with full production values -- showrunner reaction, fan response, Variety headline. This teaches WEIGHT.

**Encounter Breakdown:**

| Event | Timing | Player Choice | Stakes |
|---|---|---|---|
| **First Cancellation** | Week 8 | Cancel the dog OR keep paying for it | Budget relief vs. showrunner loyalty |
| **Midseason Pilot Scouting** | Week 7-9 | Greenlight 3-5 midseason replacements | Planting seeds for January |
| **Competitive Countermove** | Week 6 | Respond to rival's schedule change | Tactical vs. strategic thinking |
| **Marketing Budget Reallocation** | Week 9 | Shift money from a flop to a rising star | Cutting losses vs. sunk cost fallacy |

**Exit Condition:** Week 9 ends. November Sweeps begin. The pacing shifts from strategic to PRESSURIZED.

---

### ZONE 3: NOVEMBER SWEEPS (Weeks 10-13)

**Purpose:** BOSS FIGHT. The first crucible. All three rival networks are at full strength. Every overnight matters. This is what the player has been building toward.

**Emotional Beat:** Pressure. Focus. "Everything I've built is being tested RIGHT NOW."

**Pacing:** INTENSE. The ratings reveals are longer, more detailed, more dramatized. The inbox is chaos -- showrunners demanding attention, advertisers watching closely, Arthur Hamill checking in weekly. The player cannot look away.

**Strategic Focus:** Execution. The player has already locked their schedule. November Sweeps is NOT the time for experiments. The player's job is to MAXIMIZE what they have -- stack event episodes, coordinate crossovers (if stretch goals met), and watch the scoreboard.

**Flow Diagram:**

```
Week 10 (START OF SWEEPS)
    |
    v
Lock all shows at their best timeslots -- no changes during sweeps
    |
    v
Week 10-11: Nightly ratings battles -- WIN or LOSE each night against rivals
    |
    v
Week 12: Mid-sweeps crisis event (a star's scandal, a production delay, a rival's stunt)
    |
    v
Week 13: Final sweeps week -- the scoreboard tallies
    |
    v
SWEEPS RESULTS SCREEN (compare to rivals, set Q4 revenue)
    |
    v
ZONE EXIT: December arrives. Pressure drops. The player exhales.
```

**Breadcrumbing:**
- The UI shifts during sweeps. Competitive comparison becomes the DEFAULT view, not a side panel. The player sees their numbers AGAINST the rivals in real time.
- Event episodes are highlighted. If the player has high-quality shows, the game suggests "this is the week to air your best episode."
- A running scoreboard shows: "You won Monday. Lost Tuesday. Split Wednesday. Thursday PENDING."

**Encounter Breakdown:**

| Event | Timing | Player Choice | Stakes |
|---|---|---|---|
| **Sweeps Stunt Opportunity** | Week 10 | Spend extra marketing $ for an event push | Budget vs. short-term spike |
| **Crisis Event (RNG)** | Week 12 | Respond to actor scandal / production delay | Damage control under pressure |
| **Rival Counterprogramming** | Week 11 | Do you respond mid-sweeps (risky) OR hold position? | Discipline vs. panic |
| **Sweeps Results** | Week 13 end | OBSERVE ONLY (scoring event) | Judgment. Did you win? |

**Victory Condition (Internal Scoring):**
- **Win Sweeps:** Finish 1st in total viewers OR 1st in 18-49 demo. Arthur Hamill praises you. Budget increases. Showrunner loyalty +5 across the board.
- **Place 2nd-3rd:** Acceptable. Budget holds steady. Arthur is neutral.
- **Finish Last:** Arthur calls you into his office. Budget pressure. This is a WARNING.

**Exit Condition:** Week 13 ends. Sweeps results are final. The player enters the HOLIDAY LULL -- the only LOW-PRESSURE zone in the season.

---

### ZONE 4: HOLIDAY LULL (Weeks 14-17)

**Purpose:** RECOVERY + PLANNING. The player catches their breath, reflects on the season so far, and prepares for the second half.

**Emotional Beat:** Quiet. Reflection. "What have I built? What needs to change?"

**Pacing:** SLOW. This is the only zone where the player can SKIP WEEKS if they want. Reruns fill the schedule. Originals are sparse. The ratings don't matter as much (advertisers expect lower numbers during holidays). The game's pressure valve opens.

**Strategic Focus:** Midseason prep. The player finalizes which midseason pilots to air in January, which bubble shows to cancel, and which slots need reinforcement. This is the PLANNING phase before the second act.

**Flow Diagram:**

```
Week 14
    |
    v
Holiday programming (reruns, specials -- autopilot mode available)
    |
    v
Week 15-16: STRATEGY SCREEN unlocked -- review full season data, plan midseason
    |
    v
Week 17: Lock midseason replacement schedule
    |
    v
ZONE EXIT: January approaches. The second launch window opens.
```

**Breadcrumbing:**
- The UI explicitly offers a "COAST THROUGH HOLIDAYS" button that auto-fills the schedule with reruns and lets the player skip to Week 18. This teaches pacing control.
- A strategic overview screen becomes available: "Here's your year so far. Here's what's working. Here's what's dying."
- Jordan Park delivers a midseason recommendations report: "These pilots tested well. These shows are on the bubble. Here's what I'd do."

**Encounter Breakdown:**

| Event | Timing | Player Choice | Stakes |
|---|---|---|---|
| **Midseason Greenlight** | Week 15 | Choose 3-5 pilots to replace cancelled shows | Planting seeds for spring |
| **Bubble Show Review** | Week 16 | Cancel now OR give them the back half of the season | Budget vs. patience |
| **Talent Contract Pre-Negotiation** | Week 17 | Lock in a star early (cheap) OR wait (expensive) | Timing and leverage |
| **Strategic Planning Session** | Week 15-17 | Player sets their midseason GOAL (ratings? prestige? margin?) | Intentionality |

**Exit Condition:** Week 17 ends. The midseason schedule is locked. January launches. The second act begins.

---

### ZONE 5: MIDSEASON LAUNCH (Weeks 18-22)

**Purpose:** SECOND CHANCE. New shows launch to replace the fall failures. This is a mini-version of the Fall Premiere zone, but with less fanfare and more scrutiny.

**Emotional Beat:** Determination. "The first wave didn't work. THIS wave has to."

**Pacing:** RISING. Not as frenetic as Fall Premiere, but the pressure builds week by week toward February Sweeps.

**Strategic Focus:** Course correction. The player is replacing failed shows with midseason entries. The challenge: midseason shows have LOWER marketing budgets and HIGHER audience skepticism. They must be better to succeed.

**Flow Diagram:**

```
Week 18 (MIDSEASON PREMIERE WEEK)
    |
    v
3-5 new shows launch in the slots vacated by cancellations
    |
    v
Week 19-20: Overnights arrive for midseason shows -- do they HOOK or FLOP?
    |
    v
Week 21: Pre-sweeps check-in -- lock the lineup before February
    |
    v
Week 22: February Sweeps START
    |
    v
ZONE TRANSITION: February Sweeps (mini-boss fight, similar structure to November)
```

**Breadcrumbing:**
- Midseason shows have a DIFFERENT success metric than fall shows. The UI makes this clear: "Midseason shows need a 6M floor to justify renewal. Fall shows needed 8M." This teaches context.
- Rival networks are ALSO launching midseason shows. The competitive landscape shifts again.

**Encounter Breakdown:**

| Event | Timing | Player Choice | Stakes |
|---|---|---|---|
| **Midseason Launch** | Week 18 | Which slots get the new shows? | Placement is CRITICAL with limited marketing |
| **Fast Cancellation Decision** | Week 20 | A midseason show is bombing -- cut losses NOW or wait? | Sunk cost vs. brutal pragmatism |
| **February Sweeps Prep** | Week 21 | Do you lean on new shows or old reliables? | Risk vs. safety |

**Exit Condition:** Week 22 ends. February Sweeps resolve (abbreviated version of November's structure). The player enters the SPRING GRIND.

---

### ZONE 6: SPRING GRIND (Weeks 23-30)

**Purpose:** ENDURANCE TEST. The longest, flattest stretch of the season. No sweeps pressure. No launch excitement. Just the weekly loop, grinding forward.

**Emotional Beat:** Fatigue. Routine. "Is it May yet?"

**Pacing:** FLAT. This is INTENTIONAL. The Spring Grind tests whether the player has built a sustainable system or is constantly firefighting. A well-built schedule coasts through the grind. A fragile schedule collapses here.

**Strategic Focus:** Maintenance + Long-term planning. The player makes renewal/cancellation decisions that affect NEXT season. This is where you plant seeds six months ahead.

**Flow Diagram:**

```
Week 23
    |
    v
Week 24-29: THE GRIND (weekly loop, minimal variation, optional fast-forward)
    |
    v
Week 28: Renewal decisions for existing shows (affects next season's budget)
    |
    v
Week 30: Pre-finale planning (which shows get 2-hour finales, which get cliff-hangers)
    |
    v
ZONE EXIT: May Sweeps approach. The final boss fight.
```

**Breadcrumbing:**
- The UI offers FAST-FORWARD during the grind IF the player's schedule is stable. "Your lineup is steady. Skip to Week 28? [YES] [NO]"
- Renewal notices arrive. The game forces the player to commit: "This show is renewed for Season 2" OR "This show is cancelled."
- Trade headlines hint at rival networks' moves for NEXT fall. The meta-game surfaces.

**Encounter Breakdown:**

| Event | Timing | Player Choice | Stakes |
|---|---|---|---|
| **Renewal Wave** | Week 28-29 | Renew 8-12 shows, cancel the rest | Next season's foundation |
| **Talent Holdout** | Week 27 | A star demands a raise mid-season | Budget pressure vs. stability |
| **Showrunner Pitch for Next Season** | Week 26 | A loyal showrunner brings you their next project early | Relationship rewards |

**Exit Condition:** Week 30 ends. May Sweeps begin. The season's final exam.

---

### ZONE 7: MAY SWEEPS & FINALES (Weeks 31-35)

**Purpose:** FINAL EXAM + EMOTIONAL PAYOFF. The season's biggest ratings week. Series finales and cliffhangers stack. The scoreboard determines your annual review.

**Emotional Beat:** Climax. Triumph or failure. "This is what everything was for."

**Pacing:** PEAK INTENSITY. Every overnight matters. Event episodes everywhere. Finales pull 1.3x normal viewership. The player is glued to the results screen.

**Strategic Focus:** Execution + Storytelling. The player has no control left -- the schedule is locked, the episodes are produced. All that remains is watching the result and feeling the weight of what they built.

**Flow Diagram:**

```
Week 31 (MAY SWEEPS START)
    |
    v
Series finales begin airing (returning shows end their seasons)
    |
    v
Week 32-34: Nightly ratings battles -- highest stakes of the year
    |
    v
Week 35 (SEASON FINALE WEEK): 8-12 finales air in one week -- event television
    |
    v
MAY SWEEPS RESULTS SCREEN (full scoring, rival comparison)
    |
    v
ANNUAL REVIEW (Arthur Hamill evaluates your performance)
    |
    v
EMMY CEREMONY (if you had prestige shows, they compete for awards)
    |
    v
SEASON COMPLETE
```

**Breadcrumbing:**
- The UI highlights which shows are airing finales and predicts their performance: "This finale could pull 12M if the lead-in holds."
- A "Finale Tracker" appears showing how many viewers each finale pulled compared to its season average. This tells the player which shows GREW their audience (good sign for renewal) and which LOST viewers (bad sign).

**Encounter Breakdown:**

| Event | Timing | Player Choice | Stakes |
|---|---|---|---|
| **May Sweeps Execution** | Week 31-35 | OBSERVE ONLY (scoring event) | Final judgment |
| **Annual Review** | Post-Week 35 | OBSERVE + RESPOND | Arthur evaluates you -- budget, pressure, praise |
| **Emmy Nominations** | Post-Week 35 | OBSERVE ONLY | Prestige scoring |
| **Upfront Prep** | Post-Week 35 | Begin planning NEXT season's pitch | Meta-loop hook |

**Victory Condition (Annual Review Scoring):**

Arthur evaluates the player across four axes:
1. **Total Viewership** (did you grow the network?)
2. **Profit Margin** (did you make money?)
3. **Prestige** (did you win critical acclaim / Emmy nominations?)
4. **Network Identity** (is your brand coherent?)

The scoring is NOT pass/fail. It is a PROFILE. The player receives a report card:
- "You dominated in ratings but sacrificed prestige."
- "You built a critically acclaimed network but struggled with margins."
- "You grew across all dimensions -- this was your best year yet."

**Exit Condition:** The season ends. The player transitions to the NEXT season OR (if Season 12) to the ENDGAME.

---

## 3. ERA SHIFTS AS WORLD TRANSITIONS

The meta-level structure is 12 seasons spanning 2000-2012. But those 12 seasons are NOT identical levels. The rules CHANGE. The terrain shifts. This is how we maintain challenge and surprise across 30+ hours.

Think of era shifts like moving from one biome to another in a large open-world game. The core verbs stay the same (schedule, watch ratings, respond), but the CONTEXT changes everything.

### 3.1 Era Map (12-Season Campaign Structure)

```
ERA 1: THE GOLDEN AGE RUSH (Seasons 1-3, 2000-2003)
    ├─ Season 1: Learning the Board (tutorial level)
    ├─ Season 2: Full grid unlocked (first real level)
    └─ Season 3: Reality TV explosion (new mechanics introduced)

ERA 2: THE PRESTIGE WARS (Seasons 4-6, 2003-2006)
    ├─ Season 4: Cable competition intensifies (AI rivals get smarter)
    ├─ Season 5: DVR adoption begins (metrics start shifting)
    └─ Season 6: Prestige arms race (quality ceiling raises, costs escalate)

ERA 3: THE CRISIS (Seasons 7-8, 2006-2008)
    ├─ Season 7: Strike warning signs (labor tension surfaces)
    └─ Season 8: WRITERS' STRIKE (crucible level -- survival mode)

ERA 4: THE RECKONING (Seasons 9-12, 2008-2012)
    ├─ Season 9: Post-strike recovery (landscape permanently altered)
    ├─ Season 10: DVR mainstreaming (revenue model shifts)
    ├─ Season 11: Streaming rumblings (poaching begins)
    └─ Season 12: THE FINAL SEASON (existential difficulty spike)
```

### 3.2 Era Shift Design Principles

Each era shift must:
1. **Change a core system** -- not just flavor, but actual mechanical alteration
2. **Be telegraphed** -- the player sees it coming 1-2 seasons ahead via headlines and minor events
3. **Force adaptation** -- strategies that worked in the previous era become suboptimal
4. **Unlock new tools** -- the player gets new mechanics to handle new threats

**Example: The DVR Shift (Seasons 5-10)**

```
SEASON 5 (2004): DVR Adoption = 10%
    - Headline appears: "TiVo sales surge -- advertisers nervous"
    - Mechanical effect: MINOR. Live ratings drop 2-3% on serialized dramas.
    - Player response: Awareness. No action needed yet.

SEASON 6 (2005): DVR Adoption = 18%
    - New metric unlocked: "Live+3" ratings shown alongside live ratings
    - Mechanical effect: MODERATE. 5-8% divergence between live and L+3.
    - Player response: Start tracking both metrics.

SEASON 7 (2006): DVR Adoption = 25%
    - Advertiser events fire: "We want assurances about live viewing"
    - Mechanical effect: SIGNIFICANT. Revenue tied to live ratings, but L+7 shows true audience.
    - Player response: Strategic tension -- prestige shows pull better in L+7 but earn less $.

SEASON 8 (2007): DVR Adoption = 32%
    - Writers' Strike compounds the issue (content scarcity makes DVR even more valuable)
    - Mechanical effect: MAJOR. Revenue model starts shifting toward L+3 partial credit.

SEASON 9-10 (2008-2010): DVR Adoption = 40%+
    - Revenue model FULLY shifts to L+7 as industry standard
    - Mechanical effect: TRANSFORMATIVE. Serialized prestige dramas are now VIABLE in ways they weren't in Season 1.
    - Player response: If the player adapted early (invested in prestige + serialization), they BENEFIT. If they resisted, they're now behind the curve.
```

This is level design through systems, not geometry. But the principle is identical: the terrain changes, and mastery is adaptation.

---

## 4. COMPETITIVE SCENARIOS (Encounter Design)

The rival networks are not static obstacles. They are AI-driven opponents with strategies, personalities, and the capacity to SURPRISE the player. Each rival is a different encounter type.

### 4.1 Rival Network Profiles (Enemy Archetypes)

**AmeriNet -- "The Juggernaut"**
- **Strategy:** Volume + Safety. They flood the schedule with procedurals and broad comedies. They NEVER take risks.
- **Threat Type:** Attrition. They don't spike -- they grind. Every night, they pull 8-10M viewers with formulaic content. You can't ignore them.
- **Counterstrategy:** Counterprogramm with niche demos they ignore (18-34, female-skewing) OR outspend them in sweeps with event programming.
- **Behavioral Tell:** AmeriNet clones your hits 6 months after you launch them. If your procedural succeeds, they'll have a knockoff by midseason.

**Crowne Broadcasting -- "The Prestige Hunter"**
- **Strategy:** Quality over quantity. They greenlight expensive auteur-driven dramas and chase Emmys.
- **Threat Type:** Talent Poaching. They offer no-notes deals to your best showrunners. They win awards that boost their CPM.
- **Counterstrategy:** Build showrunner loyalty EARLY so they resist Crowne's offers. OR compete directly for prestige and win the arms race.
- **Behavioral Tell:** Crowne schedules their best shows on Sunday nights (the prestige slot). If they're weak on Sundays, they're vulnerable.

**Pacific Television -- "The Disruptor"**
- **Strategy:** Chaos. Reality TV, stunt programming, genre experiments. They throw everything at the wall.
- **Threat Type:** Unpredictability. You can't model their behavior. They'll launch a reality show at 8 PM on Tuesday that pulls 12M viewers out of nowhere.
- **Counterstrategy:** DON'T try to predict them. Build a flexible schedule that can absorb shocks. Keep midseason replacements ready.
- **Behavioral Tell:** Pacific goes quiet for 2-3 weeks, then drops a scheduling bomb (a surprise launch or a major move). Watch for the silence.

### 4.2 Scenario Design: Competitive Events

**SCENARIO: The Clone War (Mid-Game Event)**

**Trigger:** Player launches a procedural that pulls 10M+ viewers for 4+ consecutive weeks.

**Event:**
```
VARIETY HEADLINE: "AmeriNet Greenlights 'Badge Protocol' -- Insiders Say It's A 'Cold Open' Clone"

[Six weeks later]

AmeriNet's clone launches in direct competition against your original show.
```

**Player Decision:**
- **OPTION A:** Move your original show to avoid the clone (surrender the slot, protect the show)
- **OPTION B:** Stay and fight (ratings war -- both shows suffer, but yours has loyalty advantage)
- **OPTION C:** Counterprogramm THEIR other nights (ignore the clone, attack elsewhere)

**Outcome Matrix:**

| Choice | Short-term Effect | Long-term Effect |
|---|---|---|
| Move | Your show's ratings drop 15% (weaker slot). Clone dominates the abandoned slot. | You avoid the bloodbath. Show survives. |
| Fight | Both shows drop 20-25%. Ratings war. | If your Quality Rating is higher, you win long-term. If not, you both bleed. |
| Counterprogramm | Your show takes a 30% hit (facing the clone alone). BUT you damage AmeriNet's other nights. | Strategic sacrifice. You lose the battle but weaken their overall position. |

**Lesson Taught:** Competition is not just about YOUR schedule. It's about the WHOLE landscape.

---

**SCENARIO: The Poaching Offer (Late-Game Event)**

**Trigger:** Player has a high-loyalty showrunner (Loyalty 60+) with a hit show (8M+ viewers, QR 75+).

**Event:**
```
PHONE CALL: [Showrunner's Name]

"I need to tell you something. Crowne offered me a deal. Full creative control, no notes, two-season guarantee, budget 30% higher than what we have here. I haven't said yes. But I wanted you to hear it from me. What are you offering me to stay?"
```

**Player Decision:**
- **OPTION A:** Match the offer (massive budget hit, but keep the talent)
- **OPTION B:** Counter with creative perks instead of money (no budget hit, but requires high Loyalty to work)
- **OPTION C:** Let them go (lose the showrunner, show's QR drops -15, Loyalty with other talent -10)
- **OPTION D:** Call their bluff (risky -- 40% chance they leave anyway)

**Outcome Matrix:**

| Choice | Immediate Cost | Long-term Effect |
|---|---|---|
| Match Offer | $4-6M/season budget increase | Showrunner stays. Show quality holds. Other talent sees you reward loyalty. |
| Creative Perks | $0 budget cost, but only works if Loyalty > 65 | If it works, showrunner stays and deepens loyalty (+15). If it fails, they leave bitter. |
| Let Them Go | Lose showrunner + show QR penalty | Budget relief. But the show declines, and talent across the network questions your commitment. |
| Call Bluff | 60% chance they stay, 40% they leave immediately | High risk, high reward. If you're right, they respect the power move (+10 Loyalty). If you're wrong, catastrophic. |

**Lesson Taught:** Talent management is poker. You're playing the player behind the showrunner, not just the stats.

---

## 5. DIFFICULTY CURVES & MASTERY GATING

The game must feel ACCESSIBLE at Hour 1 and DEEP at Hour 30. This is a mastery curve, not a difficulty ramp.

### 5.1 Teaching vs. Testing

**Teaching Levels (Seasons 1-2):**
- Reduced grid size (Season 1 starts with 5 nights × 2 slots = 10 slots, not 21)
- Only 2 rival networks visible (the third is "inactive" for narrative reasons)
- Forgiving budget (you can't be fired in Season 1)
- Explicit tutorials via Jordan Park memos: "Here's why that move worked" or "Here's what went wrong"

**Testing Levels (Seasons 3-8):**
- Full complexity unlocked
- All systems active simultaneously (talent, budget, rivals, pilots, ratings, DVR metrics)
- Firing threshold is active (you can lose)
- The game stops explaining and starts EXPECTING

**Mastery Levels (Seasons 9-12):**
- Meta-game surface: You're not just managing a season, you're managing a LEGACY
- Era shifts punish outdated strategies
- The game introduces NEW mechanics (streaming poaching in Season 11) even at the end to prevent stagnation
- Victory is not "survive" -- it's "thrive under paradigm shift"

### 5.2 Mastery Gating (How We Know the Player Is Ready)

The game tracks player performance across multiple dimensions and uses THRESHOLDS to gate difficulty spikes.

**Threshold 1: Lead-In Mastery (Required for Season 3 complexity)**

The player must demonstrate understanding of lead-in flow by achieving:
- Three consecutive nights where lead-in retention > 70% (green flow lines)
- OR deliberately building a counterprogramming strategy (explicitly choosing LOW retention to capture a different demo)

If the player hasn't hit this threshold by the end of Season 2, the game TUTORIALIZES it in Season 3's opening via a Jordan Park intervention: "I ran the numbers. If you move Show X to follow Show Y, the demo overlap is 82%. That's a huge lead-in bonus. Want me to show you the math?"

**Threshold 2: Budget Management (Required for Season 5 talent pressure)**

The player must demonstrate sustainable budgeting by:
- Ending two consecutive seasons with profit > $5M
- OR ending one season with profit > $15M

If the player is consistently broke, the talent negotiation events in Season 5+ are SOFTENED (smaller raises, longer contracts). This prevents death spirals.

**Threshold 3: Competitive Awareness (Required for Season 8 strike survival)**

The player must demonstrate they're tracking rival behavior by:
- Making at least one counterprogramming move per season (deliberately scheduling AGAINST a rival's strength)
- OR poaching a rival's talent at least once

If the player hasn't done this by Season 7, the game TEACHES it via an Arthur Hamill conversation: "Crowne is launching a prestige drama on Sundays. That's their flagship night. You have two options: avoid them, or hit them where they're weak. What's your read?"

### 5.3 Difficulty Modifiers (Optional Player Control)

The game offers THREE difficulty modes that affect AI rival behavior and budget pressure:

**BROADCAST MODE (Normal Difficulty):**
- Rival AI plays competently but makes occasional mistakes
- Budget threshold for firing: -$10M for two consecutive seasons
- Talent loyalty shifts are moderate (±10 typical range)

**CABLE MODE (Hard Difficulty):**
- Rival AI plays optimally and adapts to player strategies
- Budget threshold for firing: -$5M for two consecutive seasons OR finish last place once
- Talent loyalty shifts are volatile (±20 range, big swings for big decisions)
- Prestige shows cost 20% more (reflecting cable's premium market)

**STREAMING MODE (Narrative Difficulty):**
- No firing threshold (you can't lose your job)
- Budget is always positive (you can experiment freely)
- Rival AI is softened (makes more mistakes)
- **PURPOSE:** This mode is for players who want to experience the STORY without the strategic pressure. It is not a "training mode" -- it is a different experience. The player can still FAIL (shows can bomb, talent can leave), but they can't get FIRED.

---

## 6. PACING BREAKDOWNS (Moment-to-Moment Flow)

The player's experience operates at FOUR timescales simultaneously. Each has its own pacing rhythm.

### 6.1 The 30-Second Loop (Tactical Pacing)

**VERB:** Drag card, read stats, place card, see ripple.

**PACING GOAL:** This must feel TACTILE and IMMEDIATE. No lag. No loading. The feedback loop is instant.

**Interaction Flow:**
```
[Player hovers over a show card in the bench area]
    ↓
[Card enlarges slightly, full stats visible on hover -- 0.1 sec delay]
    ↓
[Player drags card toward a grid slot]
    ↓
[As the card moves OVER a slot, that slot highlights and shows PREDICTED impact]
    ↓
[Player drops card into slot]
    ↓
[Card SNAPS into place with subtle sound effect -- 0.2 sec animation]
    ↓
[Adjacent slots' stats UPDATE with number changes (green +X.X M viewers, red -X.X M)]
    ↓
[Competitive threat panel on right side REFRESHES (0.3 sec delay)]
    ↓
[If this placement creates a strong flow chain, connecting lines appear between cards]
    ↓
[Total time: 1.5 seconds from drop to full feedback resolution]
```

**Pacing Rule:** The player must SEE the consequences of their action within 2 seconds. If feedback takes longer, the loop feels sluggish.

**Variance Injection:** Not every card placement is dramatic. 70% of placements are routine -- the player is filling slots, optimizing incrementally. But 30% of placements trigger EVENTS:
- "This move angers the showrunner" (loyalty event fires)
- "This creates a perfect lead-in chain" (achievement notification)
- "You just scheduled against AmeriNet's flagship -- this is a BATTLE" (competitive warning)

The variance keeps the loop from feeling mechanical.

### 6.2 The 5-Minute Loop (Encounter Pacing)

**VERB:** Lock schedule, simulate week, receive ratings, respond to events.

**PACING GOAL:** This is the "room clear" loop. The player must feel a sense of COMPLETION and CONSEQUENCE at the end of each cycle.

**Interaction Flow:**
```
[Player locks weekly schedule -- button press OR auto-lock if no changes made]
    ↓
[WEEK SIMULATION -- 2-4 seconds of compressed time, calendar animates forward]
    ↓
[OVERNIGHT RATINGS REVEAL SCREEN appears]
    ↓
[Ratings appear SEQUENTIALLY by night -- Monday first, then Tuesday, etc.]
    ↓ (3-8 seconds depending on number of shows)
[Summary screen: "You won 3 nights, lost 2, split 2. Total weekly viewers: 47.3M."]
    ↓
[EVENT INBOX appears -- 2-6 events waiting (talent calls, advertiser memos, headlines)]
    ↓
[Player TRIAGES events -- respond to urgent ones, file the rest]
    ↓ (1-3 minutes depending on event complexity)
[Player optionally adjusts schedule for next week]
    ↓
[LOOP REPEATS]
```

**Pacing Rule:** The entire 5-minute loop should take 3-7 minutes depending on event density. If it's taking 10+ minutes, there's too much friction (too many events, too much required reading).

**Dynamic Pacing:** Event density is NOT constant. It follows the season tension curve:
- **Fall Premiere / Sweeps:** HIGH event density (4-6 events per week)
- **Settling / Grind:** MEDIUM event density (2-4 events per week)
- **Holiday Lull:** LOW event density (0-2 events per week, often skippable)

This creates natural breathing room.

### 6.3 The Session Loop (Play Session Pacing)

**VERB:** Play for 30-90 minutes, experience a narrative arc, reach a stopping point.

**PACING GOAL:** Each play session should feel like a chapter. It has a beginning (a goal), middle (pursuit of that goal), and end (resolution or cliffhanger).

**Natural Stopping Points (Save-and-Quit Moments):**

| Stopping Point | Why It Works | Frequency |
|---|---|---|
| **End of a Sweeps Month** | Natural climax + resolution. Scoreboard is final. Player knows where they stand. | 3 per season |
| **End of Midseason Launch Week** | New shows have premiered, first overnights are in. Clear checkpoint. | 1 per season |
| **After a Major Event Resolution** | Talent crisis resolved, contract signed, big decision made. Emotional closure. | Variable, 2-4 per season |
| **End of Season (Annual Review)** | MAJOR stopping point. Full closure. Season-long arc complete. | 1 per season (12 per campaign) |

**Anti-Pattern to Avoid:** The player should NEVER feel trapped in the middle of a crisis with no way to pause. Every major event sequence should have an "I'll handle this later" option that files it for the next session.

**Session Length Targets:**
- **Minimum viable session:** 15 minutes (complete 1-2 weeks, make a decision, save at a checkpoint)
- **Typical session:** 45-60 minutes (complete 4-8 weeks, navigate an event sequence, reach a sweeps boundary)
- **Deep session:** 90-150 minutes (complete a full season zone, 10-15 weeks, sweeps event included)

### 6.4 The Campaign Loop (Multi-Session Pacing)

**VERB:** Play across multiple sessions, build a network identity over seasons, experience the full 12-season arc.

**PACING GOAL:** The player should feel PROGRESSION across the campaign -- not just "more of the same," but "the same verbs in increasingly complex/meaningful contexts."

**Progression Markers (Milestones That Signal Progress):**

| Milestone | When | What It Signals |
|---|---|---|
| **First Emmy Win** | Season 2-4 (typically) | "I've built something prestigious." |
| **First $20M+ Profit Season** | Season 3-5 (typically) | "I've built something sustainable." |
| **First Talent Loyalty > 80** | Season 4-6 (typically) | "I've built a relationship that transcends transactions." |
| **Surviving the Writers' Strike** | Season 8 (forced) | "I adapted to a paradigm shift." |
| **Reaching Season 10** | Fixed | "I've lasted a decade. I'm a veteran." |
| **Completing Season 12** | Fixed | "I saw the era through to its end." |

**Narrative Checkpoints (Story Beats Across Campaign):**

```
SEASON 1: The Corner Office Is Yours
    ↓
SEASON 3: Reality TV Changes Everything (first paradigm test)
    ↓
SEASON 5: Vanessa Cole Contract Negotiation (first human relationship climax)
    ↓
SEASON 8: The Writers' Strike (crucible -- survival test)
    ↓
SEASON 10: Jordan Park's Rival Offer (mirror moment -- what have you taught them?)
    ↓
SEASON 12: The Reckoning (legacy evaluation)
```

Each narrative checkpoint is a BEAT in a 12-act structure. The player is not just managing seasons -- they are LIVING a career.

---

## 7. BREADCRUMBING STRATEGY (Teaching Without Telling)

The game must teach the player HOW to master it without EXPLAINING mastery. Breadcrumbs, not tutorials.

### 7.1 Visual Breadcrumbs (The Board as Teacher)

**COLOR CODING:**
- **Green numbers** = improvement, success, positive flow
- **Red numbers** = decline, failure, negative consequence
- **Yellow highlights** = warning, attention needed, bubble show
- **Gray cards** = inactive/reruns (low priority)

The player learns to SCAN for yellow and red first. The eye is trained by color before the brain engages.

**FLOW LINES:**
- Shows with strong lead-in chains are connected by visible green lines
- Weak connections show yellow/red lines
- No line = no adjacency benefit

The player learns flow architecture by SEEING it, not by reading a tutorial.

**CARD ARRANGEMENT:**
- High-performing shows have a subtle GLOW (success feedback)
- Bubble shows PULSE slowly (anxiety/urgency signal)
- Cancelled shows FADE OUT over 2 seconds (grief/finality)

Every visual element tells the player something about the state of their schedule WITHOUT a single word.

### 7.2 Systemic Breadcrumbs (Consequences as Lessons)

**Example: Teaching Lead-In Flow**

```
SEASON 1, WEEK 3

The player has a strong 8 PM comedy pulling 10M viewers and a weak 9 PM drama pulling 4M viewers.

The player receives a Jordan Park memo:

"The 9 PM drama's demo skew matches the comedy's audience almost perfectly (78% overlap).
If we keep this pairing, the lead-in should stabilize that drama around 7M by Week 6.
Just flagging it -- no action needed, but watch the trend."

[No tutorial. No forced action. Just: here's a pattern. Watch it happen.]

Week 6 arrives. The drama is now pulling 6.8M. The prediction was right.

The player has learned lead-in theory BY EXPERIENCING IT, not by reading it.
```

**Example: Teaching Competitive Counterprogramming**

```
SEASON 2, WEEK 8

AmeriNet launches a male-skewing action procedural at Thursday 9 PM. It pulls 12M viewers.

The player's Thursday 9 PM show (also male-skewing) drops from 9M to 6M overnight.

Arthur Hamill calls:

"Thursday's a bloodbath. AmeriNet is eating our lunch with that cop show.
You have two moves: find a better show to fight them, or target a different audience they're ignoring.
Your call."

[The game has NAMED the strategy (counterprogramming) and presented two paths. The player chooses.]

If the player moves a female-skewing drama into Thursday 9 PM, that show pulls 8M viewers
(lower ceiling than the action show would have, but higher floor because it's not competing for the same demo).

The player has learned counterprogramming BY DOING IT.
```

### 7.3 Narrative Breadcrumbs (Characters as Guides)

Each major character serves as a breadcrumb for a different system:

| Character | System They Teach | How They Teach It |
|---|---|---|
| **Jordan Park** | Strategic meta-game (pipeline, long-term planning) | Memos that highlight patterns: "This genre is saturating. Next season's pilot pool will be weaker in procedurals." |
| **Arthur Hamill** | Business system (budget, margins, profitability) | Quarterly calls that frame decisions in financial terms: "That prestige drama costs $3M/episode and pulls 5M viewers. The margin is brutal. Is it worth it?" |
| **Margaux Lessard** | Quality vs. Commerce tension | Her show is critically acclaimed but low-rated. Keeping it is a CHOICE the player must justify to themselves. |
| **Dale Bruckner** | Reliability and consistency | His procedurals are boring but profitable. He teaches the value of the FLOOR. |
| **Vanessa Cole** | Talent management (leverage, loyalty, negotiation) | Her contract negotiation is a masterclass in reading power dynamics. |

The player learns the SYSTEMS by engaging with the PEOPLE. The systems are never abstract -- they are always embodied.

---

## 8. PLAYTESTING METRICS (How We Measure Success)

The level design is not done until we TEST it. These are the metrics that tell us if the design is working.

### 8.1 Core Metrics (Moment-to-Moment)

| Metric | Target | How We Measure | What It Tests |
|---|---|---|---|
| **Time to First Card Placement** | < 30 sec from opening The Board | Eye-tracking + interaction logs | Is The Board READABLE at a glance? |
| **Card Placement Frequency** | 3-8 placements per 5-min loop | Interaction logs | Is the player ENGAGED or just watching? |
| **Ratings Reveal Duration** | 15-45 sec for a full week | Session recordings | Is the reveal DRAMATIC without being TEDIOUS? |
| **Event Response Rate** | 70%+ of events get a player response (not auto-filed) | Interaction logs | Are events MEANINGFUL or noise? |
| **Schedule Change Frequency** | 2-5 changes per season (outside premiere/midseason) | Save file analysis | Is the player ITERATING or set-and-forget? |

### 8.2 Flow Metrics (Session-to-Session)

| Metric | Target | How We Measure | What It Tests |
|---|---|---|---|
| **Session Length** | 45-90 min average | Telemetry | Is the session loop SATISFYING? |
| **Quit Point Distribution** | 60%+ quit at natural stopping points (sweeps end, season end) | Telemetry | Are stopping points CLEAR? |
| **Return Rate** | 70%+ of players who complete Season 1 return for Season 2 | Retention data | Did the first season HOOK them? |
| **Season Completion Rate** | 50%+ of players who start a season finish it | Drop-off analysis | Is the GRIND tolerable? |

### 8.3 Mastery Metrics (Campaign-Long)

| Metric | Target | How We Measure | What It Tests |
|---|---|---|---|
| **Lead-In Optimization** | 40%+ of players achieve 3+ nights of green flow chains by Season 3 | Save file analysis | Are players LEARNING flow architecture? |
| **Competitive Awareness** | 60%+ of players make at least one counterprogramming move by Season 5 | Interaction logs | Are players thinking about the LANDSCAPE, not just their schedule? |
| **Budget Sustainability** | 50%+ of players end Season 6+ with positive profit | Economic data | Have players learned to BALANCE prestige and profit? |
| **Campaign Completion** | 25%+ of players complete all 12 seasons | Completion rate | Is the 30-hour arc COMPELLING enough to finish? |

### 8.4 Emotional Metrics (Qualitative)

These cannot be measured by telemetry. These require OBSERVATION and INTERVIEWS.

**Playtest Questions (Asked Post-Session):**

1. "When you look at The Board, where do your eyes go first?" (Tests attention hierarchy)
2. "Describe a decision you made this session that you're still thinking about." (Tests emotional weight)
3. "Did any show feel REAL to you -- like you cared about it beyond the numbers?" (Tests environmental storytelling effectiveness)
4. "When you cancelled a show, how did it feel?" (Tests cancellation drama tuning)
5. "If you started a new campaign, would you play differently? How?" (Tests replayability / mastery depth)

**Success Thresholds:**

- 70%+ of playtesters should answer Q1 with "Thursday 9 PM" or "my weakest show" (correct attention priority)
- 60%+ should have a specific answer to Q2 (decisions are memorable)
- 40%+ should answer YES to Q3 with a show name (environmental storytelling is working)
- 50%+ should describe cancellation as "hard" or "necessary but sad" (weight without paralysis)
- 80%+ should have a specific strategic change in mind for Q5 (depth exists to explore)

---

## 9. LEVEL DESIGN RISK ASSESSMENT

What could break the spatial design of this game?

### RISK 1: The Board Becomes Unreadable (Critical)

**Symptom:** The player looks at the 7×3 grid and feels OVERWHELMED instead of strategic.

**Cause:** Too much information density. Every card shows 8+ stats, rival schedules are fully visible, event notifications pile up.

**Mitigation:**
- **Default to strategic overview, details on demand.** Show cards display title, genre icon, expected viewership range, and ONE primary stat (quality rating OR demo skew, player-selectable preference). Everything else is hover/click.
- **Color-code by priority.** Hot slots (Thursday) have a subtle background tint. Dead slots (Friday) are visually DE-emphasized (slightly grayed).
- **Rival schedules shown as THREAT LEVEL, not full cards.** Instead of showing AmeriNet's full Thursday lineup, show: "Thursday 9 PM: HIGH THREAT (AmeriNet flagship 12M expected)."

**Test:** Can a new player answer "What's my strongest night?" within 5 seconds? If no, UI has failed.

---

### RISK 2: The Grind Zones Feel Like Padding (High)

**Symptom:** Weeks 23-30 (Spring Grind) become a slog. Players disengage or fast-forward mindlessly.

**Cause:** Nothing changes week-to-week. The loop becomes ROUTINE instead of strategic.

**Mitigation:**
- **Inject variance into the grind.** Even "quiet" weeks should have 1-2 minor events (a showrunner calls to thank you for a renewal, a headline about a rival's struggle, a talent scouting report for next season).
- **Offer FAST-FORWARD with consequence.** If the player fast-forwards through 4 weeks, they SKIP the chance to respond to events that happened during that time. Fast-forward is a CHOICE with tradeoffs, not a "skip boring stuff" button.
- **Make the grind the REWARD for good planning.** A well-built schedule COASTS through the grind. A fragile schedule COLLAPSES here. The grind is a test of whether the player built a system or a house of cards.

**Test:** Do players fast-forward through the grind more than 50% of the time? If yes, it's padding. If they fast-forward 20-30%, it's optional relief (correct).

---

### RISK 3: Sweeps Months Lose Their Impact After Season 3 (Medium)

**Symptom:** The first November Sweeps is exciting. By Season 4, it's routine. By Season 8, the player barely notices.

**Cause:** Repetition without escalation. Sweeps are mechanically identical every time.

**Mitigation:**
- **Escalate the STAKES, not the mechanics.** Early sweeps are about "did I win or lose?" Later sweeps are about "did I protect my legacy show from getting crushed?" or "did I launch the midseason replacement that will define next year?"
- **Vary the CRISIS events during sweeps.** Season 2 sweeps might have an actor scandal. Season 5 sweeps might have a production strike threat. Season 9 sweeps might have a streaming platform poaching announcement. Same structure, different narrative pressure.
- **Track HISTORICAL performance.** The sweeps results screen should show: "This is your 6th November Sweeps. You've won 3, placed 2nd twice, placed 3rd once. This is your best performance yet." The player's history makes each sweeps MORE meaningful, not less.

**Test:** Do late-game sweeps months (Season 8+) feel like HIGH-STAKES events? If they feel routine, we've failed.

---

### RISK 4: The Era Shifts Feel Arbitrary Instead of Inevitable (High)

**Symptom:** DVR adoption or the writers' strike feels like a "rocks fall, everyone dies" moment instead of a natural evolution.

**Cause:** Insufficient telegraphing. The shift arrives without warning.

**Mitigation:**
- **Telegraph EVERY era shift 1-2 seasons in advance.** DVR headlines start appearing in Season 4 (adoption at 5%, mechanically negligible). By Season 7, it's 25% and mechanically significant. The player SEES it coming.
- **Give the player TOOLS to adapt BEFORE the shift hits hard.** The player can invest in serialized prestige dramas in Season 5-6 (when DVR is still minor) to PREPARE for Season 9-10 (when DVR becomes the dominant metric). Strategic foresight is REWARDED.
- **Frame shifts as INDUSTRY evolution, not punishment.** The game's tone should be: "The world is changing. How will you adapt?" NOT "The game is now harder for no reason."

**Test:** Do players feel the era shifts are FAIR challenges or CHEAP difficulty spikes? Survey post-Season 8 (strike). If 60%+ say "fair," we succeeded.

---

### RISK 5: The Endgame (Season 12) Lacks a Clear Climax (Medium)

**Symptom:** Season 12 feels like "just another season" instead of a FINALE.

**Cause:** No mechanical or narrative differentiation. The loop is identical to Season 11.

**Mitigation:**
- **Introduce a final threat: Streaming Poaching.** Season 12 is when Netflix/Hulu begin aggressively poaching broadcast talent with massive deals. The player faces an EXISTENTIAL question: "Can I keep my best people, or is the era ending?"
- **Slow the pacing.** Season 12 should feel REFLECTIVE. Fewer events. More space. The game is giving the player room to LOOK at what they've built.
- **End with the LEGACY SCREEN.** After the final May Sweeps, the game presents The Board one last time -- every show the player ever scheduled, visualized as a timeline. Hits glow bright. Flops fade. Cancelled shows are ghosts. The player SEES their career as a single image.

**Test:** Does Season 12 feel like a CONCLUSION or just a stopping point? Playtest the ending specifically. Does the player feel CLOSURE?

---

## 10. LEVEL DESIGN DOCUMENT SUMMARY

### Core Spatial Principles

1. **The Board is the map.** Every strategic decision is spatial -- placement, adjacency, flow.
2. **The season is the level.** 35 weeks, seven zones, escalating from tutorial to boss fight to reflection.
3. **The era is the world.** 12 seasons across 3 eras, each with shifting rules and terrain.
4. **The rivals are the encounters.** Three AI opponents with distinct strategies and behavioral tells.
5. **The player's eye is the camera.** Visual hierarchy guides attention -- hot zones bright, dead zones dim, threats highlighted.

### Pacing Summary

- **30-second loop:** Tactical. Immediate feedback. Drag, place, ripple.
- **5-minute loop:** Encounter. Lock, simulate, react. 3-7 minutes per cycle.
- **Session loop:** Chapter. 45-90 minutes, beginning/middle/end, natural stopping points.
- **Campaign loop:** Career. 12 seasons, 30+ hours, four timescales of mastery.

### Teaching Strategy

- **Visual breadcrumbs:** Color, flow lines, card states. The UI teaches without words.
- **Systemic breadcrumbs:** Consequences are lessons. The player learns by doing, not reading.
- **Narrative breadcrumbs:** Characters teach systems. Jordan teaches strategy. Arthur teaches budget. Margaux teaches cost.

### Victory Condition

There is no single "win." The player wins when they look at The Board at the end of Season 12 and feel the weight of what they built -- the shows that mattered, the shows they killed, the talent they nurtured, the era they survived. The game does not judge. The player judges themselves.

---

## GRID's Closing Note

I've designed levels for shooters, platformers, RPGs, and puzzle games. The principles are always the same: Where does the player LOOK? What's the critical path? How do we pace tension? Where are the breadcrumbs?

PREMIERE is a management sim, but The Board is as much a level as any FPS map. It has hot zones and dead zones. It has sightlines and chokepoints. It has a critical path (the Thursday night pipeline) and optional exploration (Sunday prestige slots, Friday sacrifices). Every card placement is a door. Every season is a level. Every era shift is a new world.

The player never leaves the corner office. But the view from that office -- The Board, the rivals, the overnights, the talent, the headlines -- is a landscape that changes every week for twelve years. The player's job is to read that landscape, navigate it, and leave something behind when the era ends.

What's the critical path? Thursday 9 PM. That's where every player looks first. That's the crown jewel. The rest of the schedule unfolds from there.

What's the pacing? Fast at the edges (premieres, sweeps), slow in the middle (grind, lull). Peaks and valleys. Tension and release. Never flat.

Where are the breadcrumbs? In the color of the numbers. In the flow lines between cards. In Jordan's memos. In the weight of a cancellation. In the silence after a finale. The game teaches by SHOWING, not TELLING.

Every level is a lesson. Every room teaches something. PREMIERE's room is a scheduling grid under fluorescent light, and the lesson is: what do you build when the ground won't hold?

Let's find the flow.

-- GRID
