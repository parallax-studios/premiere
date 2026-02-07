# PREMIERE -- Game Design Document

**Designed by REED**
**Status: Complete GDD v1.0**
**Genre: Management Sim / Tycoon / Strategy**
**Platform: PC (Steam), Steam Deck**
**Target: Adults 25-45, management sim enthusiasts, TV obsessives**

---

## 0. REED's Note

Let me be blunt. Every management sim I've ever played -- and I've played hundreds -- eventually collapses into one of two failure modes. Either the core interaction is hollow and the game compensates with content (more buildings, more units, more menus), or the core interaction is solid but the systems around it are disconnected -- you're making decisions that don't ripple.

PREMIERE doesn't get to make either mistake. The pitch is extraordinary. The setting is untapped. The fantasy is real. But none of that saves us if the answer to "what's the loop?" is weak. So this document does one thing before anything else: it nails the loop. Every number, every formula, every system described below exists to serve the 30-second act of picking up a show card and deciding where it goes. If that act isn't strategic, readable, and satisfying, we have nothing.

What's the loop? The loop is The Board.

Where's the depth? The depth is in the ripples -- every card you move changes the math of every adjacent slot, every rival's counter-strategy, every advertiser's confidence, and every showrunner's loyalty.

Let's build it.

---

## 1. Player Fantasy Statement

**"I am the most powerful person in entertainment -- the one who decides what America watches, who gets a second season, and whether my network stands for prestige or profit. Every week, I stare at a scheduling board, move the pieces, and live with the consequences. The fantasy is control. The truth is that control is an illusion, and the illusion is addictive."**

This is not a fantasy about making television. The player never writes a script, never directs a scene, never edits a cut. This is a fantasy about *curating and commanding* television -- about being the person who holds a dozen creative visions in their hands and decides which ones survive. The emotional register is executive power: the thrill of a greenlight, the weight of a cancellation, the chess of counterprogramming, and the slow realization that the audience -- that vast, unknowable, fickle audience -- has the only vote that counts.

The player verb is not "create." The player verb is **"schedule."** And scheduling is a bet, every single time.

---

## 2. Core Loop

### 2.1 The 30-Second Loop: The Move

The player picks up a show card from the holding area (or from another slot on The Board), reads its stats at a glance -- genre icon, quality bar, demo skew indicator, cost-per-episode number, lead-in compatibility arrows -- and places it in a timeslot on the weekly grid. The moment the card lands, adjacent slots recalculate: lead-in flow percentages update, demographic overlap indicators shift, and the competitive threat display for that timeslot refreshes against the rival networks' known schedules.

This is the atom of the game. Drag. Read. Place. Ripple. Every other system feeds into this moment or flows out of it. If this doesn't feel tactile, strategic, and consequential, we ship nothing.

**Duration:** 5-15 seconds per card placement, 20-45 seconds when agonizing over a contested slot.

### 2.2 The 5-Minute Loop: The Week

Once the player locks their schedule (or leaves it unchanged), the week simulates. Overnight ratings arrive timeslot by timeslot in a staggered reveal -- Monday night first, then Tuesday, cascading through Sunday. Each night's ratings show: total viewers (millions), 18-49 demo rating, share percentage, and a comparison to the same slot last week and to the competing networks' same-slot numbers.

After the week's ratings land, the player enters the **Response Phase.** Notes pile up in an inbox: talent demands, advertiser reactions, critical reviews, fan campaigns, executive pressure memos, pilot scouting reports. The player triages: respond to the urgent ones, file the rest, and decide whether to make any schedule changes for next week. The player can also spend development budget to greenlight a new pilot, fast-track a midseason replacement, order additional episodes for a performer, or cancel a show.

**Duration:** 3-7 minutes per in-game week.

### 2.3 The Season Loop: September to May

A full television season runs approximately 35 in-game weeks, segmented into strategic phases:

| Phase | Weeks | What Happens |
|---|---|---|
| **Fall Premiere** | Weeks 1-4 (Sep) | New shows launch. First impressions. Huge marketing spend. Audience is sampling. |
| **Fall Settling** | Weeks 5-9 (Oct) | Shows find their audience (or don't). First cancellation decisions. Bubble shows identified. |
| **November Sweeps** | Weeks 10-13 (Nov) | Ratings count for local ad rates. Stunt programming, crossovers, event episodes. Pressure is maximum. |
| **Holiday Lull** | Weeks 14-17 (Dec) | Reruns, specials, reduced originals. Low-pressure period. Planning window for midseason. |
| **Midseason Launch** | Weeks 18-22 (Jan-Feb) | New shows replace cancelled ones. Second wave of premieres. February Sweeps (weeks 21-24). |
| **Spring Grind** | Weeks 23-30 (Mar-Apr) | Long slog. Fatigue sets in. Shows live or die on consistency. Renewals/cancellations announced. |
| **May Sweeps & Finales** | Weeks 31-35 (May) | Season finales. Cliffhangers. Final ratings push. Upfront prep. |

The season ends with two events: the **Emmy Ceremony** (prestige scoring) and the **Annual Review** (network president evaluates your performance against targets). These together determine whether you keep your job, get a budget increase, or face pressure to change strategy.

**Duration:** 2-4 hours per full season.

### 2.4 The Meta Loop: The Career (2000-2012)

Across 12 in-game seasons (roughly 24-48 hours of play for a full career), the player builds a network identity. Decisions compound: greenlight enough prestige dramas and you become the "quality network" that attracts auteur showrunners but struggles with mass-market advertisers. Stack reality shows and procedurals and you're the ratings juggernaut that critics ignore and accountants love.

The meta loop is defined by **era shifts** -- industry-wide changes that alter the strategic landscape:

| Year | Era Shift | Mechanical Impact |
|---|---|---|
| 2000-2002 | Post-Sopranos Prestige Rush | Cable competitors begin bidding for prestige talent. Quality ceiling on broadcast shows increases. |
| 2003-2004 | Reality Explosion | Reality show pilots flood the pipeline. Costs drop 40% for unscripted. Scripted budgets feel the squeeze. |
| 2005-2006 | DVR Early Adoption | 15% of audience time-shifts. Live ratings begin diverging from "Live+3" and "Live+7" numbers. Advertisers start caring about the gap. |
| 2007-2008 | Writers' Strike | Scripted development pipeline gutted for 1.5 seasons. Reality and game shows fill the gap. Showrunner loyalty tested. |
| 2009-2010 | DVR Mainstreaming | 40% of audience time-shifts. Ad revenue model under stress. "Live+7" becomes the standard metric. |
| 2011-2012 | Streaming Rumblings | A new competitor ("StreamFlix") begins poaching talent with no-notes deals and full-season orders. The ground shifts. |

### 2.5 Core Loop Diagram

```
                    +-----------------------+
                    |    THE BOARD           |
                    |  (Scheduling Grid)     |
                    |  Pick up card -> Read  |
                    |  stats -> Place in     |
                    |  slot -> Ripples       |
                    +----------+------------+
                               |
                          [Lock Schedule]
                               |
                               v
                    +----------+------------+
                    |    THE WEEK            |
                    |  Simulate -> Overnight |
                    |  ratings arrive ->     |
                    |  Notes/events pile up  |
                    |  -> Respond/adjust     |
                    +----------+------------+
                               |
                        [Repeat x35]
                               |
                               v
                    +----------+------------+
                    |    THE SEASON          |
                    |  Sweeps -> Midseason   |
                    |  -> Finales -> Emmys   |
                    |  -> Annual Review      |
                    +----------+------------+
                               |
                     [New pilot pool arrives]
                               |
                               v
                    +----------+------------+
                    |    THE CAREER          |
                    |  Network identity      |
                    |  compounds -> Era      |
                    |  shifts alter rules -> |
                    |  Legacy is built       |
                    +----------+------------+
                               |
                      [2012: The Reckoning]
                               |
                               v
                    +----------+------------+
                    |    ENDGAME             |
                    |  Your schedule,        |
                    |  season by season.     |
                    |  The shows you made.   |
                    |  The shows you killed. |
                    |  Judge yourself.       |
                    +-----------------------+
```

---

## 3. Core Mechanics

### 3.1 The Board (Scheduling System)

**Player Verb:** Drag, place, swap, and remove show cards on a 7-day x 3-slot weekly grid.

**System Description:**
The Board is a 7x3 grid representing Monday through Sunday, 8 PM / 9 PM / 10 PM. Each cell holds one show card or is empty (dead air -- never acceptable for more than one week during premiere season). The player drags cards from a holding area (the "bench") onto the grid, or rearranges cards already on the grid.

Each show card displays:
- **Title** and **genre icon** (procedural, drama, comedy, reality, event)
- **Quality Rating (QR):** 1-100 scale. Determines critical reception and long-term audience loyalty.
- **Audience Floor (AF):** Minimum expected viewers in millions, based on genre and timeslot. A cheap procedural has a floor of 5M; an edgy cable-style drama has a floor of 2M.
- **Audience Ceiling (AC):** Maximum potential viewers if everything goes right. A broad comedy might ceiling at 18M; a niche prestige drama might ceiling at 8M.
- **Demo Skew:** Icon indicating primary demographic -- M18-49 (blue), F18-49 (pink), A25-54 (gray), Broad (green).
- **Cost Per Episode (CPE):** In thousands. Ranges from $400K (cheap reality) to $3.5M (prestige drama with A-list cast).
- **Lead-In Compatibility:** Arrows showing how well this show's ending audience matches the next show's starting audience. Green (80%+ retention), yellow (50-79%), red (<50%).
- **Network Fit Score:** How well this show matches your network's established identity. Ranges from 0-100.

**Adjacency Rules:**
When a card is placed, the system calculates **Lead-In Flow** for the card in the next timeslot:

```
Lead-In Bonus = Base Audience * Lead-In Compatibility * Timeslot Decay Factor

Where:
- Base Audience = previous show's actual viewership
- Lead-In Compatibility = demographic overlap percentage (0.0 to 1.0)
- Timeslot Decay Factor = 0.85 (8PM->9PM), 0.75 (9PM->10PM)
```

Example: Your 8 PM broad comedy pulls 12M viewers with a 65% female 18-49 skew. Your 9 PM legal drama has a 55% female 18-49 skew. Demographic overlap is 0.72. Lead-In Bonus = 12M * 0.72 * 0.85 = **7.34M additional base viewers** flowing into the 9 PM slot. That 9 PM show's actual viewership will be its own organic audience plus this lead-in, minus competitive drain from rival networks' 9 PM offerings.

**Feedback:**
When a card is placed, three things happen instantly:
1. The adjacent slots' expected-viewership ranges update with visible number changes (green for increase, red for decrease).
2. The competitive threat panel on the right side of The Board refreshes, showing what rival networks are running against your new placement.
3. A subtle "card snap" sound and a brief highlight animation confirm the placement. Cards in strong lead-in chains glow with a connected line. Cards isolated in weak positions dim slightly.

**Depth:**
A beginner places their highest-rated show in the "best" timeslot (Thursday 9 PM) and hopes. An intermediate player builds lead-in chains and avoids scheduling weak shows against rival flagships. An expert builds **flow architecture** -- entire nights designed as demographic pipelines, where each show's ending audience maps precisely to the next show's opening audience. The expert also practices **counterprogramming**: if every rival runs male-skewing action at 9 PM on Thursdays, the expert schedules a female-skewing drama to capture the uncontested demo. The expert sees empty slots not as problems but as strategic sacrifices -- dead zones where a cheap show absorbs competitive fire to protect the rest of the lineup.

### 3.2 The Pilot Pipeline (Development System)

**Player Verb:** Scout, evaluate, greenlight, and develop pilot scripts into series-ready show cards.

**System Description:**
At the start of each season (and again at midseason), the game generates a **Pilot Pool** -- a set of 25-40 pilot concepts with procedurally generated properties. The player has a **Development Budget** (starting at $35M in Season 1, scaling with network performance) and each pilot has a **Development Cost** to greenlight (ranging from $2M for a cheap reality pilot to $8M for a prestige drama with attached A-list talent).

Each pilot in the pool has:
- **Title and Premise:** A 2-3 sentence logline generated from genre templates and trope combinations. ("BADGE & BURDEN: A burned-out Chicago homicide detective is partnered with an idealistic forensic psychologist. Procedural cases with a slow-burn conspiracy arc.")
- **Genre/Subgenre:** From a taxonomy of 6 genres x 4 subgenres each (24 combinations).
- **Quality Ceiling (QC):** The maximum Quality Rating this show can achieve if everything goes well. Determined by showrunner talent + source material quality + cast attachment. Range: 40-95.
- **Quality Floor (QF):** The minimum Quality Rating if things go poorly. Range: 15-60.
- **Audience Skew Profile:** A distribution across demographic buckets.
- **Showrunner Attachment:** Named AI personality with a track record. Veteran showrunners have higher QC but also higher salary demands and bigger egos.
- **Cast Attachment:** Named AI actors with Star Power ratings (1-10) that directly influence opening-night viewership.
- **Estimated CPE:** What this show will cost per episode if ordered to series.
- **Risk Factor:** A 1-5 rating indicating volatility. High-risk shows have wider gaps between QC and QF -- they might be brilliant or terrible. Low-risk shows are predictable and safe.
- **Test Audience Score:** After greenlighting, a simulated audience test returns a score (1-100) that correlates loosely with actual performance. Loosely. Some bombs test well. Some masterpieces test terribly. The test is information, not truth.

**Greenlight Capacity:** The player can greenlight 8-15 pilots per season depending on budget. Of those, typically 5-9 will go to series (some pilots fail in production and never air). The player must balance quantity vs. quality -- greenlight fewer expensive prestige pilots or more cheap genre entries.

**Pilot Generation Formula:**

```
Quality Ceiling = (Showrunner Talent * 0.4) + (Source Material * 0.3) + (Cast Quality * 0.2) + (Genre Freshness * 0.1) + Random(-5, +5)

Where:
- Showrunner Talent = 1-100 (based on track record)
- Source Material = 1-100 (based on premise originality and genre saturation)
- Cast Quality = 1-100 (based on attached actors' Star Power)
- Genre Freshness = 100 - (number of similar-genre shows currently on air across all networks * 4)
```

**Feedback:**
Greenlit pilots enter a "Development" track visible on the side of The Board. Over 4 in-game weeks, their status updates: "In Production," "Rough Cut," "Test Screening," "Ready for Schedule." At each stage, a brief event card may fire -- the lead drops out, the showrunner delivers a brilliant pilot, the test audience hates the ending. The player sees their investment develop (or deteriorate) in real time.

**Depth:**
A beginner greenlights the highest-QC pilots and ignores cost. An intermediate player balances QC against CPE and demographic gaps in their lineup. An expert reads the *meta* -- they notice that rival networks are over-saturating procedurals, so they greenlight three comedies knowing the competitive landscape will be favorable two seasons from now. The expert also cultivates showrunner relationships across multiple seasons, taking a risk on an unproven writer in Season 2 because that writer's QC ceiling will be 85+ by Season 5 if they get the experience. The pipeline is where you plant seeds. The Board is where you harvest.

### 3.3 The Ratings Engine (Competition System)

**Player Verb:** Observe, analyze, and react to weekly overnight ratings and competitive performance data.

**System Description:**
Three AI-driven rival networks operate simultaneously, each with a strategic personality:

| Rival | Strategy Archetype | Behavior |
|---|---|---|
| **AmeriNet** | The Populist | Prioritizes broad comedies and procedurals. High volume, low risk. Will clone your hits shamelessly. Counterprograms by overwhelming with safe content. |
| **Crowne Broadcasting** | The Prestige Chaser | Invests heavily in quality dramas and auteur showrunners. Lower ratings tolerance, higher award ambition. Will poach your best showrunners with creative-freedom deals. |
| **Pacific Television** | The Disruptor | Leans into reality, event programming, and genre-bending experiments. Unpredictable scheduling. Will launch stunt programming during your sweeps pushes. |

Each rival network runs its own pilot pipeline, scheduling logic, and talent management. Their schedules are partially visible to the player (announced shows and timeslots are public; unannounced midseason moves are hidden until they air).

**Audience Simulation Model:**
Each week, the Ratings Engine resolves viewership for every timeslot across all four networks using this model:

```
Show Viewership = (Organic Audience + Lead-In Bonus - Competitive Drain) * Seasonal Modifier * Event Modifier

Where:
- Organic Audience = f(Quality Rating, Star Power, Marketing Spend, Week Number, Genre Popularity)
  Specifically: AF + ((AC - AF) * (QR/100) * Star Power Modifier * Marketing Modifier * Loyalty Curve)

- Lead-In Bonus = (see 3.1 adjacency formula)

- Competitive Drain = Sum of (Rival Show Appeal * Demographic Overlap * 0.15) for each rival in the same timeslot

- Seasonal Modifier = multiplier based on time of year:
  September premieres: 1.15
  October: 1.05
  November sweeps: 1.20
  December holidays: 0.70
  January: 0.90
  February sweeps: 1.10
  March-April: 0.95
  May sweeps/finales: 1.25

- Event Modifier = special circumstance multiplier (e.g., post-Super Bowl slot: 2.5x, finale episode: 1.3x, scandal involving cast: range 0.8x to 1.4x depending on type)
```

**Loyalty Curve:**
New shows start with a Loyalty Factor of 0.3 (audiences are sampling, not committed). Over weeks of consistent quality, Loyalty rises toward 1.0 following a logarithmic curve:

```
Loyalty = min(1.0, 0.3 + 0.7 * (1 - e^(-0.08 * weeks_on_air)) * (QR / 80))
```

This means a high-quality show (QR 85) reaches 0.8 Loyalty by week 12, while a mediocre show (QR 55) plateaus at 0.65 Loyalty around week 20. Loyalty declines if quality drops: a 10-point QR drop causes Loyalty to bleed at 0.03 per week until it finds a new equilibrium.

**DVR Modifier (Era-Dependent):**

```
Live Viewership = Total Viewership * (1 - DVR Adoption Rate * Show DVR Propensity)

Where:
- DVR Adoption Rate = 0.05 (2000) scaling to 0.45 (2012)
- Show DVR Propensity = 0.1 (reality/live events) to 0.7 (serialized prestige dramas)
```

Live viewership is what advertisers pay for initially. As the era progresses, "Live+3" and eventually "Live+7" metrics unlock, partially recovering ad value from DVR viewers (at 60% and 80% of live CPM respectively).

**Feedback:**
Overnight ratings arrive in a stylized "morning report" screen -- a printout aesthetic with your shows' numbers highlighted. Green arrows for up-week-over-week, red arrows for down. A summary line reads: "Your network averaged 8.4M total viewers, 3.2 in the 18-49 demo. You placed 2nd for the night behind AmeriNet (9.1M)." Critical reviews appear as Metacritic-style scores with pull quotes. Social buzz appears as a "watercooler index" (1-100) measuring cultural conversation.

**Depth:**
Beginners react to ratings. Intermediates predict ratings based on lead-in chains and competitive matchups. Experts model audience flow across the entire landscape -- they know that AmeriNet's Thursday 9 PM flagship is losing its lead actress next season, so they develop a show specifically to exploit that future weakness. Experts also manage the DVR transition: they recognize that a prestige drama pulling 5M live + 4M DVR is generating more total engagement than a procedural pulling 8M live + 1M DVR, and they lobby (via the advertiser system) for Live+7 metrics to become the standard, shifting the revenue model in their favor.

### 3.4 The Talent Web (Relationship System)

**Player Verb:** Hire, manage, negotiate with, appease, and occasionally fire persistent AI-driven talent.

**System Description:**
The Talent Web tracks every named character in the game -- showrunners, actors, writers, directors, and executives -- as persistent entities with the following attributes:

**Showrunner Attributes:**
- **Talent Level (TL):** 1-100. Determines Quality Ceiling contribution.
- **Ego (E):** 1-100. Determines how much creative control they demand, how they react to schedule moves, and their probability of walking.
- **Loyalty (L):** -100 to +100. Starts at 0. Increases when you support their vision; decreases when you interfere, move their show, or cancel their work. At -50, they refuse to work with you. At +50, they accept worse deals to stay.
- **Specialty:** Genre(s) they excel in. A showrunner with Specialty: Legal Drama gets +15 to QC on legal dramas.
- **Career Stage:** Rising (TL growing 2-5 points/season), Peak (stable), Declining (TL dropping 1-3 points/season), Comeback (variable).

**Actor Attributes:**
- **Star Power (SP):** 1-10. Directly modifies show opening-night viewership (each point = +0.5M viewers organic baseline).
- **Salary Demand:** Per-episode fee. Ranges from $25K (unknown) to $750K (megastar).
- **Volatility:** 1-10. High-volatility actors generate tabloid events -- scandals, feuds, rehab stints -- that can spike or tank viewership.
- **Contract Length:** 1-7 seasons. When a contract expires, the actor renegotiates. Stars with hit shows demand 3-5x their original salary.

**Relationship Events:**
Every week, the system rolls for talent events based on attribute thresholds:

| Trigger | Event | Consequence |
|---|---|---|
| Actor Volatility > 7, random roll < 15% | **Tabloid Scandal** | Viewership +8% (curiosity) for 2 weeks, then -5% (advertiser pullback). Advertiser confidence -15 for that show. |
| Showrunner Ego > 70, show moved timeslots | **Creative Revolt** | Showrunner threatens to quit. Player must choose: restore the timeslot (losing the strategic move) or call the bluff (40% chance they leave, taking a QR hit of -12 on the show). |
| Showrunner Loyalty < -30 | **Talent Poaching** | Rival network offers the showrunner a deal. Player must counter-offer (budget cost) or lose them. If lost, any show they're running takes a QR hit of -8 to -20 depending on their TL. |
| Actor contract expires, show is a hit | **Salary Holdout** | Actor demands 3x salary. Player can pay (budget strain), recast (QR -10, viewership -15% for 6 weeks), or write them off (QR -5 if well-written exit, permanent cast change). |
| Showrunner Loyalty > 60 | **Passion Project Pitch** | Showrunner brings you a high-risk, high-QC pilot at a discount development cost. This is the reward for long-term relationship investment. |

**Feedback:**
Talent events appear as phone calls, memos, and Variety headlines. The player's relationship status with key talent is visible on a "Rolodex" screen -- a period-appropriate Rolodex with cards showing each person's face, attributes, current show, and relationship temperature (warm/cool/cold/hostile, represented by a color gradient).

**Depth:**
A beginner hires the best talent available and pays whatever they ask. An intermediate player manages contracts strategically -- locking stars into long deals early, before their shows become hits. An expert cultivates a stable of loyal showrunners over multiple seasons, investing in rising talent when they're cheap and reaping the rewards when they peak. The expert also weaponizes the Talent Web offensively: they know that Crowne Broadcasting's star showrunner is in a contract year, so they offer a lavish deal to poach them -- not because they need the showrunner, but to gut Crowne's flagship.

### 3.5 The Ledger (Business System)

**Player Verb:** Allocate budget across development, marketing, talent, and operations; set advertising rate targets; manage financial health.

**System Description:**
The Ledger tracks the network's financial state across four budget categories:

**Revenue Model:**

```
Weekly Ad Revenue Per Show = Viewers (in millions) * Demo Multiplier * CPM Rate * Ad Slots Per Hour

Where:
- Demo Multiplier:
  18-49 viewers: 2.5x
  25-54 viewers: 1.8x
  55+ viewers: 0.7x
  (These reflect real advertising economics -- the 18-49 demo is gold)

- CPM Rate: Base $25, modified by:
  Brand Safety Score (controversial content: -30%; family-friendly: +15%)
  Network Prestige Rating (Emmy wins boost CPM by 5% per award, up to +25%)
  Season (Sweeps months: +20%; Summer: -25%)

- Ad Slots Per Hour: 16 minutes of commercials = approximately 32 slots per hour at 30 seconds each
```

**Annual Budget Allocation:**

| Category | Starting Budget (Season 1) | Range by Season 12 |
|---|---|---|
| **Development** | $35M | $20M - $60M |
| **Marketing** | $25M | $15M - $50M |
| **Talent Contracts** | $80M | $50M - $200M |
| **Operations** | $20M (fixed) | $18M - $25M |
| **Total** | $160M | $103M - $335M |

Budget for next season is determined by this season's performance:

```
Next Season Budget = This Season Revenue * 0.85 + Parent Company Baseline

Where:
- Parent Company Baseline = $60M (guaranteed floor, unless you're fired)
- The 0.85 multiplier represents the parent company taking their cut
```

**Marketing Spend:**
Marketing budget can be allocated per-show:

| Spend Level | Cost/Show/Season | Effect on Premiere Viewership | Effect on Ongoing |
|---|---|---|---|
| **No Push** | $0 | Baseline | Baseline |
| **Standard** | $1.5M | +12% premiere viewers | +3% ongoing |
| **Heavy Push** | $4M | +25% premiere viewers | +8% ongoing |
| **Event Launch** | $8M | +45% premiere viewers | +12% for 4 weeks, then +5% ongoing |

Event Launch is reserved for 1-2 shows per season. Overuse dilutes effectiveness (each additional Event Launch after the 2nd reduces the bonus by 10 percentage points).

**Feedback:**
The Ledger is a spreadsheet-style screen accessible from The Board's corner -- a tabbed manila folder aesthetic. The top line shows net profit/loss for the current season with a trend arrow. Each show has a row showing revenue generated vs. cost, with a "Margin" column. Profitable shows glow green; money-losing shows glow red. A warning appears when the development budget runs below 20% ("You're out of money to develop new shows -- hope your current lineup holds").

**Depth:**
A beginner spends everything on big shows and goes broke. An intermediate player balances high-cost prestige dramas (low margin, high awards potential) with cheap reality shows (high margin, no prestige). An expert builds a **portfolio strategy**: two or three high-margin "cash cow" shows fund the development of risky passion projects. The expert understands that a $400K-per-episode reality show pulling 6M viewers generates more profit than a $3M-per-episode prestige drama pulling 8M viewers -- but the prestige drama attracts the showrunners who make the next hit. Profit and prestige are currencies in different markets, and the expert trades between them deliberately.

---

## 4. Systems Interactions

### 4.1 Feedback Loops

**Positive Feedback Loop: The Prestige Flywheel**
```
Win Emmy -> Prestige Rating rises -> Better showrunners want to work with you ->
Higher QC pilots enter pipeline -> Better shows on The Board ->
Higher Quality Ratings -> More Emmy nominations -> Win Emmy (loop)
```
This loop is powerful but slow (takes 2-3 seasons to build momentum) and fragile (one bad season of cancellations can crater showrunner trust, breaking the cycle). It also has a built-in tension: prestige shows often rate *lower* than populist alternatives, meaning the flywheel can spin while your budget shrinks.

**Positive Feedback Loop: The Ratings Snowball**
```
High-rated 8 PM show -> Strong lead-in to 9 PM -> Strong lead-in to 10 PM ->
Dominant night -> Advertiser confidence rises -> Bigger marketing budget ->
Attract better talent -> Higher-rated shows -> (loop)
```
This loop is faster (builds within a single season) but vulnerable to a single show's decline -- if the 8 PM anchor falters, the entire night collapses.

**Negative Feedback Loop: The Cost Spiral (Balancing)**
```
Hit show -> Lead actor demands raise -> CPE increases -> Margin shrinks ->
Less development budget -> Fewer new pilots -> Aging lineup ->
Ratings decline -> Revenue drops -> Budget pressure -> (forced correction)
```
This loop prevents any single show from being a permanent advantage. Every hit carries the seed of its own cost escalation. This is the rubber band that prevents runaway dominance.

**Negative Feedback Loop: Genre Saturation (Balancing)**
```
Procedural crime show is a hit -> Player greenlights more procedurals ->
Rivals also launch procedurals -> Genre Freshness score drops ->
New procedural QC ceilings reduced -> Audience fatigues ->
Procedural ratings decline across the landscape -> (genre correction)
```
The Genre Freshness modifier in the pilot generation formula ensures that no single genre can dominate indefinitely. This models real television history: every boom (crime procedurals in the early 2000s, reality in 2003-2006, serialized drama in 2007-2012) eventually exhausts itself.

### 4.2 Cross-System Interactions

| System A | System B | Interaction |
|---|---|---|
| The Board | Ratings Engine | Card placement determines viewership through adjacency, lead-in, and competitive matchup calculations. |
| The Board | Talent Web | Moving a show to a worse timeslot angers its showrunner (Loyalty -10 to -25 depending on Ego). Moving it to a better slot earns gratitude (Loyalty +5 to +15). |
| The Board | The Ledger | Each slot's show generates revenue based on ratings and demo composition. Empty slots generate zero revenue and incur a reputational penalty. |
| Pilot Pipeline | Talent Web | Showrunner attachment to a pilot determines its QC. A showrunner you've burned won't bring you their best projects. |
| Pilot Pipeline | The Ledger | Development budget constrains how many pilots you greenlight. Overspend on development and you can't market what you've built. |
| Ratings Engine | The Ledger | Viewership directly drives ad revenue. But the demo composition matters more than total viewers -- 5M viewers in the 18-49 demo are worth more than 8M viewers skewing 55+. |
| Ratings Engine | Talent Web | A show's ratings affect its talent's leverage. A star on a hit show demands more money. A showrunner on a flop becomes desperate and pliable. |
| Talent Web | Pilot Pipeline | Loyal showrunners bring better pilots (QC +5 to +10 for showrunners with Loyalty > 40). Hostile showrunners bring their best work to rivals instead. |

### 4.3 Emergent Possibilities

These are not scripted -- they arise from system interactions:

- **The Shield Maneuver:** A player discovers that scheduling a cheap, expendable show in a brutal timeslot (e.g., Thursday 8 PM against AmeriNet's juggernaut) protects their expensive shows in other slots. The cheap show dies, but it absorbs competitive fire. This emerges naturally from the cost/benefit calculation of the Ledger + Ratings Engine interaction.

- **The Kingmaker Play:** A player cultivates a young, unproven showrunner over three seasons -- greenlighting their risky pilots, protecting their shows from cancellation, building Loyalty to +80. By Season 4, the showrunner's Talent Level has grown to 90 and they bring a passion project with a QC of 95. The player has manufactured their own prestige hit by investing in the Talent Web.

- **The Poison Pill:** A player notices a rival is about to poach their star actor. Instead of counter-offering, they let the actor go -- knowing that the actor's Volatility rating of 9 will generate scandals that damage the rival's show. The Talent Web becomes a weapon.

- **The DVR Gambit:** In the late-game (2009+), a player deliberately schedules serialized prestige dramas in death slots, accepting low live ratings. Why? Because these shows have high DVR Propensity, and as Live+7 metrics become standard, their true audience is revealed -- and the advertiser CPM adjusts upward. The player was playing the meta before the market caught up.

- **The Sweeps Stunt:** A player holds back a major casting announcement and a crossover event for November Sweeps, stacking them in the same week to create an Event Modifier spike. Combined with marketing spend, they dominate the sweeps month -- not through lineup strength, but through tactical timing.

---

## 5. Progression Design

### 5.1 Player Growth Axes

The player grows along three simultaneous axes:

**Skill Growth (Player Knowledge):**

| Phase | Hours | Player Understands |
|---|---|---|
| **Novice** | 0-2 | Basic card placement, genre matching, "put good shows in good slots" |
| **Apprentice** | 2-6 | Lead-in mechanics, demographic targeting, basic counterprogramming |
| **Practitioner** | 6-15 | Flow architecture, portfolio budgeting, talent cultivation, sweeps strategy |
| **Expert** | 15-30 | Multi-season planning, DVR meta-gaming, rivalry exploitation, pipeline seeding 2 seasons ahead |
| **Master** | 30+ | Whole-landscape thinking -- predicting rival moves, engineering genre cycles, building network legacies |

**Network Growth (Mechanical Progression):**

| Season | Network Status | Unlocks |
|---|---|---|
| 1 | **Newcomer** | Basic Board (5 nights, 2 slots/night). 25 pilot pool. 2 rival networks visible. |
| 2 | **Established** | Full Board (7 nights, 3 slots/night). 30 pilot pool. All 3 rivals visible. Midseason replacement system unlocks. |
| 3-4 | **Contender** | Marketing push system. Emmy campaign mini-game (if stretch goal met). 35 pilot pool. Showrunner loyalty rewards kick in. |
| 5-7 | **Power Player** | Upfront presentation events. Syndication revenue from completed shows. 40 pilot pool. Can poach rival talent offensively. |
| 8-10 | **Institution** | Full DVR metrics. StreamFlix begins poaching. 40 pilot pool but quality ceiling rises. Legacy scoring visible. |
| 11-12 | **Legend or Relic** | Streaming cliff approaches. Final reckoning. All systems at maximum complexity. |

**Network Identity (Reputation Progression):**
The player's decisions build a **Network Identity Score** across five axes, displayed as a radar chart:

- **Prestige** (0-100): Driven by Emmy wins, critical scores, auteur showrunner count
- **Popularity** (0-100): Driven by total viewership, top-rated shows, broad demographic reach
- **Innovation** (0-100): Driven by genre-busting shows, format experiments, risk-taking greenlights
- **Reliability** (0-100): Driven by consistent scheduling, long-running series, low cancellation rate
- **Profitability** (0-100): Driven by margin percentage, budget efficiency, advertiser satisfaction

No network can max all five. The tension between these axes IS the game's thematic core. Prestige trades against Popularity. Innovation trades against Reliability. Profitability constrains everything.

### 5.2 Difficulty Curve

The difficulty curve is **stepped with escalating complexity**, not linear:

```
Difficulty
  |
  |                                              ___________
  |                                         ____/   S11-12
  |                                    ____/    Streaming cliff
  |                              _____/  S8-10
  |                         ____/   DVR disruption
  |                    ____/  S5-7
  |               ____/   Full competitive landscape
  |          ____/  S3-4
  |     ____/   Talent ego + budget pressure
  | ___/  S1-2
  |/  Learning the Board
  +-------------------------------------------------> Time
```

**Difficulty Drivers by Era:**

- **Seasons 1-2:** Limited competition, forgiving budget, small grid. Difficulty comes from learning mechanics. Player can make mistakes and recover.
- **Seasons 3-4:** Full grid, full competition, talent costs escalating. First real budget crunches. Cancellation decisions become agonizing. The game stops being "easy to win" and starts being "interesting to play."
- **Seasons 5-7:** Genre saturation makes hit-finding harder. Rival networks have adapted to your strategy. The Writers' Strike (if playing through 2007-2008) guts your pipeline. Difficulty is strategic, not mechanical.
- **Seasons 8-10:** DVR adoption fundamentally changes the revenue model. Shows you thought were safe are now losing live viewers to time-shifting. Advertisers demand new metrics. Your old strategies don't work anymore. Difficulty is adaptive -- can you change how you think?
- **Seasons 11-12:** StreamFlix poaches your best talent with no-notes deals. The audience is fragmenting. The scheduling grid that was your superpower now feels like a constraint. Difficulty is existential -- can you survive a paradigm shift?

### 5.3 Pacing

**Mechanic Introduction Schedule:**

| When | What's Introduced | What's Tested |
|---|---|---|
| Season 1, Week 1 | The Board (basic placement) | Can you fill a schedule? |
| Season 1, Week 3 | Lead-in mechanics | Can you build a flow? |
| Season 1, Week 8 | First cancellation decision | Can you kill a show? |
| Season 1, November Sweeps | Competitive pressure spike | Can you handle pressure? |
| Season 2, Start | Full 7x3 grid, midseason replacements | Can you manage scale? |
| Season 2, Mid | Talent negotiation events | Can you manage people? |
| Season 3, Start | Marketing allocation system | Can you manage money? |
| Season 3, May | Upfront presentation (stretch) | Can you sell your vision? |
| Season 5 | Syndication revenue | Can you think long-term? |
| Season 6 | DVR metrics begin appearing | Can you read new data? |
| Season 8 | DVR-adjusted revenue model | Can you adapt your strategy? |
| Season 11 | StreamFlix talent poaching | Can you survive disruption? |

**Rule of pacing:** Never introduce a new mechanic during a sweeps month. Sweeps are for *testing* mastery of existing mechanics under pressure. New mechanics are introduced during the lower-pressure Fall Settling or Midseason Launch phases, giving the player 4-6 weeks to learn before the next pressure spike.

---

## 6. Risk Assessment

### 6.1 What Could Be Unfun

**RISK 1: Information Overload (Severity: Critical)**
The Board is a 7x3 grid with 21 slots, each containing a card with 8+ visible stats, against 3 rival networks with their own grids. That is a staggering amount of information. If the player feels overwhelmed -- if they can't read The Board at a glance and identify where the problems are -- the game dies.

*Mitigation:* Visual hierarchy is everything. Show cards must be readable at a glance through *color and icon*, not text. The most important stat (expected viewership range) should be the largest number on the card. Competitive threat should be shown as a single red/yellow/green indicator, not a rival's full card. Details are available on hover/click, but the default view is *strategic overview*. Playtest this first: can a player look at The Board for 3 seconds and tell you which night is their strongest and which is their weakest? If not, the UI has failed.

**RISK 2: The Ratings Reveal Becomes Tedious (Severity: High)**
The weekly ratings reveal is the payoff moment -- the slot machine pull after the strategic bet. If it becomes routine (click through 21 numbers every week for 35 weeks for 12 seasons), it turns from exciting to exhausting. That's 8,820 individual ratings reveals in a full career playthrough.

*Mitigation:* The ratings reveal should be **summarized by default** with an option to drill down. Default view: "Monday: You won the night. Tuesday: Lost to AmeriNet. Wednesday: Split." Then the player clicks into the nights they care about. Highlight only significant changes -- big swings, new lows, new highs, bubble shows. Make the boring weeks fast and the dramatic weeks slow. The system should identify the "story" of each week and lead with it: "BADGE & BURDEN hit a series low. AmeriNet's new comedy crushed you at 8 PM."

**RISK 3: Cancellation Decisions Become Routine (Severity: High)**
The pitch promises that cancellation should "sting." But if the player cancels 3-5 shows every season for 12 seasons, that is 36-60 cancellations. Grief doesn't scale. By Season 4, the player might cancel shows without feeling anything.

*Mitigation:* Not every cancellation should be weighted equally. The system should identify which cancellations are *narratively significant* -- shows with attached high-Loyalty showrunners, cult fan bases, or critical acclaim that were killed by low ratings. These get the full treatment: showrunner reaction, fan campaign, Variety headline, a "legacy card" that records the show forever. Routine cancellations of low-quality filler should be quick and painless. The emotional system should be selective, not exhaustive.

**RISK 4: AI Show Generation Feels Formulaic (Severity: High)**
If by Season 5, the player has seen every combination of genre + trope + character archetype, the pilot pipeline becomes a spreadsheet exercise. "Oh, another legal procedural with a grizzled veteran and a rookie. I've seen this six times." The procedural generation must maintain surprise.

*Mitigation:* Implement a **trope combination engine** with at least 200 base premises across 24 genre/subgenre combos, modified by era-specific cultural events, showrunner specialties, and trend mutations. Use a "weird pilot" roll: 10% of pilots in each pool should be genuine oddities that don't fit any template -- a musical drama, a show-within-a-show, a genre mashup that shouldn't work. These high-Risk Factor pilots are how the system stays surprising.

**RISK 5: The Late Game Feels Punishing (Severity: Medium)**
The DVR disruption and streaming cliff are designed to challenge expert players, but if they feel *unfair* -- if the player has no tools to adapt -- the late game becomes a death march. "I'm losing and there's nothing I can do" is the worst feeling in a strategy game.

*Mitigation:* Every era shift must come with new tools, not just new threats. DVR disruption should also unlock new metrics that reward serialized storytelling. The streaming cliff should introduce "talent retention bonuses" for loyal showrunners who stay when others flee. The player who has built strong relationships and a diverse portfolio should feel challenged but *equipped*. The player who has coasted on one strategy should feel the pain -- but that pain should be the consequence of their choices, not arbitrary punishment.

**RISK 6: The Meta Loop Lacks a Clear Finish (Severity: Medium)**
"The game ends when the world changes beneath you" is thematically beautiful but mechanically ambiguous. What is the player working toward? What does "winning" look like at the end of a 40-hour campaign?

*Mitigation:* The endgame should present a **Legacy Score** -- a composite evaluation of the player's career across multiple dimensions (total viewership generated, Emmys won, profit earned, shows that became "cultural touchstones" -- defined as shows that ran 4+ seasons with QR > 75, and talent relationships maintained). The Legacy Score is not a single number but a *profile* -- a radar chart showing what kind of executive you were. There is no single "win" condition. But the game should make you feel the weight of your career by showing it to you in full, season by season, show by show. The player judges themselves. But the game gives them the evidence.

### 6.2 Playtest Priorities

In order of urgency:

**Playtest 1: The Board Feel (Week 1 of development)**
Before anything else is built, test a static version of The Board with placeholder cards. Can the player drag and place cards smoothly? Is the grid readable? Does the information hierarchy work? Can a player identify their strongest and weakest nights within 5 seconds? Test with 8 people who have never seen the game. If 6 of 8 can answer "which is your best night?" correctly, the UI works. If not, iterate on visual design before building any simulation.

**Playtest 2: The 30-Second Loop (Week 4)**
Test card placement with live adjacency calculations. When a card is placed, do the lead-in numbers update visibly? Does the player feel the *ripple*? Do they understand that moving one card changes the math of adjacent slots? Test with 8 people. Ask: "Why did you put that show there?" If they answer with strategic reasoning ("because the lead-in from the comedy should carry into the drama"), the loop works. If they answer with guessing ("it seemed like a good slot"), the feedback is too opaque.

**Playtest 3: One Full Week Cycle (Week 8)**
Test the complete 5-minute loop: set schedule, simulate week, see ratings, respond to events, adjust. Is the ratings reveal exciting? Is the event inbox manageable? Does the player feel like they're making meaningful decisions in the Response Phase or just clicking through notifications? Measure time-per-week: target is 4-6 minutes. Under 3 minutes means the week is too shallow. Over 8 minutes means there's too much friction.

**Playtest 4: One Full Season (Week 14)**
Test the complete season arc: Fall Premiere through May Sweeps. Does the pacing hold? Do the sweeps months feel different from regular months? Does the midseason replacement system create interesting decisions? Is the cancellation moment appropriately dramatic for significant shows and appropriately quick for filler? Ask at the end: "Do you want to play another season?" If yes, the season loop works. If the player says "I'm satisfied" or "I'm tired," dig into where they felt fatigue.

**Playtest 5: Multi-Season with Era Shifts (Week 22)**
Test three consecutive seasons spanning the Reality Explosion era shift. Does the strategic landscape change meaningfully? Does the player feel they need to adapt? Are they excited by the new challenge or frustrated by the rule change? This tests whether the meta loop justifies a 30+ hour investment.

---

## 7. Economy Tables and Balance Framework

### 7.1 Show Economy Table

| Show Type | CPE Range | Audience Floor | Audience Ceiling | Margin Profile | Strategic Role |
|---|---|---|---|---|---|
| Broad Comedy | $800K-$1.5M | 6M | 18M | High margin if successful | Lead-in builder, 8 PM anchor |
| Legal/Crime Procedural | $1.2M-$2.2M | 5M | 15M | Moderate margin, reliable | Workhorse, any slot |
| Prestige Drama | $2M-$3.5M | 2M | 10M | Low margin, high prestige | Emmy bait, 10 PM prestige |
| Serialized Thriller | $1.5M-$2.5M | 3M | 12M | Moderate margin, volatile | High risk/reward, sweeps weapon |
| Reality/Unscripted | $300K-$800K | 4M | 14M | Extremely high margin | Cash cow, budget filler |
| Event/Limited Series | $2.5M-$4M | 4M | 20M | Negative margin short-term | Prestige spike, sweeps stunt |
| Sitcom (multi-cam) | $600K-$1.2M | 5M | 16M | High margin, long-running | Syndication candidate, 8 PM |
| Newsmagazine | $400K-$700K | 3M | 8M | Very high margin | Friday filler, reliable floor |

### 7.2 Advertiser CPM Table

| Demographic | Base CPM | Premium Events (Sweeps, Finales) | Discount Events (Summer, Reruns) |
|---|---|---|---|
| Adults 18-49 | $25 | $32 | $15 |
| Adults 25-54 | $18 | $23 | $11 |
| Adults 55+ | $7 | $9 | $5 |
| Teens 12-17 | $12 | $15 | $8 |

**Brand Safety Modifier:**

| Content Rating | Modifier |
|---|---|
| Family-friendly | +15% CPM |
| Mainstream | +0% (baseline) |
| Edgy | -15% CPM |
| Controversial | -30% CPM |

### 7.3 Balance Framework: The Prestige-Popularity Tension

This is the central balance relationship in the game. If either prestige or popularity is strictly dominant, the game's thematic core collapses.

**Design Rule:** At any point in the game, a purely prestige-focused strategy and a purely popularity-focused strategy should both be *viable* but *suboptimal*. The optimal strategy should require blending both, with the exact mix depending on era conditions, rival behavior, and network identity.

**How this is enforced:**

- **Prestige advantages:** Better showrunner pipeline (high-TL showrunners prefer prestige networks), Emmy wins boost CPM by up to 25%, prestige shows have higher syndication value per episode.
- **Prestige costs:** Lower average viewership, higher CPE, advertisers pay less for "controversial" or "edgy" content, smaller audience floor means more cancellation risk.
- **Popularity advantages:** Higher raw revenue, bigger marketing budgets, more stable viewership, advertiser confidence is higher, easier to fill the full grid.
- **Popularity costs:** Showrunner talent pool is shallower (the best writers want creative freedom), no Emmy wins (missing the prestige flywheel), genre saturation hits harder because you're competing in crowded lanes, network identity is "generic."

**The balancing lever:** In early eras (2000-2005), popularity is slightly favored because live ratings dominate revenue. In late eras (2008-2012), prestige is slightly favored because DVR-adjusted metrics reward serialized storytelling and critical acclaim drives cultural conversation that transcends raw Nielsen numbers. This era shift forces players to evolve -- a strategy that worked in 2003 is suboptimal by 2010.

### 7.4 Firing Threshold

The player can be fired by the network president (game over for that career) if they meet any of these conditions:

- **Three consecutive seasons** of declining total network viewership AND declining profit.
- **Two consecutive seasons** finishing last place (4th of 4 networks) in total viewers.
- **One catastrophic season** where profit drops below -$20M (bankruptcy threat).
- **Network Identity collapse:** All five identity axes drop below 30 simultaneously (you stand for nothing).

The player receives warnings one season before any firing threshold is reached, giving them a chance to course-correct. The warning comes as a memo from The Suit: corporate language, cold but specific. "The board has noted a concerning trend. We expect improvement. This is not a conversation we want to have again."

---

## 8. Open Questions for Playtesting

These are the questions I don't know the answer to yet. These are the questions that only a player sitting in front of The Board can answer. Every one of these will be resolved by observation, not theory.

1. **What is the right number of cards to manage at peak complexity?** The pitch says 18 shows across seven nights. Is that too many? Does the player feel strategic with 18 cards or just busy? My instinct says 12-15 is the sweet spot for "every card matters" -- but the real grid had more. Test both.

2. **How fast should a week resolve?** The pitch says 3-7 minutes per in-game week. But 35 weeks per season means 2-4 hours per season. Is that right, or should some weeks be "fast-forwardable" with only significant events interrupting? My gut says the player needs a "coast" button for weeks where nothing dramatic happens, but I worry that coasting breaks the feeling of weekly control. Test it.

3. **How much rival network transparency is optimal?** If the player can see all rival schedules perfectly, counterprogramming becomes a solved puzzle. If rivals are fully hidden, the player feels blind. The current design shows announced schedules with hidden midseason moves. Is that the right information ratio, or does the player want more visibility? Or less?

4. **Does the Talent Web need visible relationship numbers or should it be qualitative?** Showing "Loyalty: 43" is precise but gamey. Showing "This showrunner is fond of you" is atmospheric but vague. Management sims historically lean toward visible numbers. But PREMIERE's thematic pitch is that these are *people*, not spreadsheets. What does the player want here? I suspect we need both -- a qualitative surface with numbers available on a detail view -- but test the qualitative-only version first and see if players can intuit relationship states from behavior cues alone.

5. **What is the emotional ceiling on cancellation events?** The pitch says cancellation should "sting." But how much production value do we invest in the sting? A full cinematic sequence with showrunner reactions, fan campaigns, and cast farewells? Or a headline and a card removal? The right answer is probably somewhere in between, but the *exact* amount of emotional staging determines whether the player feels the weight or feels exhausted. Build three versions (minimal, moderate, maximal) and test which one players remember a week later.

6. **Is the 2000-2012 era span too long?** Twelve seasons at 2-4 hours each is a 24-48 hour campaign. That is a serious commitment. Some players will love the epic sweep. Others will bounce at Season 6. Should we offer a "Short Career" mode (2000-2006, pre-DVR) and a "Full Career" mode? Or does cutting the era in half gut the late-game payoff?

7. **How does the AI show generator maintain surprise past Season 8?** By the eighth season, the player will have evaluated 280-320 pilots. If the generation system doesn't maintain novelty, the pipeline becomes a sorting exercise. What is the minimum number of unique premise templates needed? My estimate is 200 base premises with era-specific modifiers, but this needs validation. Run a stress test: generate 400 pilots in sequence and have 10 players rate "how many felt samey."

8. **Should the player be able to set a network-wide strategy that automatically adjusts AI behavior?** For example: "My network prioritizes 18-49 demo" which biases the pilot pipeline toward young-skewing shows. Or is the player's strategy best expressed *only* through individual decisions? The former is more accessible; the latter is purer. I lean toward the latter -- your strategy is what you do, not what you declare -- but it might be too implicit for casual players.

9. **What happens after a firing?** Is it game over? Can the player get hired by another network? Can they restart from a checkpoint? A permadeath career with firing as the fail state is thematically rich but could feel punishing after 20+ hours. An "ironic second chance" -- getting hired by a smaller network after being fired from a big one -- could be an elegant recovery mechanic. But it might also dilute the stakes. Test both.

10. **How does the endgame Legacy Score drive replayability?** If the player finishes a career and sees their Legacy profile, do they immediately want to try a different strategy? ("Last time I was the prestige network. This time I'll be the populist juggernaut.") The answer depends on how different the two strategies *feel*. If prestige and popularity just mean different numbers going up, replayability is low. If they mean fundamentally different pilot pools, talent relationships, rival dynamics, and narrative events, replayability is high. The latter is the goal. Test whether it's achieved.

---

## REED's Closing Note

I've designed a lot of systems in my career. Some of them were clever. Some of them were elegant. The ones that shipped, the ones that players actually loved, had one thing in common: they were *legible*. The player could look at the game state, understand why things were happening, and make a decision that felt *theirs*.

PREMIERE has that potential. The Board is legible. The ratings are legible. The talent is legible. The budget is legible. Every system feeds back into the one place the player is always looking -- that 7x3 grid of show cards under fluorescent light.

But potential is not execution. And execution is not fun. Fun is what happens when a player drags a show card to Thursday at 9 PM, watches the numbers ripple, grins because they just counterprogrammed AmeriNet's flagship with a cheap reality show, and says out loud: "Let's see how that plays."

That moment. That's what we build toward. Everything in this document exists to make that moment possible.

What's the loop? The loop is The Board.

Where's the depth? In every ripple.

How does this feel at hour 20? Like you're the most dangerous person in television.

Let's find the fun.

-- REED
