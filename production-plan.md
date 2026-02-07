# PREMIERE — Production Plan

**Producer:** CLOCK
**Status:** Production-Ready
**Target Platform:** PC (Steam), Steam Deck
**Estimated Timeline:** 20 months to gold
**Team Size:** 6 core + 3 contract
**Budget Target:** $980K (full production)

---

## 0. CLOCK's Note

Let me be clear about what we're building and what we're not.

PREMIERE is a management sim where you drag cards onto a grid and watch numbers change. That's the loop. Everything else — the procedural show generation, the talent relationships, the 12-season career arc — exists to make that loop *matter*. If the Board doesn't feel good to use by Week 3, we have nothing. I don't care how beautiful the Emmy ceremony is or how deep the narrative bible goes. If dragging a card doesn't feel satisfying, players quit.

I've shipped six games. Four of them shipped late. Two of them were good. The two that were good shipped *early* because we cut scope before it cut us. The ones that shipped late? We kept adding features because we were afraid of shipping something "incomplete." We were wrong. A tight, focused game beats a sprawling mess every time.

Here's what we're cutting and when we're cutting it: anything that doesn't serve the 30-second loop goes in the "post-launch" pile. No exceptions.

This production plan has one goal: ship PREMIERE in 20 months with a stable core loop, 12 playable seasons, and zero game-breaking bugs. Everything else is negotiable.

What's the critical path? Board feel → Ratings engine → Pilot generation → Season loop. Lock those in sequence. Everything else can parallelize.

Let's ship this.

-- CLOCK

---

## 1. Project Overview

### 1.1 Scope Definition

**Core Deliverable:**
A single-player management sim where the player runs a cable TV network from 2000-2012. The primary interaction is drag-and-drop card placement on a 7-day x 3-slot scheduling grid. Each week simulates, ratings arrive, events fire, and the player responds. A full career spans 12 seasons (25-40 hours of gameplay).

**What's In:**
- The Board (scheduling grid with 21 slots, drag-and-drop UI, real-time adjacency feedback)
- Ratings Engine (simulates audience behavior for 4 networks, demographic targeting, competitive counterprogramming)
- Pilot Pipeline (procedural show generation, 200+ premise templates, 24 genre combinations)
- Talent Web (50+ persistent showrunners/actors with loyalty tracking, event-driven relationship system)
- The Ledger (economy simulation, budget allocation, ad revenue calculation)
- Era Progression (2000-2012 timeline with 6 major industry shifts including DVR adoption and writers' strike)
- Event System (80+ event types with player choices and consequences)
- Save/Load (full state serialization, 3 rotating autosaves, Steam Cloud integration)
- Audio suite (adaptive music, 120+ SFX, 50+ voice lines)
- Art direction (period-authentic UI, 2000s network office aesthetic)

**What's Cut from v1.0:**
- Upfront presentation mini-game (stretch goal → post-launch DLC if sales support it)
- Writers' room system (scope creep, adds 2 months, minimal impact on core loop)
- Awards campaign mini-game (nice-to-have, not need-to-have)
- Syndication afterlife system (backend-heavy, deferred)
- Network notes system (risks over-complication, cut unless playtest demands it)
- Real licensed shows (legal nightmare, use procedural generation only)
- Multiplayer/leaderboards (single-player first, async scoring post-launch if demand exists)
- Console ports (PC/Steam Deck at launch, console after we prove market fit)

**What Never Gets Built:**
- 3D graphics (this is a 2D card game, delete Unity's 3D pipeline)
- VR support (absolutely not)
- Live-service mechanics (no daily quests, no battle pass, no grinding)
- Microtransactions (one-time purchase, no IAP)

### 1.2 Success Criteria

**Minimum Viable Product (MVP):**
- Player can schedule 10+ shows across 21 timeslots
- Week simulation completes in under 200ms
- One full season (35 weeks) is playable start to finish
- Adjacency recalculation happens without frame drops during card drag
- Save/load works reliably
- Core loop (schedule → simulate → respond → adjust) feels satisfying

**Shippable Product:**
- 12 seasons (2000-2012) fully playable
- 200+ unique show premises generated procedurally without noticeable repetition
- 3 rival networks with distinct AI personalities
- 80+ events with meaningful player choices
- Budget simulation balanced (no dominant strategy)
- Audio/visual polish complete
- Zero critical bugs (crashes, save corruption, soft-locks)
- Steam integration complete (Cloud saves, achievements, workshop-ready)

**Commercial Success Targets:**
- 5,000+ wishlists before launch (validates market)
- 50,000 units sold in first year (breakeven + team salaries)
- 75%+ positive reviews on Steam (proves design works)
- 25+ hour average playtime (engagement metric)

### 1.3 Team Structure

**Core Team (Full-Time, 20 months):**

| Role | Count | Responsibilities | Key Skills |
|---|---|---|---|
| **Lead Programmer** | 1 | Core systems architecture, ratings engine, save system, performance optimization, team coordination | C#, Unity, systems design, shipping games |
| **Gameplay Programmer** | 2 | Board system, pilot generation, talent web, event system, AI scripting | C#, Unity, data structures, problem-solving |
| **UI Programmer** | 1 | UI Toolkit implementation, drag-and-drop, animations, responsive layouts | Unity UI, DOTween, UX design |
| **Tools Programmer** | 1 | Editor tools, balance exporters, testing utilities, build pipeline, CI/CD | Unity Editor scripting, automation |
| **Producer** | 1 | Milestone tracking, scope management, dependency coordination, risk mitigation, playtesting | Project management, critical path analysis |

**Contract Roles (Part-Time):**

| Role | Duration | Deliverables |
|---|---|---|
| **Audio Director/Composer** | 4 months | Adaptive music system (14 cues, ~28 min), 120+ SFX, 50+ VO lines, FMOD integration |
| **Visual Designer/Artist** | 5 months | UI art (card templates, icons, backgrounds), key art, style guide, Steam assets |
| **QA Lead** | 3 months (final phase) | Test plan execution, bug tracking, balance feedback, Steam Deck validation |

**External Support:**
- Voice actors (10-15 actors, 1 week recording session, contract)
- Legal review (contract terms, IP clearance, 1 day consult)
- Marketing consultant (Steam page optimization, trailer script, 2 weeks contract)

**Why This Size:**
Six core people is the right balance. Smaller and we lack bandwidth for parallel workstreams. Larger and communication overhead kills velocity. I've shipped with teams of 3 and teams of 15. Six is the sweet spot for a data-driven sim.

### 1.4 Platform & Tech Stack

**Primary Platform:** PC (Windows/macOS/Linux via Steam)
**Secondary Platform:** Steam Deck (fully verified, native controller support)
**Future Platforms:** Switch/PlayStation/Xbox (post-launch, only if sales justify port costs)

**Engine:** Unity 2022 LTS
**Language:** C#
**UI Framework:** Unity UI Toolkit (IMGUI for editor tools)
**Audio Middleware:** FMOD Studio
**Version Control:** Git + GitHub (or GitLab)
**CI/CD:** GitHub Actions (automated builds for Win/Mac/Linux)

**Supporting Libraries:**
- DOTween (UI animation, card tweening)
- Odin Inspector (editor tooling, data entry workflows)
- TextMeshPro (typography, card text rendering)
- Newtonsoft.Json (save/load serialization)

**External Services:**
- Steamworks SDK (Cloud saves, achievements, workshop)
- FMOD Studio (adaptive audio, stem mixing)

---

## 2. Milestones & Timeline

### Milestone Overview (20 Months to Gold)

| Phase | Duration | End Date | Deliverable | Gate Criteria |
|---|---|---|---|---|
| **Prototype** | Months 1-3 | Week 13 | Board UI + adjacency system + basic simulation | Playtester can schedule 10 shows and explain their placement logic |
| **Vertical Slice** | Months 4-6 | Week 26 | One full season playable (35 weeks) | Playtester completes Season 1 and wants to play Season 2 immediately |
| **Full Feature Set** | Months 7-12 | Week 52 | All systems online, 12 seasons playable | Playtester completes 3+ seasons without hitting missing features |
| **Content & Balance** | Months 13-16 | Week 69 | 200+ show templates, 80+ events, balance tuning | Full 12-season career playable with high replayability |
| **Polish & Ship Prep** | Months 17-20 | Week 87 (Gold) | Audio/visual polish, Steam integration, QA certification | Zero critical bugs, 60 FPS on recommended spec, Steam Deck verified |

**Total Timeline:** 20 months (87 weeks) from kickoff to gold master.

---

## 3. Detailed Phase Breakdown

### Phase 1: Prototype (Months 1-3)

**Goal:** Prove the core loop feels good. If dragging cards doesn't satisfy, we have nothing.

**Deliverables:**

**Month 1 (Weeks 1-4):**
- **Week 1-2:** Project setup, Unity project init, Git repo, dev environment, team onboarding
  - Lead Programmer: Core architecture skeleton (GameController, SaveManager, EventBus)
  - UI Programmer: Board grid layout (7x3 slot grid, placeholder cards)
  - Tools Programmer: Editor tooling setup (Odin Inspector integration, ScriptableObject templates)
- **Week 3-4:** First playable Board
  - UI Programmer: Drag-and-drop system (card pickup, drag cursor follow, drop zone detection)
  - Gameplay Programmer 1: ShowCard data model (ScriptableObject with stats: title, genre, quality, audience floor/ceiling, CPE)
  - Gameplay Programmer 2: Card instantiation system (spawn 10 test shows on bench, drag to grid)
  - **Playtest:** Can you drag a card? Does it snap to grid? (Pass/Fail gate)

**Month 2 (Weeks 5-8):**
- **Week 5-6:** Adjacency calculation system
  - Gameplay Programmer 1: Lead-in bonus formula (previous show viewership x demo overlap x decay factor)
  - Gameplay Programmer 2: Real-time stat update on card placement (viewership ranges recalculate instantly)
  - UI Programmer: Visual feedback (lead-in flow arrows, stat number ticker animations)
- **Week 7-8:** Basic ratings simulation
  - Lead Programmer: Ratings engine foundation (calculate viewership for one show based on quality, star power, marketing)
  - Gameplay Programmer 1: Seasonal modifiers (sweeps multiplier, holiday drop)
  - Gameplay Programmer 2: Ratings reveal screen (overnight numbers display sequentially)
  - **Playtest:** Place cards, lock schedule, see ratings. Do numbers make sense? (Pass/Fail gate)

**Month 3 (Weeks 9-13):**
- **Week 9-10:** Week simulation loop
  - Lead Programmer: Week simulation controller (lock schedule → simulate → reveal → player response phase)
  - Gameplay Programmer 1: Event inbox system (placeholder events: "Show renewed" / "Show on bubble")
  - Tools Programmer: Debug tools (manual event triggers, week skip buttons)
- **Week 11-12:** Prototype polish
  - UI Programmer: UI animation pass (card snap easing, number count-up, transition smoothness)
  - Audio Designer (contract begins): Temp SFX (card snap, ticker sound, confirm beep)
  - All: Bug fixing, performance profiling (target: 60 FPS during card drag)
- **Week 13:** Milestone 1 Playtest
  - **Gate Criteria:**
    - Tester can schedule 10 shows across 7 nights
    - Adjacency recalculation happens without frame drops
    - Tester can explain why they placed Show A in Slot B ("because of the lead-in from Show C")
    - If Pass → proceed to Vertical Slice
    - If Fail → iterate Week 14, re-test Week 15

**Key Risks for Prototype Phase:**
- UI performance during drag (mitigation: throttle recalculations to 100ms intervals, profile early)
- Adjacency math opacity (mitigation: detailed tooltips, color-coded feedback)

**Prototype Budget:** ~$180K (3 months x 6 people x avg $10K/month loaded cost)

---

### Phase 2: Vertical Slice (Months 4-6)

**Goal:** One full season (September to May, 35 weeks) is playable start to finish.

**Deliverables:**

**Month 4 (Weeks 14-17):**
- **Week 14-15:** Pilot pipeline (procedural show generation)
  - Gameplay Programmer 2: GenreTemplate ScriptableObject (premise templates, stat ranges, demo defaults)
  - Gameplay Programmer 1: Show generator (combines protagonist + setting + hook, rolls quality ceiling, attaches talent)
  - Tools Programmer: Show template editor (custom Unity window for creating genre templates)
  - Target: Generate 25 pilots per season with visible variety
- **Week 16-17:** Season calendar system
  - Lead Programmer: Season state machine (Fall Premiere → Sweeps → Midseason → Finales)
  - Gameplay Programmer 1: Seasonal modifiers (November Sweeps 1.2x, December holidays 0.7x)
  - Gameplay Programmer 2: Midseason replacement system (cancel show, replace with new pilot)

**Month 5 (Weeks 18-21):**
- **Week 18-19:** Talent system foundation
  - Gameplay Programmer 2: ShowrunnerData ScriptableObject (talent level, ego, loyalty, specialty)
  - Gameplay Programmer 1: Loyalty tracking (player actions modify loyalty: greenlight +10, cancel -20, etc.)
  - Lead Programmer: Talent event roller (scandals, contract disputes, poaching attempts)
- **Week 20-21:** Economy system
  - Gameplay Programmer 1: Revenue calculator (viewership x demo weight x CPM x ad slots)
  - Gameplay Programmer 2: Budget allocation UI (sliders for Development/Marketing/Talent/Operations)
  - Lead Programmer: Profit/loss tracking, end-of-season financial report

**Month 6 (Weeks 22-26):**
- **Week 22-23:** Save/load system
  - Lead Programmer: SaveData structure (serialize all systems to JSON)
  - Tools Programmer: Save file versioning, migration system, autosave (end of week, end of season)
  - Lead Programmer: Load game, validate state, handle corruption gracefully
- **Week 24-25:** Vertical slice polish
  - UI Programmer: Season transition screens (calendar page flip, Emmy ceremony placeholder)
  - Audio Designer: Music cues (Board Work theme, Ratings Reveal music, Crisis Motif)
  - All: Bug fixing, balance tuning (does the economy work? Can player go bankrupt?)
- **Week 26:** Milestone 2 Playtest
  - **Gate Criteria:**
    - Tester completes one full season (2-4 hours)
    - Tester can describe their network's identity ("I'm going prestige-first" or "I'm chasing ratings")
    - Tester wants to play Season 2 immediately (engagement test)
    - Save/load works without corruption
    - If Pass → proceed to Full Feature Set
    - If Fail → extend VS phase 2 weeks, identify missing "fun factor"

**Key Risks for Vertical Slice:**
- Procedural generation feels repetitive (mitigation: 200+ premise templates, "weird pilot" roll)
- Save corruption (mitigation: JSON format, 3 autosaves, extensive testing)

**Vertical Slice Budget:** ~$180K (3 months x 6 people x $10K/month)

---

### Phase 3: Full Feature Set (Months 7-12)

**Goal:** All systems online. 12-season career is mechanically complete.

**Month 7-8 (Weeks 27-34):**
- **Gameplay Programmer 1:** Competitor AI (AmeriNet, Crowne Broadcasting, Pacific Television)
  - Three AI personalities with distinct scheduling logic
  - Counterprogramming, talent poaching, copycat shows
  - AI difficulty scaling (Seasons 1-2 easy, Seasons 9-12 adaptive)
- **Gameplay Programmer 2:** Full talent system (actors, contracts, volatility, scandals)
  - Actor contract expiration, salary holdouts, recasting system
  - Scandal events (DUI, feuds, rehab), tabloid impact on ratings
- **Lead Programmer:** Event system architecture
  - EventManager, priority queue, event factory
  - 30 event types implemented (talent revolts, fan campaigns, advertiser boycotts)
- **UI Programmer:** Competitive threat display, rival network schedules UI

**Month 9-10 (Weeks 35-43):**
- **Gameplay Programmer 1:** Era progression system (2000-2012 timeline)
  - 2003 Reality Explosion, 2005 DVR Early Adoption, 2007 Writers' Strike, 2009 DVR Mainstreaming, 2011 Streaming Cliff
  - Each era shift modifies game rules (DVR metrics, genre saturation, talent flight)
- **Gameplay Programmer 2:** Expand event system (50 more event types)
  - Industry events (strike, DVR milestones), competitive events (rival poaching), audience events (cult following)
- **Lead Programmer:** DVR metrics system (Live vs Live+3 vs Live+7, advertiser CPM adjustments)
- **UI Programmer:** Era transition screens, industry report memos, Variety headline ticker

**Month 11-12 (Weeks 44-52):**
- **All Programmers:** System integration, bug fixing, performance optimization
  - Full 12-season career end-to-end testing
  - Profile week simulation (target: sub-200ms for 84 shows x 4 networks)
  - Save/load stress testing (Season 10 saves with 150+ shows in history)
- **Audio Designer:** Remaining music cues (Emmy Ceremony, Annual Review, Career Legacy theme)
- **Visual Designer (contract begins):** UI art pass (card backgrounds, genre icons, slot highlights)
- **Week 52:** Milestone 3 Playtest
  - **Gate Criteria:**
    - Tester completes 3+ seasons (6-12 hours) without hitting missing features
    - Competitor AI makes believable strategic decisions (not random, not perfect, but credible)
    - DVR era shift (Seasons 8-10) feels challenging but fair
    - Zero game-breaking bugs (crashes, save corruption, soft-locks)
    - If Pass → proceed to Content & Balance
    - If Fail → extend 2 weeks, fix critical gaps

**Key Risks for Full Feature Set:**
- Competitor AI feels dumb (mitigation: distinct personalities, believable mistakes, playtesting)
- DVR shift feels punishing (mitigation: gradual introduction, new strategies unlocked, advisor tooltips)

**Full Feature Set Budget:** ~$360K (6 months x 6 people x $10K/month)

---

### Phase 4: Content & Balance (Months 13-16)

**Goal:** Content-fill, balance tuning, replayability validation.

**Month 13-14 (Weeks 53-60):**
- **Gameplay Programmer 1 + 2:** Content creation
  - 200+ show premise templates (24 genre/subgenre combos x 8-10 templates each)
  - 100+ talent personalities (50 showrunners, 50 actors, distinct traits and arcs)
  - Complete event library (80+ events with choice trees)
- **Tools Programmer:** Balance exporter tool
  - Export all show stats, economy formulas, event outcomes to CSV
  - Designer can tune balance in Google Sheets, re-import JSON
- **Lead Programmer:** Balance pass on economy
  - CPM rates, CPE costs, profit margins, budget scaling across 12 seasons
  - Goal: No dominant strategy, prestige vs popularity equally viable

**Month 15-16 (Weeks 61-69):**
- **Audio Designer:** Full audio suite
  - 120+ SFX (card interactions, UI sounds, notification alerts)
  - 50+ VO lines (showrunner phone calls, actor negotiations, The Suit's reviews)
  - FMOD adaptive music system (5 stem layers for Board Work, intensity scaling)
- **Visual Designer:** Art completion
  - All UI elements final (card templates, icons, buttons, backgrounds)
  - Key art for Steam (capsule, header, library hero)
  - Period-authentic aesthetic (2000s office environments, Variety headlines)
- **All:** Playtesting marathon
  - 10+ external testers complete full 12-season careers (25-40 hours each)
  - Identify repetition fatigue, balance exploits, pacing issues
- **Week 69:** Milestone 4 Playtest
  - **Gate Criteria:**
    - Tester completes full 12-season career and rates replayability high ("I want to try a different strategy")
    - Show generation doesn't feel repetitive after 300+ pilots seen
    - Economy is balanced (no single genre or strategy dominates)
    - Audio/visual polish is at "shippable" quality
    - If Pass → proceed to Polish & Ship Prep
    - If Fail → extend 2 weeks, address critical feedback

**Key Risks for Content & Balance:**
- Content fatigue (mitigation: 200+ templates, weird pilot roll, vary event frequency)
- Balance holes (mitigation: export to spreadsheet, aggregate playtest data, iterate)

**Content & Balance Budget:** ~$240K (4 months x 6 people x $10K/month)

---

### Phase 5: Polish & Ship Prep (Months 17-20)

**Goal:** Ship v1.0 to Steam. Zero critical bugs. Marketing launch.

**Month 17 (Weeks 70-73):**
- **QA Lead (contract begins):** Test plan execution
  - 100+ hours of structured testing (full playthroughs, edge case hunting, save corruption stress testing)
  - Bug database setup (GitHub Issues or Jira), priority triaging (Critical/High/Medium/Low)
- **All Programmers:** Bug fixing sprint
  - Target: Zero critical bugs (crashes, save corruption, progression blockers)
  - High-priority bugs: Fix before Week 75
  - Medium/low bugs: Triage to post-launch patch or "won't fix"
- **Tools Programmer:** Steam integration
  - Steamworks SDK (Cloud saves, achievements, rich presence)
  - Steam Workshop prep (expose show templates, genre configs as moddable files)

**Month 18 (Weeks 74-77):**
- **UI Programmer:** Final polish pass
  - Animation timing refinement (card snaps, stat tickers, screen transitions)
  - Responsive layout validation (1080p, 1440p, 4K, Steam Deck 800p)
  - Accessibility features (colorblind mode, text scaling, high contrast mode)
- **Audio Designer:** Audio mix & mastering
  - Final mix balance (music ducks for SFX, SFX prioritization)
  - Master limiter for consistent loudness (-18 LUFS integrated)
  - Steam Deck audio testing (built-in speakers + headphones)
- **Visual Designer:** Key art & trailer assets
  - Steam capsule (616x353), header (460x215), library hero (3840x1240)
  - Trailer storyboard (30-60 sec sizzle reel of Board gameplay, ratings drama, Emmy wins)

**Month 19 (Weeks 78-82):**
- **Lead Programmer + Tools Programmer:** Performance optimization
  - Profile on minimum spec hardware (Intel i5-6500, integrated graphics)
  - Target: 60 FPS on recommended spec, 30 FPS on minimum spec
  - Steam Deck validation (40 FPS stable, 4+ hour battery life)
- **All:** Final QA certification
  - QA Lead runs full regression suite (all features, all platforms)
  - Zero critical bugs remaining
  - Save/load tested with 50+ different save states (early/mid/late game, all eras)
- **Producer:** Pre-launch prep
  - Steam store page live (with Coming Soon tag)
  - Press outreach (send keys to YouTubers, streamers, press)
  - Community setup (Discord server, subreddit monitoring)

**Month 20 (Weeks 83-87):**
- **Week 83-84:** Gold master build
  - Final build exported (Windows/macOS/Linux)
  - Steamworks depot upload, release branch locked
  - Day-one patch readiness (hotfix pipeline tested)
- **Week 85:** Pre-launch marketing
  - Announce release date (2 weeks before launch)
  - Trailer released (YouTube, Twitter, Steam store page)
  - Demo available (if scope allows: first 2 seasons playable)
- **Week 86:** Launch week
  - Monitor launch metrics (wishlists converting, reviews, crash reports)
  - Hotfix team on standby (Lead Programmer + Tools Programmer ready for emergency patches)
- **Week 87:** Post-launch Week 1
  - Address critical launch bugs within 48 hours
  - Communicate with community (acknowledge issues, commit to fixes)
  - Begin post-launch roadmap (Patch 1.1 planning)

**Gate Criteria for Gold:**
- Zero critical bugs in QA certification
- 60 FPS on recommended spec, 30 FPS stable on minimum spec
- Steam Cloud saves work across devices
- Steam Deck verified badge earned
- Store page has 5,000+ wishlists (marketing validation)
- Trailer has 50K+ views (audience interest validation)

**Polish & Ship Prep Budget:** ~$240K (4 months x 6 people x $10K/month)

---

## 4. Dependency Map & Critical Path

### 4.1 Critical Path

The critical path is the sequence of tasks that MUST complete on time or the project slips. Everything else can parallelize or delay without blocking gold.

**Critical Path (Bold = Blocking):**

```
Week 1-2: Project Setup
    ↓
**Week 3-4: Board UI (drag-and-drop works)**
    ↓
**Week 5-8: Adjacency calculation + stat updates**
    ↓
**Week 9-13: Week simulation loop**
    ↓ [Milestone 1 Gate]
    ↓
**Week 14-17: Pilot generation (procedural shows)**
    ↓
**Week 18-21: Season calendar + talent system foundation**
    ↓
**Week 22-26: Save/load system**
    ↓ [Milestone 2 Gate]
    ↓
**Week 27-34: Competitor AI + full talent system**
    ↓
**Week 35-43: Era progression + DVR metrics**
    ↓
**Week 44-52: System integration + full 12-season testing**
    ↓ [Milestone 3 Gate]
    ↓
**Week 53-69: Content creation (200+ templates, 80+ events)**
    ↓ [Milestone 4 Gate]
    ↓
**Week 70-77: QA + bug fixing sprint**
    ↓
**Week 78-82: Performance optimization + final QA**
    ↓
**Week 83-87: Gold master + launch**
```

**Estimated Critical Path Duration:** 87 weeks (20 months)

**Slack Time:** 2 weeks built into Milestone 3 and 4 for iteration if gates fail. If both pass clean, we ship 2 weeks early.

### 4.2 Parallel Workstreams (Non-Blocking)

These can run in parallel without blocking critical path:

**Audio (Months 3-18, contract):**
- Temp SFX (Month 3, supports Prototype playtest)
- Music composition (Months 6-12, supports Vertical Slice + Full Feature)
- Final audio suite (Months 15-18, polish phase)

**Visual Design (Months 12-18, contract):**
- UI art pass (Months 12-14, supports Full Feature polish)
- Final art assets (Months 15-17, polish phase)
- Key art & trailer (Month 18, pre-launch)

**Tools & Editor (Ongoing):**
- Tools Programmer builds utilities throughout (doesn't block gameplay)
- Balance exporter (Month 13-14, supports tuning phase)
- Steam integration (Month 17, pre-launch)

### 4.3 Dependency Matrix

| System | Depends On | Blocks |
|---|---|---|
| **Board UI** | None (first system) | Everything (core loop) |
| **Adjacency Calc** | Board UI, ShowCard data | Ratings simulation |
| **Ratings Engine** | Adjacency calc, ShowCard data | Week simulation, AI |
| **Pilot Generation** | ShowCard data model | Season loop, talent attachment |
| **Talent System** | Pilot generation, Event system | Talent events, poaching |
| **Competitor AI** | Ratings engine, Pilot generation | None (can ship without AI if desperate, but shouldn't) |
| **Save/Load** | All core systems | Nothing (but required for VS gate) |
| **Era Progression** | Ratings engine, Talent system | Late-game balance |
| **Audio** | None (parallel) | Nothing (can ship silent, but shouldn't) |
| **Art** | Board UI layout | Nothing (can ship with placeholder art if desperate) |

**Key Insight:** Board UI is the foundation. Everything depends on it feeling good. If Week 3-4 slips, the entire project slips. Lock the Board interaction feel before proceeding.

---

## 5. Risk Register

### 5.1 Critical Risks (Red)

**RISK 1: Board UI Performance During Drag**

**Likelihood:** Medium (50%)
**Impact:** Critical (blocks core loop)
**Trigger:** Frame drops during card drag on minimum spec hardware

**Mitigation:**
- Profile in Week 4 (immediately after first drag implementation)
- Throttle adjacency recalculations to 100ms intervals during drag (not every frame)
- Use dirty flags to update only affected cards
- Cache competitor schedules per frame (don't query 21 times)
- If still slow: disable live updates during drag, only recalculate on drop

**Contingency:** If mitigation fails, simplify adjacency math (remove some variables) or reduce grid size to 5 nights x 3 slots (15 cards instead of 21). This is last resort.

**Owner:** UI Programmer (primary), Lead Programmer (oversight)

---

**RISK 2: Procedural Show Generation Feels Repetitive**

**Likelihood:** High (70%)
**Impact:** High (kills 20+ hour engagement)
**Trigger:** Playtesters report "all pilots look the same" by Season 5

**Mitigation:**
- Build 200+ premise templates (not 50)
- Implement "weird pilot" roll (10% of pool are genre mashups)
- Track generated premises, bias against recent duplicates
- Playtest pilot generation in isolation: generate 500 pilots, have 10 testers rate "samey-ness"
- Target: No more than 15% "felt repetitive" rate

**Contingency:** If templates aren't enough, add 50 hand-written "signature pilots" that appear rarely as high-quality standouts. Increases content work by 1 week but guarantees variety.

**Owner:** Gameplay Programmer 2 (primary), Producer (playtesting coordination)

---

**RISK 3: Save File Corruption**

**Likelihood:** Medium (40%)
**Impact:** Critical (player loses 20+ hours of progress)
**Trigger:** Complex game state (200+ entities, 420 weeks of data) leads to edge case serialization failures

**Mitigation:**
- Use JSON (human-readable, debuggable, less prone to binary corruption)
- Implement save file versioning and migration system
- Keep 3 rotating autosaves (Autosave_1, Autosave_2, Autosave_3)
- Write unit tests for serialization/deserialization of every major system
- Stress test: Load/save 100 times in a row without corruption

**Contingency:**
- Build "Repair Save File" utility that validates structure and fills missing data with defaults
- Steam Cloud saves provide remote backup if local saves corrupt

**Owner:** Lead Programmer (primary), Tools Programmer (repair utility)

---

### 5.2 High Risks (Orange)

**RISK 4: Ratings Engine Balance Is Opaque**

**Likelihood:** High (60%)
**Impact:** Medium (strategic depth collapses if players can't read the system)
**Trigger:** Playtesters can't explain why Show A got 8M viewers and Show B got 4M

**Mitigation:**
- Detailed tooltips on hover: "Organic: 5.2M, Lead-In: +2.1M, Competition: -1.4M, Final: 5.9M"
- "Ratings Explainer" tooltips for every stat
- Build testing tool (Ratings Simulator) to validate outcomes match designer intent
- Playtest with spreadsheet players (min-maxers) and ask: "Can you predict outcomes?"

**Contingency:** Add optional "Advisor Mode" — an NPC who explains ratings results in plain language after each week. Toggleable in settings. Adds 2 weeks of writing/implementation but solves opacity.

**Owner:** Lead Programmer (formula clarity), UI Programmer (tooltip implementation)

---

**RISK 5: DVR Era Shift Feels Punishing**

**Likelihood:** Medium (50%)
**Impact:** Medium (late-game engagement drops if players feel helpless)
**Trigger:** Seasons 9-12 feel like "inevitable decline" with no player agency

**Mitigation:**
- Introduce DVR metrics gradually (show as secondary stats in Season 6, primary in Season 9)
- Unlock new strategies: serialized dramas get DVR bonuses, advertisers accept Live+7
- Provide in-game "industry report" memos explaining the shift and suggesting adaptations
- Playtest Seasons 8-10 specifically with players who haven't seen early game

**Contingency:** Offer "Short Career" mode (2000-2008, 8 seasons) that ends before DVR dominates. Players who want full 12-season experience opt in knowing the challenge.

**Owner:** Gameplay Programmer 1 (DVR mechanics), Producer (playtesting)

---

**RISK 6: Competitor AI Feels Dumb**

**Likelihood:** Medium (50%)
**Impact:** Medium (competition feels hollow if AI is nonsensical)
**Trigger:** Rival networks make obviously bad decisions (empty slots, terrible matchups)

**Mitigation:**
- Give each rival a clear strategic personality (populist, prestige, disruptor)
- AI should make "believable mistakes" not "random mistakes" (e.g., over-investing in fading genre)
- Playtest: show rival schedules without context, ask "can you describe their strategy?"
- AI difficulty scaling (early seasons easy, late seasons adaptive)

**Contingency:** Simplify AI to "clone player's successes + random noise." Boring but functional. Better than nonsensical.

**Owner:** Gameplay Programmer 1 (AI logic), Lead Programmer (oversight)

---

### 5.3 Medium Risks (Yellow)

**RISK 7: Event Fatigue**

**Likelihood:** Medium (40%)
**Impact:** Low (annoying but not game-breaking)
**Trigger:** Player bombarded with talent events every week, inbox becomes tedious

**Mitigation:**
- Cap events at 3-5 per week max
- Prioritize events: urgent first, deferrable second
- Provide "Auto-Resolve" option for minor events (game picks "safe" choice)

**Contingency:** Add event frequency slider in settings (Low/Medium/High).

**Owner:** Gameplay Programmer 2 (event system)

---

**RISK 8: Steam Deck Performance**

**Likelihood:** Low (20%)
**Impact:** Medium (delays Steam Deck verified badge)
**Trigger:** UI-heavy game struggles on Deck's limited hardware

**Mitigation:**
- This is a 2D card game, Deck should handle it fine
- Profile early on Deck hardware (or SteamOS VM)
- Reduce texture resolution on Deck if needed (2K → 1K sprites)

**Contingency:** Cap at 30 FPS on Deck (still playable for turn-based sim).

**Owner:** Lead Programmer (performance), Tools Programmer (platform builds)

---

### 5.4 Low Risks (Green)

**RISK 9: Scope Creep**

**Likelihood:** High (80%) — this is always a risk
**Impact:** High (slips timeline, burns budget)
**Trigger:** "Wouldn't it be cool if..." feature requests mid-production

**Mitigation:**
- This production plan is the contract. Anything not on this list goes in "post-launch" pile.
- Weekly check-ins: Producer asks "are we building what we committed to?"
- Stretch goals clearly marked (Upfront mini-game, Writers' room) — NOT v1.0 scope

**Contingency:** Producer has veto power on all new features during production. No exceptions.

**Owner:** Producer (CLOCK)

---

## 6. Sprint Plan (Sample: Prototype Phase)

### Sprint Structure

**Sprint Duration:** 2 weeks
**Team:** 6 people (Lead, Gameplay x2, UI, Tools, Producer)
**Ceremonies:**
- Sprint Planning (Monday Week 1, 2 hours)
- Daily Standups (async Slack check-ins: "What I did, what I'm doing, blockers")
- Sprint Review (Friday Week 2, 1 hour: demo progress to team)
- Retrospective (Friday Week 2, 30 min: what went well, what didn't, action items)

### Sprint 1: Weeks 1-2 (Project Setup)

| Task | Owner | Estimate | Dependency | Priority |
|---|---|---|---|---|
| Unity project init, Git repo setup | Lead Programmer | 1 day | None | Critical |
| Core architecture skeleton (GameController, EventBus) | Lead Programmer | 3 days | Project init | Critical |
| Board grid layout (7x3 slots, placeholder cards) | UI Programmer | 4 days | Project init | Critical |
| Odin Inspector integration, ScriptableObject templates | Tools Programmer | 3 days | Project init | High |
| ShowCard data model (ScriptableObject) | Gameplay Programmer 1 | 3 days | Project init | Critical |
| Dev environment setup (all team members) | All | 1 day | Project init | Critical |
| Sprint planning for Sprint 2 | Producer | 1 day | None | High |

**Sprint Goal:** Team can open Unity project, see a 7x3 grid, and create ShowCard ScriptableObjects.

---

### Sprint 2: Weeks 3-4 (First Playable Board)

| Task | Owner | Estimate | Dependency | Priority |
|---|---|---|---|---|
| Drag-and-drop system (card pickup, drag follow, drop detect) | UI Programmer | 5 days | Board grid | Critical |
| Card instantiation (spawn 10 test shows on bench) | Gameplay Programmer 2 | 3 days | ShowCard data model | Critical |
| Snap-to-grid logic, valid/invalid drop zones | UI Programmer | 3 days | Drag-and-drop | Critical |
| Card visual states (default, hover, drag, placed) | UI Programmer | 2 days | Drag-and-drop | High |
| Placeholder card art (genre icons, stat layout) | Tools Programmer | 2 days | None | Medium |
| Playtest preparation (build setup, test notes template) | Producer | 1 day | None | High |

**Sprint Goal:** Player can drag a card from bench to grid, and it snaps into place.

**Playtest (End of Sprint 2):** Can you drag a card? Does it snap? Pass/Fail gate.

---

### Sprint 3: Weeks 5-6 (Adjacency Calculation)

| Task | Owner | Estimate | Dependency | Priority |
|---|---|---|---|---|
| Lead-in bonus formula implementation | Gameplay Programmer 1 | 4 days | Card placement | Critical |
| Real-time stat update (viewership recalculates on place) | Gameplay Programmer 2 | 4 days | Lead-in formula | Critical |
| Demo overlap calculation (DemoProfile.Overlap) | Gameplay Programmer 1 | 2 days | ShowCard data model | Critical |
| Visual feedback (lead-in arrows, stat ticker animation) | UI Programmer | 4 days | Stat updates | High |
| Performance profiling (frame time during card drag) | Lead Programmer | 2 days | Stat updates | Critical |
| Debug tools (manual stat display, inspector values) | Tools Programmer | 2 days | None | Medium |

**Sprint Goal:** Place a card, adjacent slot's stats update instantly with visible lead-in bonus.

---

### Sprint 4: Weeks 7-8 (Basic Ratings Simulation)

| Task | Owner | Estimate | Dependency | Priority |
|---|---|---|---|---|
| Ratings engine foundation (organic audience calc) | Lead Programmer | 5 days | ShowCard data | Critical |
| Seasonal modifiers (sweeps 1.2x, holidays 0.7x) | Gameplay Programmer 1 | 2 days | Ratings engine | High |
| Ratings reveal screen (overnight numbers display) | Gameplay Programmer 2 | 4 days | Ratings engine | Critical |
| Sequential rating reveal animation (staggered ticker) | UI Programmer | 3 days | Reveal screen | High |
| Test scenarios (10 shows, known inputs, validate outputs) | Lead Programmer | 2 days | Ratings engine | Critical |

**Sprint Goal:** Lock schedule, simulate week, see ratings for all 10 shows.

**Playtest (End of Sprint 4):** Do ratings numbers make sense? Can tester explain why Show A beat Show B?

---

### Sprint 5-6: Weeks 9-13 (Week Simulation Loop + Prototype Polish)

*(Similar sprint structure continues... condensed here for brevity)*

**Key Sprints:**
- Sprint 5 (Weeks 9-10): Week simulation controller, event inbox
- Sprint 6 (Weeks 11-12): Prototype polish (animations, temp SFX, bug fixing)
- Sprint 7 (Week 13): Milestone 1 Playtest + iteration

---

## 7. Resource Allocation & Budget

### 7.1 Team Cost Breakdown

**Core Team (Full-Time, 20 months):**

| Role | Count | Monthly Rate | Total Cost (20 months) |
|---|---|---|---|
| Lead Programmer | 1 | $12,000/month | $240,000 |
| Gameplay Programmer | 2 | $10,000/month | $400,000 |
| UI Programmer | 1 | $10,000/month | $200,000 |
| Tools Programmer | 1 | $9,000/month | $180,000 |
| Producer | 1 | $11,000/month | $220,000 |
| **Subtotal** | **6** | | **$1,240,000** |

**Contract Roles:**

| Role | Duration | Rate | Total Cost |
|---|---|---|---|
| Audio Director/Composer | 4 months | $8,000/month | $32,000 |
| Visual Designer/Artist | 5 months | $7,000/month | $35,000 |
| QA Lead | 3 months | $6,000/month | $18,000 |
| Voice Actors | 1 week | $10,000 (bulk) | $10,000 |
| **Subtotal** | | | **$95,000** |

**Software & Services:**

| Item | Cost |
|---|---|
| Unity Pro licenses (6 seats x 20 months) | $10,800 |
| FMOD Studio license (indie tier) | $500 |
| Odin Inspector (6 seats) | $330 |
| GitHub (team plan, 20 months) | $800 |
| Steamworks (one-time partner fee) | $100 |
| Sound library licenses (ambiances, instruments) | $3,000 |
| Cloud storage (backup, build artifacts) | $1,000 |
| **Subtotal** | **$16,530** |

**Overhead & Contingency:**

| Item | Cost |
|---|---|
| Office/coworking space (optional, remote team) | $0 |
| Hardware (monitors, peripherals, upgrades) | $5,000 |
| Legal (contract review, IP clearance) | $3,000 |
| Marketing (trailer production, press outreach) | $8,000 |
| Contingency (10% buffer for overruns) | $135,000 |
| **Subtotal** | **$151,000** |

---

### 7.2 Total Budget

**Total Project Cost:** $1,240,000 (core) + $95,000 (contract) + $16,530 (software) + $151,000 (overhead/contingency)
**= $1,502,530**

**Rounded Budget:** $1.5M

**Budget Allocation by Phase:**

| Phase | Duration | Cost |
|---|---|---|
| Prototype | 3 months | $270,000 |
| Vertical Slice | 3 months | $270,000 |
| Full Feature Set | 6 months | $540,000 |
| Content & Balance | 4 months | $300,000 |
| Polish & Ship Prep | 4 months | $300,000 |
| **Total** | **20 months** | **$1,680,000** |

**Funding Strategy:**

- Self-funded ($500K from founders/savings)
- Publisher advance ($600K milestone-based, recoupable)
- Angel investment ($400K equity round, 15% dilution)
- Grant/subsidy (regional game dev grant, $100K non-dilutive if available)

**Breakeven Analysis:**

- Total budget: $1.5M
- Steam revenue split: 70% (after 30% Valve cut)
- Price: $19.99
- Net per unit: $14 (after Valve cut + payment processing)
- Publisher recoup: $600K (43,000 units to recoup)
- Full breakeven: $1.5M / $14 = **107,000 units**

**Target:** 50,000 units Year 1 (covers team salaries + operating costs), 100,000+ units lifetime (full recoup + profit).

---

## 8. Scope Management Rules

### What's In vs. What's Out (The Contract)

**In Scope (v1.0 Committed Features):**
- The Board (7 days x 3 slots = 21 slots, drag-and-drop, adjacency system)
- Ratings Engine (4 networks, competitive simulation, demographic targeting)
- Pilot Pipeline (procedural generation, 200+ templates, 24 genres)
- Talent Web (50+ showrunners/actors, loyalty tracking, 80+ events)
- The Ledger (revenue calc, budget allocation, profit/loss)
- 12-season career (2000-2012, era progression, DVR shift)
- Save/Load (JSON, 3 autosaves, Steam Cloud)
- Audio (adaptive music, 120+ SFX, 50+ VO lines)
- Art (period UI, card templates, key art)

**Stretch Goals (Post-Launch DLC or Free Updates):**
- Upfront Presentation mini-game
- Writers' Room system (influence show content)
- Awards Campaign mini-game (Emmy lobbying)
- Syndication afterlife system
- Network Notes system (write actual notes on scripts)
- Pre-2000 eras (1980s-1990s expansion)
- Async leaderboards (highest-rated network per season)

**Cut Forever (Not Happening):**
- 3D graphics
- VR support
- Live-service mechanics (daily quests, battle passes)
- Microtransactions
- Real licensed shows (legal nightmare)
- Multiplayer head-to-head (design doesn't support it)

### Change Request Process

**If someone proposes a new feature mid-production:**

1. **Producer reviews:** Does it serve the core loop? (schedule → simulate → respond → adjust)
2. **Estimate impact:** How many dev-weeks does it cost? What does it block?
3. **Trade-off analysis:** What existing feature gets cut or delayed to fit this in?
4. **Team vote:** If 4+ of 6 core team members say "this is critical," we discuss. Otherwise, auto-reject.
5. **Final call:** Producer (CLOCK) has veto power. The answer is usually "no, post-launch."

**Example:**

*"Wouldn't it be cool if players could watch simulated clips of their shows?"*

- Does it serve the core loop? No. The game is about managing schedules, not watching content.
- Dev cost? 3-4 months (video generation, UI integration, performance).
- Trade-off? Cuts Content & Balance phase entirely.
- Decision: **Rejected. Post-launch DLC possibility if sales justify it.**

### Cut List (If We're Behind Schedule)

**Priority tiers for cuts if timeline slips:**

**Tier 1 (Cut First):**
- Colorblind mode (nice-to-have, affects 5% of players, can patch post-launch)
- Text scaling option (accessibility, but workable at default size)
- Steam Workshop integration (moddability, post-launch feature)

**Tier 2 (Cut If Desperate):**
- 50 late-game events (reduce from 80 to 30, still functional)
- Voice acting (replace with text-only events, saves $10K and 2 weeks)
- Emmy ceremony cutscene (replace with static screen, saves 1 week)

**Tier 3 (Cut Only If Catastrophic):**
- Seasons 11-12 (ship with 10-season career, add final 2 seasons in patch)
- One rival network (3 networks becomes 2, still competitive)

**Never Cut:**
- The Board (core interaction)
- Ratings Engine (simulation is the game)
- Save/Load (player expects this)
- Pilot generation (content source)

---

## 9. Communication Plan

### 9.1 Internal Communication

**Daily:**
- Async Slack check-ins (each person posts: what I did, what I'm doing, blockers)
- No required meetings (meetings are expensive)

**Weekly:**
- Monday: Sprint planning (async or 1-hour call if needed)
- Friday: Sprint review (1 hour: demo progress, blockers, next sprint prep)
- Friday: Retrospective (30 min: what went well, what didn't, action items)

**Milestone Gates:**
- Full team playtest (half-day session, everyone plays the build)
- Post-playtest debrief (2 hours: what worked, what didn't, pass/fail decision)

**Tools:**
- Slack (daily comms, file sharing)
- GitHub (code, issues, pull requests)
- Google Sheets (task tracking, balance data, playtesting feedback)
- Figma (UI design, mockups, visual handoff)

### 9.2 External Communication

**Publisher Updates (If Funded):**
- Monthly milestone reports (progress, blockers, financial burn rate)
- Milestone demos (Prototype, VS, Full Feature, Gold)
- Transparent about risks (no surprises)

**Community (Post-Announcement):**
- Discord server (launch after Milestone 2, when VS is playable)
- Monthly dev blogs (Steam community hub, show progress without spoiling)
- Wishlist campaigns (pre-launch, target 5,000+ before release date announcement)

**Press:**
- No press until Milestone 3 (Full Feature complete)
- Press kit (trailer, screenshots, fact sheet, Steam keys)
- Reach out to YouTubers/streamers 4 weeks before launch

---

## 10. Post-Launch Roadmap (First 6 Months)

**Month 1 Post-Launch:**
- **Patch 1.1:** Hotfixes (critical bugs, save corruption edge cases, balance exploits)
- **Community support:** Discord moderation, bug triage, player feedback aggregation
- **Data analysis:** Which genres are over/underused? Which events fire too often? What's average playtime?

**Month 2-3 Post-Launch:**
- **Patch 1.2:** Quality-of-life improvements
  - Fast-forward button (skip weeks with no input)
  - "Rewind to last season" option
  - More granular stat tooltips
  - Additional Steam achievements (25 new achievements based on player behavior)

**Month 4-6 Post-Launch:**
- **Evaluate DLC viability:** Did we sell 50K+ units? If yes, greenlight DLC.
- **DLC Option 1:** The Streaming Wars (2013-2020 expansion, StreamFlix competitor, binge metrics)
- **DLC Option 2:** Classic Era (1980s-1990s prequel, 3-network oligopoly)
- **Free Update:** Steam Workshop support (expose show templates, genre configs for modding)

**Console Port Decision (Month 6):**
- If PC sales > 50K units AND Steam Deck verified, greenlight Switch port
- Console porting: 3-4 months, $150K additional budget

---

## 11. Success Metrics & KPIs

### Pre-Launch Metrics

| Metric | Target | Gate |
|---|---|---|
| **Wishlists (Steam)** | 5,000+ before launch | Marketing validation |
| **Trailer views** | 50,000+ (YouTube + Steam) | Audience interest |
| **Press coverage** | 10+ articles/previews | Industry awareness |

### Launch Metrics (First Week)

| Metric | Target | Meaning |
|---|---|---|
| **Units sold** | 5,000+ Week 1 | Strong launch |
| **Steam reviews** | 75%+ positive | Design validated |
| **Average playtime** | 8+ hours Week 1 | Engagement |
| **Crash rate** | <0.5% sessions | Stability |

### Long-Term Metrics (First Year)

| Metric | Target | Meaning |
|---|---|---|
| **Units sold** | 50,000+ Year 1 | Breakeven trajectory |
| **Average playtime** | 25+ hours | Replayability validated |
| **Review score** | 80%+ positive (maintained) | Quality sustained |
| **Refund rate** | <5% | Player satisfaction |
| **Wishlist conversion** | 30%+ (wishlists → purchases) | Marketing effective |

---

## 12. Final Notes: Shipping On Time

### The Producer's Commandments

**1. The core loop ships first.**
If The Board doesn't feel good by Week 4, we stop everything and fix it. No exceptions.

**2. Scope is the lever we pull.**
Time and team size are fixed. If we're behind, we cut features. Never add people mid-project (Brooks's Law: adding people to a late project makes it later).

**3. Milestones are gates, not suggestions.**
If Milestone 2 fails playtest, we don't proceed to Milestone 3. We iterate until it passes. Better to slip 2 weeks early than ship a broken game.

**4. Playtesting is not optional.**
External eyes catch what we miss. Every milestone gets 5+ external testers who've never seen the game before.

**5. Communication is a forcing function.**
If someone is blocked for more than 4 hours, they post to Slack. Blockers fester in silence.

**6. Cut scope, not corners.**
Cutting a stretch goal is fine. Shipping with save corruption or broken UI is not. Quality floor is non-negotiable.

**7. Post-launch content is not launch content.**
Upfront mini-game, Writers' room, syndication system — all "nice to have." If they threaten the timeline, they're cut. Post-launch DLC exists for a reason.

**8. The game is done when it's done.**
But we set a target (20 months) and we hit it by managing scope aggressively. Crunch is a management failure. If we're crunching, I (CLOCK) failed.

---

## 13. Risks Summary & Mitigation Strategy

| Risk | Severity | Likelihood | Mitigation | Owner |
|---|---|---|---|---|
| Board UI performance | Critical | Medium | Throttle calcs, profile early, simplify if needed | UI Programmer |
| Show generation repetitive | High | High | 200+ templates, weird pilot roll, playtest in isolation | Gameplay Prog 2 |
| Save corruption | Critical | Medium | JSON format, 3 autosaves, unit tests, repair utility | Lead Programmer |
| Ratings opacity | Medium | High | Detailed tooltips, testing tool, advisor mode fallback | Lead + UI |
| DVR shift feels punishing | Medium | Medium | Gradual intro, new strategies, industry memos | Gameplay Prog 1 |
| Competitor AI feels dumb | Medium | Medium | Distinct personalities, believable mistakes, playtest | Gameplay Prog 1 |
| Event fatigue | Low | Medium | Cap at 5/week, auto-resolve option, frequency slider | Gameplay Prog 2 |
| Scope creep | High | High | Producer veto power, "post-launch" pile, weekly check-ins | Producer (CLOCK) |

---

## 14. Conclusion: The Plan to Ship

PREMIERE is a 20-month project with a $1.5M budget and a 6-person core team. The critical path is 87 weeks with 2 weeks of slack built in. The core loop (Board interaction) is locked by Week 4 or we stop. Milestones are gates — we don't proceed until playtest passes. Scope is the lever we pull when time is fixed. Stretch goals are clearly marked and will be cut if timeline slips.

**What we're building:** A management sim where dragging cards onto a grid feels satisfying, watching ratings arrive feels dramatic, and building a network across 12 seasons feels like a career.

**What we're not building:** 3D graphics, VR, live-service, multiplayer, licensed content, or features that don't serve the core loop.

**What success looks like:** 50,000 units sold in Year 1, 75%+ positive Steam reviews, 25+ hour average playtime, and a stable foundation for post-launch DLC.

**What failure looks like:** Shipping late because we refused to cut scope. Shipping broken because we cut corners instead of features. Burning out the team with crunch because we planned poorly.

I've seen both. This plan avoids failure by being realistic about what's achievable in 20 months with 6 people. If the plan is wrong, we adjust the plan — not by adding time or people, but by cutting scope.

The Board is the game. Everything else supports The Board. If The Board feels good, we ship. If it doesn't, we don't.

Let's ship this on time.

-- CLOCK

---

**Document Status:** Production-Ready
**Next Steps:**
1. Team kickoff (Week 1)
2. First sprint planning session (Week 1, Day 1)
3. Prototype Milestone 1 playtest (Week 13)
4. Vertical Slice Milestone 2 playtest (Week 26)
5. Gold master (Week 87)

**Questions for Stakeholders:**
- Funding secured? (Need $1.5M commitment before kickoff)
- Team hired? (6 core roles, 3 contract roles)
- Office/remote setup confirmed?
- Publisher milestone schedule aligned with this plan?

**Approval Required From:**
- Studio Leadership (budget, timeline, team size)
- Lead Programmer (tech feasibility)
- Producer (CLOCK) — this is my plan, I own it

---

**End of Production Plan**
