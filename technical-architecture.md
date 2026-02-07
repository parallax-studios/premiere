# PREMIERE — Technical Architecture Document

**Version:** 1.0
**Author:** BYTE (Lead Programmer)
**Target Platform:** PC (Steam), Steam Deck
**Genre:** Management Sim / Strategy Tycoon
**Projected Development Time:** 16-20 months
**Team Size:** 4-6 (1 lead, 2 gameplay, 1 UI, 1 tools, 1 systems)

---

## 0. Executive Summary

PREMIERE is a data-heavy management sim where the primary interaction is a drag-and-drop scheduling grid. The technical challenge is not complexity — it's *clarity*. The player needs to read dozens of stats at a glance, watch numbers ripple across interconnected systems, and feel like they're moving physical cards on a board. This is fundamentally a simulation engine wrapped in a period-authentic UI that hides its math behind visual metaphors.

**Core technical requirements:**
- Fast, data-driven simulation of audience behavior across 4 networks x 7 nights x 3 slots
- Procedural generation of coherent TV show concepts with consistent stat profiles
- Persistent AI personalities with relationship tracking and event systems
- Drag-and-drop UI that updates adjacency calculations in real-time without frame drops
- Save/load for complex game state (200+ entities, 35 weeks x 12 seasons)
- Modular data architecture for balance iteration

**What this is NOT:**
- 3D graphics pipeline — this is 2D UI with cards and grids
- Network multiplayer — single-player turn-based simulation
- Content-generation AI for scripts — procedural templates with randomized variables
- Reactive gameplay — the player makes decisions, then simulates, then reacts

The tech stack is lean. The data model is the complexity. The UI is the challenge.

---

## 1. Engine & Framework Recommendation

### 1.1 Recommended: Unity (2022 LTS)

**Rationale:**
- Best-in-class UI Toolkit for complex editor-style interfaces (The Board is essentially an in-game editor)
- Excellent 2D performance for card-based rendering
- C# is the right language for data-heavy simulation — readable, performant enough, excellent tooling
- Easy cross-platform build pipeline (PC, Steam Deck, console ports later)
- Mature JSON serialization for save systems
- Large asset store for UI components, icons, card templates
- I've shipped four management sims in Unity. The toolchain is known, stable, and fast to iterate.

**What Unity gives us:**
- IMGUI/UI Toolkit for The Board interface (drag handles, snap-to-grid, live stat updates)
- ScriptableObjects for data-driven show templates, genre definitions, era configs
- Coroutine system for week simulation and staggered rating reveals
- Built-in profiler to validate frame time during stat recalculations
- TextMeshPro for clean, readable typography (critical for card text)

**What we don't use from Unity:**
- 3D rendering pipeline (delete it)
- Physics engine (we have a custom grid snapping system)
- Animation system (UI tweening via DOTween, not Animator)
- Networking stack (N/A)

**Alternative Considered: Godot 4.x**
- Pros: Open-source, lean, good UI system, excellent 2D performance
- Cons: Smaller talent pool, fewer management sim precedents, less mature tooling for complex data management, no Steam Deck pre-optimization
- Verdict: Godot is great for indie action games. Unity is better for data-driven sims. Stick with Unity.

**Alternative Considered: Custom Engine (C++ / SDL)**
- Pros: Full control, no Unity overhead, ultra-lean
- Cons: 6+ months of infrastructure work before we write gameplay code. This is how projects die. Never again.
- Verdict: Hell no. I learned this lesson the hard way.

### 1.2 Supporting Libraries

| Library | Purpose | Rationale |
|---|---|---|
| **DOTween** | UI animation, card movement, number tickers | Industry-standard tweening. Handles card drag smoothness and stat ripple animations. |
| **Odin Inspector** | Editor tooling for ScriptableObject workflows | Makes data entry painless. Designers can edit show templates, genre configs, and event triggers without touching code. |
| **TextMeshPro** | Typography | Crisp text rendering for card stats, ratings reports, headlines. |
| **Newtonsoft.Json** | Save/load serialization | Mature, handles complex object graphs, human-readable save files for debugging. |
| **NaughtyAttributes** | Inspector quality-of-life | Conditional fields, validation, quick buttons. Keeps inspectors clean during rapid iteration. |

---

## 2. Core Systems Architecture

### 2.1 High-Level Component Diagram

```
┌─────────────────────────────────────────────────────────────┐
│                      GAME CONTROLLER                         │
│  (Master clock, season state, input routing)                │
└────────────────┬────────────────────────────────────────────┘
                 │
      ┌──────────┼──────────┐
      │          │           │
      ▼          ▼           ▼
┌─────────┐ ┌─────────┐ ┌─────────┐
│  BOARD  │ │ RATINGS │ │  PILOT  │
│ SYSTEM  │ │ ENGINE  │ │ PIPELINE│
└────┬────┘ └────┬────┘ └────┬────┘
     │           │           │
     └───────────┼───────────┘
                 │
                 ▼
         ┌──────────────┐
         │  TALENT WEB  │
         │  (Relations) │
         └──────┬───────┘
                │
                ▼
         ┌──────────────┐
         │   LEDGER     │
         │  (Economy)   │
         └──────────────┘
```

**Data flow:**
1. Player drags show card on BOARD SYSTEM
2. BOARD SYSTEM triggers adjacency recalculation (local)
3. BOARD SYSTEM queries RATINGS ENGINE for expected viewership given new placement
4. RATINGS ENGINE reads competitor schedules, calculates competitive drain
5. Updated stats flow back to BOARD SYSTEM UI
6. When week simulates, RATINGS ENGINE resolves all shows
7. Results feed into TALENT WEB (showrunner reactions to ratings)
8. Results feed into LEDGER (revenue calculation)
9. Events generated from TALENT WEB and LEDGER flow to player inbox

**Design principle:** Systems communicate through events and queries, not direct references. BOARD SYSTEM doesn't "know about" TALENT WEB — it fires an event `ShowMovedToNewSlot(showID, oldSlot, newSlot)` and TALENT WEB subscribes to that event. This keeps systems decoupled and testable.

### 2.2 Data Flow — One Week Simulation

```
Player locks schedule
     ↓
[Week Simulation Begins]
     ↓
For each night (Mon-Sun):
  For each timeslot (8PM, 9PM, 10PM):
    ├─ Calculate organic audience (show quality, star power, marketing)
    ├─ Calculate lead-in bonus (previous slot's viewership x compatibility)
    ├─ Calculate competitive drain (rival shows in same slot)
    ├─ Apply seasonal modifiers (sweeps, holidays)
    ├─ Apply event modifiers (scandals, finales)
    └─ Write final viewership to show's rating history
     ↓
[All ratings resolved]
     ↓
For each show:
  ├─ Calculate ad revenue (viewership x demo x CPM)
  ├─ Subtract episode cost
  └─ Update network budget
     ↓
[Economy updated]
     ↓
Roll for talent events (scandals, contract disputes, loyalty shifts)
     ↓
Roll for industry events (strike rumors, genre trends)
     ↓
Package all events into player inbox
     ↓
[Week complete — present results to player]
```

**Performance target:** Full week simulation must complete in under 200ms on minimum spec hardware. This is 21 shows x 4 networks = 84 rating calculations + economy + event rolls. All of this is pure math — no rendering, no I/O. Easily achievable. Profile it anyway.

---

## 3. Key Gameplay Systems Technical Design

### 3.1 The Board (Scheduling Grid)

**Architecture:**

```
BoardSystem (MonoBehaviour)
├─ BoardGrid (Data model: 7 days x 3 slots, stores ShowCard IDs)
├─ CardHolderUI (Visual grid of 21 UI slots + bench area)
├─ ShowCardUI (Prefab: draggable card with stat displays)
├─ AdjacencyCalculator (Service: computes lead-in bonuses)
└─ CompetitiveDisplay (UI panel: shows rival schedules for selected slot)
```

**ShowCard Data Model (ScriptableObject):**

```csharp
[CreateAssetMenu(fileName = "Show", menuName = "PREMIERE/Show")]
public class ShowData : ScriptableObject
{
    // Identity
    public string showTitle;
    public string premise;  // 2-3 sentence logline
    public Genre genre;
    public SubGenre subGenre;

    // Stats
    public int qualityRating;        // 1-100
    public float audienceFloor;      // millions
    public float audienceCeiling;    // millions
    public DemoProfile demoSkew;     // struct with M18-49, F18-49, A25-54, etc.
    public int costPerEpisode;       // thousands

    // Relationships
    public ShowrunnerData attachedShowrunner;
    public List<ActorData> cast;

    // Runtime state (not in ScriptableObject — stored in instance)
    public int episodesAired;
    public float currentLoyalty;
    public List<float> ratingHistory;  // viewership over time
}
```

**Drag-and-Drop Implementation:**

Unity's UI Toolkit provides `IPointerDownHandler`, `IDragHandler`, `IEndDragHandler`. Each ShowCardUI implements these interfaces:

```csharp
public void OnBeginDrag(PointerEventData eventData)
{
    // Store original slot
    // Set card alpha to 0.7 (dragging state)
    // Disable raycast target (so we can detect drop zones)
}

public void OnDrag(PointerEventData eventData)
{
    // Move card RectTransform to follow pointer
    // Raycast to detect valid drop zones
    // Highlight drop zone (green if valid placement, red if occupied)
}

public void OnEndDrag(PointerEventData eventData)
{
    // Raycast for final drop zone
    // If valid: BoardSystem.PlaceCard(showID, dayIndex, slotIndex)
    // If invalid: Tween card back to original position
    // Trigger adjacency recalculation
}
```

**Adjacency Recalculation (Real-Time Feedback):**

When a card is placed, three UI updates must happen within one frame:
1. The placed card's expected viewership range updates
2. The next slot's lead-in bonus updates (if one exists)
3. The competitive threat indicator refreshes

```csharp
public void PlaceCard(ShowData show, int day, int slot)
{
    // Update data model
    boardGrid[day, slot] = show.instanceID;

    // Calculate new expected viewership
    float organic = CalculateOrganicAudience(show);
    float leadInBonus = 0f;

    if (slot > 0) // Has a lead-in show
    {
        ShowData prevShow = GetShow(day, slot - 1);
        if (prevShow != null)
        {
            float demoOverlap = DemoProfile.Overlap(prevShow.demoSkew, show.demoSkew);
            float decayFactor = slot == 1 ? 0.85f : 0.75f; // 8->9 vs 9->10
            leadInBonus = prevShow.projectedViewership * demoOverlap * decayFactor;
        }
    }

    show.projectedViewership = organic + leadInBonus;

    // Update next slot (cascade)
    if (slot < 2)
    {
        ShowData nextShow = GetShow(day, slot + 1);
        if (nextShow != null)
        {
            RecalculateSlot(day, slot + 1); // Recursive for cascading updates
        }
    }

    // Fire event for UI refresh
    OnBoardChanged?.Invoke(day, slot);
}
```

**Performance Notes:**
- Full grid recalculation: 21 slots x 4 calculations per slot = 84 operations. This is trivial.
- Do NOT recalculate on mouse hover (expensive). Only on placement.
- Cache competitor schedules per frame (don't query RatingsEngine 21 times/frame).

**UI Design Constraints:**
- Card size: 220px wide x 140px tall (balances readability with grid density)
- Grid spacing: 10px between cards
- Text hierarchy: Title (18pt bold) > Quality bar (visual) > Stats (12pt) > Detail text (10pt, hidden until hover)
- Color coding: Genre icon determines card border color. Lead-in compatibility arrows are green/yellow/red.
- Animations: Card placement snaps with elastic easing (0.2s). Stat changes ticker-animate (0.3s).

### 3.2 The Pilot Pipeline (Development System)

**Architecture:**

```
PilotGenerator (Service)
├─ GenreTemplateLibrary (ScriptableObject database: 24 genre/subgenre combos)
├─ PremiseGenerator (Procedural text generation from templates)
├─ StatCalculator (Rolls QC, QF, audience skew, CPE)
└─ TalentAttacher (Assigns showrunners/actors from available pool)

PilotPoolUI (MonoBehaviour)
├─ PilotCardUI (Displays pilot info, greenlight button)
└─ DevelopmentTracker (Shows greenlit pilots in production stages)
```

**Procedural Show Generation:**

Shows are generated from templates with random variables filled in:

```csharp
[CreateAssetMenu(fileName = "GenreTemplate", menuName = "PREMIERE/GenreTemplate")]
public class GenreTemplate : ScriptableObject
{
    public Genre genre;
    public SubGenre subGenre;

    // Premise building blocks
    public List<string> protagonistTypes;  // "burned-out detective", "idealistic lawyer"
    public List<string> settings;          // "Chicago PD", "Manhattan law firm"
    public List<string> hooks;             // "solving cases while uncovering conspiracy"

    // Stat ranges
    public Vector2Int qualityCeilingRange;  // e.g., (60, 90)
    public Vector2Int qualityFloorRange;    // e.g., (30, 55)
    public Vector2 audienceFloorRange;      // millions
    public Vector2 audienceCeilingRange;
    public Vector2Int costPerEpisodeRange;  // thousands

    // Demo profile defaults
    public DemoProfile typicalSkew;
}
```

**Generation Algorithm:**

```csharp
public ShowData GeneratePilot(GenreTemplate template, int currentSeason)
{
    ShowData pilot = ScriptableObject.CreateInstance<ShowData>();

    // Build premise
    string protagonist = template.protagonistTypes.RandomElement();
    string setting = template.settings.RandomElement();
    string hook = template.hooks.RandomElement();
    pilot.premise = $"{protagonist} in {setting}, {hook}.";

    // Generate title (markov chain from template title patterns)
    pilot.showTitle = TitleGenerator.Generate(template.genre);

    // Roll quality ceiling
    int baseCeiling = Random.Range(template.qualityCeilingRange.x,
                                     template.qualityCeilingRange.y);

    // Attach showrunner (influences final QC)
    ShowrunnerData showrunner = TalentPool.GetAvailableShowrunner(template.genre);
    pilot.attachedShowrunner = showrunner;

    float showrunnerBonus = showrunner.talentLevel * 0.3f;
    pilot.qualityRating = Mathf.Clamp(baseCeiling + showrunnerBonus, 40, 95);

    // Roll audience ranges
    pilot.audienceFloor = Random.Range(template.audienceFloorRange.x,
                                        template.audienceFloorRange.y);
    pilot.audienceCeiling = pilot.audienceFloor + Random.Range(4f, 12f);

    // Calculate CPE
    pilot.costPerEpisode = Random.Range(template.costPerEpisodeRange.x,
                                         template.costPerEpisodeRange.y);

    // Adjust for era (2007+ costs rise 15% due to prestige arms race)
    if (currentSeason >= 7)
        pilot.costPerEpisode = (int)(pilot.costPerEpisode * 1.15f);

    // Demo skew (with random variation)
    pilot.demoSkew = template.typicalSkew.Vary(0.1f); // +/- 10% noise

    return pilot;
}
```

**Title Generation:**

Simple Markov chain trained on real 2000s TV show titles:

```
Corpus: ["CSI: Crime Scene Investigation", "Law & Order", "The Sopranos",
         "Without a Trace", "NCIS", "Cold Case", "The Wire", ...]

Pattern extraction:
- Procedurals: [Noun]: [Descriptor] or [Adjective] [Noun]
- Dramas: The [Noun]
- Comedies: [Name] [Preposition] [Place/Situation]

Generated examples:
- "Badge: Special Crimes" (procedural)
- "The Precinct" (drama)
- "Dave in Therapy" (comedy)
```

Store 500 pre-generated title patterns in a JSON file. Pull randomly and fill in variables. Fast, deterministic, good enough.

**Why not GPT for show generation?**
- API cost per pilot: ~$0.01. Over 300 pilots per playthrough = $3 per player in API costs. Unacceptable.
- Latency: 2-5 seconds per API call. Loading a pilot pool would take 60+ seconds. Unacceptable.
- Consistency: GPT can generate incoherent premises or stats that don't match genre. We need tight control.
- Offline play: Requires internet. Deal-breaker.

Template-based generation with randomized variables is faster, cheaper, more controllable, and offline. Ship it.

### 3.3 The Ratings Engine (Audience Simulation)

**Architecture:**

```
RatingsEngine (Singleton Service)
├─ AudienceModel (Calculates viewership for one show)
├─ CompetitorAI (Manages 3 rival networks' scheduling logic)
├─ SeasonalModifiers (Data: sweeps multipliers, holiday drops)
└─ RatingHistoryTracker (Stores all viewership data for analysis)
```

**Core Simulation Formula:**

This runs for every show on every network every simulated week.

```csharp
public float SimulateViewership(ShowData show, int day, int slot, int weekNumber)
{
    // 1. Organic audience
    float organic = CalculateOrganicAudience(show, weekNumber);

    // 2. Lead-in bonus
    float leadIn = CalculateLeadInBonus(show, day, slot);

    // 3. Competitive drain
    float drain = CalculateCompetitiveDrain(show, day, slot);

    // 4. Seasonal modifier
    float seasonalMod = GetSeasonalModifier(weekNumber);

    // 5. Event modifiers (finales, scandals)
    float eventMod = GetEventModifier(show, weekNumber);

    // Final calculation
    float viewership = (organic + leadIn - drain) * seasonalMod * eventMod;

    // Clamp to floor/ceiling
    return Mathf.Clamp(viewership, show.audienceFloor, show.audienceCeiling);
}
```

**Organic Audience Calculation:**

```csharp
private float CalculateOrganicAudience(ShowData show, int weekNumber)
{
    // Base calculation
    float qualityFactor = show.qualityRating / 100f;
    float baseAudience = Mathf.Lerp(show.audienceFloor,
                                     show.audienceCeiling,
                                     qualityFactor);

    // Star power bonus
    float starPower = show.cast.Sum(actor => actor.starPower);
    float starBonus = starPower * 0.5f; // Each star power point = +0.5M viewers

    // Marketing modifier
    float marketingMod = show.marketingLevel switch
    {
        MarketingLevel.None => 1.0f,
        MarketingLevel.Standard => 1.12f,
        MarketingLevel.Heavy => 1.25f,
        MarketingLevel.Event => 1.45f,
        _ => 1.0f
    };

    // Loyalty curve (builds over time)
    float loyalty = CalculateLoyalty(show, weekNumber);

    return (baseAudience + starBonus) * marketingMod * loyalty;
}

private float CalculateLoyalty(ShowData show, int weekNumber)
{
    // New shows start at 30% loyalty
    // High-quality shows reach 80-100% by week 12
    float weeksOnAir = show.episodesAired;
    float qualityMod = show.qualityRating / 80f;

    float loyalty = 0.3f + 0.7f * (1f - Mathf.Exp(-0.08f * weeksOnAir)) * qualityMod;
    return Mathf.Clamp01(loyalty);
}
```

**Competitive Drain Calculation:**

```csharp
private float CalculateCompetitiveDrain(ShowData show, int day, int slot)
{
    float totalDrain = 0f;

    // Get all rival shows in the same timeslot
    List<ShowData> rivals = GetRivalShows(day, slot);

    foreach (ShowData rival in rivals)
    {
        // Calculate appeal of rival show
        float rivalAppeal = rival.qualityRating / 100f * rival.audienceCeiling;

        // Calculate demographic overlap
        float demoOverlap = DemoProfile.Overlap(show.demoSkew, rival.demoSkew);

        // Drain is proportional to rival's appeal and demo overlap
        totalDrain += rivalAppeal * demoOverlap * 0.15f;
    }

    return totalDrain;
}
```

**Seasonal Modifiers (Data-Driven):**

Store in ScriptableObject:

```csharp
[CreateAssetMenu(fileName = "SeasonCalendar", menuName = "PREMIERE/SeasonCalendar")]
public class SeasonCalendar : ScriptableObject
{
    public List<WeekModifier> weekModifiers;
}

[System.Serializable]
public struct WeekModifier
{
    public int weekNumber;
    public string eventName;   // "November Sweeps", "Holiday Lull"
    public float multiplier;   // 1.20, 0.70, etc.
}
```

Example data:

```json
{
    "weekModifiers": [
        { "weekNumber": 1, "eventName": "Fall Premiere", "multiplier": 1.15 },
        { "weekNumber": 10, "eventName": "November Sweeps Start", "multiplier": 1.20 },
        { "weekNumber": 14, "eventName": "Holiday Lull", "multiplier": 0.70 },
        { "weekNumber": 31, "eventName": "May Sweeps", "multiplier": 1.25 }
    ]
}
```

### 3.4 The Talent Web (Relationship System)

**Architecture:**

```
TalentManager (Singleton Service)
├─ ShowrunnerPool (List<ShowrunnerData>: persistent entities)
├─ ActorPool (List<ActorData>: persistent entities)
├─ RelationshipTracker (Stores loyalty values: Dictionary<int, int>)
└─ EventRoller (Generates talent events based on triggers)
```

**ShowrunnerData (ScriptableObject):**

```csharp
[CreateAssetMenu(fileName = "Showrunner", menuName = "PREMIERE/Showrunner")]
public class ShowrunnerData : ScriptableObject
{
    // Identity
    public string showrunnerName;
    public Sprite portrait;

    // Stats
    public int talentLevel;         // 1-100
    public int ego;                 // 1-100
    public int loyalty;             // -100 to +100
    public Genre specialty;         // Gets +15 QC bonus in this genre
    public CareerStage stage;       // Rising, Peak, Declining, Comeback

    // Track record
    public List<ShowData> showHistory;
    public int emmyWins;
    public int emmyNominations;

    // Personality (for event text generation)
    public PersonalityTraits traits;  // e.g., "Perfectionist", "Volatile", "Collaborative"
}
```

**Loyalty System:**

Loyalty changes based on player actions:

| Action | Loyalty Delta |
|---|---|
| Greenlight their pilot | +10 to +15 |
| Renew their show | +8 |
| Cancel their show (ratings < 50% of slot average) | -5 (justified cancellation) |
| Cancel their show (ratings > 80% of slot average) | -20 to -30 (betrayal) |
| Move show to better timeslot | +5 to +15 |
| Move show to worse timeslot | -10 to -25 (scales with ego) |
| Give them a raise | +5 |
| Refuse their raise demand | -10 |
| Win Emmy for their show | +20 |

**Event Rolling System:**

Every week, for each showrunner/actor, roll for events:

```csharp
public void RollTalentEvents(int weekNumber)
{
    foreach (ShowrunnerData showrunner in activeShowrunners)
    {
        // Creative revolt check
        if (showrunner.ego > 70 && showrunner.show.slotChangedThisWeek)
        {
            if (Random.value < 0.25f) // 25% chance
            {
                FireEvent(new CreativeRevoltEvent(showrunner));
            }
        }

        // Poaching check (rival networks)
        if (showrunner.loyalty < -30)
        {
            if (Random.value < 0.15f) // 15% chance per week
            {
                FireEvent(new TalentPoachingEvent(showrunner, GetRandomRival()));
            }
        }

        // Passion project pitch (reward for high loyalty)
        if (showrunner.loyalty > 60 && showrunner.seasonsSinceLastPitch > 2)
        {
            if (Random.value < 0.10f)
            {
                FireEvent(new PassionProjectPitchEvent(showrunner));
            }
        }
    }

    foreach (ActorData actor in activeActors)
    {
        // Scandal check
        if (actor.volatility > 7)
        {
            float scandalChance = (actor.volatility - 6) * 0.03f; // 3-12% range
            if (Random.value < scandalChance)
            {
                FireEvent(new ActorScandalEvent(actor));
            }
        }

        // Contract expiration
        if (actor.contractWeeksRemaining == 4) // 4 weeks warning
        {
            FireEvent(new ContractExpiringEvent(actor));
        }
    }
}
```

**Event Resolution:**

Events present the player with choices:

```csharp
public class CreativeRevoltEvent : TalentEvent
{
    public ShowrunnerData showrunner;

    public override string GetDescription()
    {
        return $"{showrunner.showrunnerName} is furious about the timeslot move. " +
               $"They're threatening to quit unless you restore the original slot.";
    }

    public override List<EventChoice> GetChoices()
    {
        return new List<EventChoice>
        {
            new EventChoice
            {
                text = "Restore the timeslot",
                consequence = () => {
                    // Move show back
                    // Loyalty +10 (crisis averted)
                    // But lose strategic positioning
                }
            },
            new EventChoice
            {
                text = "Call their bluff",
                consequence = () => {
                    if (Random.value < 0.4f) {
                        // They actually quit
                        // Show QR -12 to -20
                        // Replace showrunner
                    } else {
                        // They stay but resent you
                        // Loyalty -15
                    }
                }
            },
            new EventChoice
            {
                text = "Negotiate a compromise (costs $2M marketing push)",
                consequence = () => {
                    // Spend $2M to keep show in new slot but with extra marketing
                    // Loyalty -5 (still annoyed but mollified)
                }
            }
        };
    }
}
```

**Performance Note:**
Talent events are rolled once per week, not per frame. With ~30-50 active talent entities, this is ~50 probability checks per week. Trivial cost.

### 3.5 The Ledger (Economy System)

**Architecture:**

```
EconomyManager (Singleton Service)
├─ BudgetTracker (Stores current budget allocations)
├─ RevenueCalculator (Computes ad revenue per show per week)
└─ FinancialReport (Generates end-of-season summary)
```

**Revenue Calculation:**

```csharp
public float CalculateWeeklyRevenue(ShowData show, float viewership)
{
    // Break viewership into demographic buckets
    DemoBreakdown demos = show.demoSkew.ApplyToViewership(viewership);

    // Calculate weighted viewership (18-49 demo worth more)
    float weighted18_49 = demos.adults18_49 * 2.5f;
    float weighted25_54 = demos.adults25_54 * 1.8f;
    float weighted55Plus = demos.adults55Plus * 0.7f;

    float weightedViewership = weighted18_49 + weighted25_54 + weighted55Plus;

    // Base CPM
    float baseCPM = 25f;

    // Brand safety modifier
    float safetyMod = show.contentRating switch
    {
        ContentRating.FamilyFriendly => 1.15f,
        ContentRating.Mainstream => 1.0f,
        ContentRating.Edgy => 0.85f,
        ContentRating.Controversial => 0.70f,
        _ => 1.0f
    };

    // Network prestige modifier (Emmy wins boost CPM)
    float prestigeMod = 1.0f + (networkEmmyWins * 0.05f); // +5% per Emmy, capped at +25%
    prestigeMod = Mathf.Min(prestigeMod, 1.25f);

    // Seasonal modifier
    float seasonalMod = GetSeasonalCPMModifier(currentWeek);

    float adjustedCPM = baseCPM * safetyMod * prestigeMod * seasonalMod;

    // Ad slots per hour: 16 minutes of commercials = 32 slots
    int adSlotsPerHour = 32;

    // Revenue = (weighted viewership in millions) * CPM * ad slots
    float revenue = weightedViewership * adjustedCPM * adSlotsPerHour;

    return revenue;
}
```

**Budget Allocation UI:**

At season start, player allocates budget:

```
Total Budget: $180M

Allocate:
- Development: [____$35M____] (slider, min $15M, max $60M)
- Marketing: [____$28M____] (slider, min $10M, max $50M)
- Talent: [____$97M____] (auto-calculated from current contracts)
- Operations: [____$20M____] (fixed)

Remaining: $0M
```

**Profit/Loss Tracking:**

```csharp
public class SeasonFinancials
{
    public int season;

    // Revenue
    public float totalAdRevenue;
    public float syndicationRevenue; // Only after shows complete 4+ seasons

    // Costs
    public float developmentSpend;
    public float marketingSpend;
    public float talentContracts;
    public float episodeProductionCosts;
    public float operationalOverhead;

    // Net
    public float netProfit => (totalAdRevenue + syndicationRevenue) -
                               (developmentSpend + marketingSpend +
                                talentContracts + episodeProductionCosts +
                                operationalOverhead);

    public float profitMargin => netProfit / (totalAdRevenue + syndicationRevenue);
}
```

---

## 4. AI & Simulation Systems

### 4.1 Competitor AI (Rival Networks)

Three rival networks with distinct strategies:

**AmeriNet (The Populist):**

```csharp
public class AmeriNetAI : CompetitorAI
{
    public override void BuildSchedule(PilotPool availablePilots)
    {
        // Strategy: Prioritize high audience ceiling, low cost
        var sorted = availablePilots.OrderByDescending(p =>
            p.audienceCeiling / (p.costPerEpisode / 1000f)); // Value per dollar

        // Greenlight top 12
        foreach (var pilot in sorted.Take(12))
        {
            Greenlight(pilot);
        }

        // Schedule: Anchor 8 PM with broad comedies
        // Fill 9 PM with procedurals
        // Stack reality shows on Fridays
    }

    public override void ReactToPlayerSuccess(ShowData playerHitShow)
    {
        // AmeriNet clones hits
        // 50% chance to generate a copycat show next season
        if (Random.value < 0.5f)
        {
            GenerateCopycatShow(playerHitShow.genre, playerHitShow.subGenre);
        }
    }
}
```

**Crowne Broadcasting (The Prestige Chaser):**

```csharp
public class CrowneBroadcastingAI : CompetitorAI
{
    public override void BuildSchedule(PilotPool availablePilots)
    {
        // Strategy: Prioritize high quality ceiling, auteur showrunners
        var sorted = availablePilots.OrderByDescending(p =>
            p.qualityCeiling + p.showrunner.talentLevel);

        // Greenlight top 8 (fewer but higher quality)
        foreach (var pilot in sorted.Take(8))
        {
            Greenlight(pilot);
        }

        // Schedule: Tuesday 10 PM prestige block
        // Sunday night drama stack
    }

    public override void PoachTalent()
    {
        // Target player's high-loyalty showrunners with creative-freedom deals
        var targetShowrunner = playerNetwork.showrunners
            .Where(sr => sr.talentLevel > 75 && sr.loyalty > 30)
            .OrderByDescending(sr => sr.talentLevel)
            .FirstOrDefault();

        if (targetShowrunner != null)
        {
            TryPoach(targetShowrunner, offerBonus: 50); // +50% loyalty bonus for offer
        }
    }
}
```

**Pacific Television (The Disruptor):**

```csharp
public class PacificTelevisionAI : CompetitorAI
{
    public override void BuildSchedule(PilotPool availablePilots)
    {
        // Strategy: 40% reality, 30% genre experiments, 30% safe procedurals
        var reality = availablePilots.Where(p => p.genre == Genre.Reality).Take(5);
        var weird = availablePilots.Where(p => p.riskFactor > 3).Take(4);
        var safe = availablePilots.Where(p => p.genre == Genre.Procedural).Take(4);

        foreach (var pilot in reality.Concat(weird).Concat(safe))
        {
            Greenlight(pilot);
        }

        // Schedule: Unpredictable timeslot moves mid-season
        // Event programming during player's sweeps pushes
    }

    public override void CounterProgram()
    {
        // Pacific intentionally schedules stunt programming during player's big weeks
        if (IsPlayerSweepsWeek())
        {
            ScheduleEventSpecial(targetSlot: playerNetwork.strongestSlot);
        }
    }
}
```

**AI Decision Frequency:**
- Schedule building: Once per season (pilot pool allocation)
- Timeslot adjustments: Once per month (midseason moves)
- Talent poaching: Rolled once every 4 weeks (15% chance)
- Counterprogramming: Reactive to player's known event weeks

**AI Difficulty Scaling:**

AI gets smarter over seasons:

| Season | AI Behavior |
|---|---|
| 1-2 | Random scheduling, no counterprogramming |
| 3-5 | Basic lead-in chains, occasional talent poaching |
| 6-8 | Adaptive counterprogramming, genre saturation exploitation |
| 9-12 | Multi-season planning, aggressive talent raids, meta-gaming DVR trends |

### 4.2 Event System

**Event Architecture:**

```
EventManager (Singleton)
├─ EventQueue (Priority queue: urgent events fire first)
├─ EventFactory (Generates events from triggers)
└─ EventHistoryLog (Tracks player choices for legacy scoring)
```

**Event Types:**

| Category | Examples | Trigger Conditions |
|---|---|---|
| **Talent** | Contract dispute, creative revolt, scandal | Loyalty thresholds, volatility rolls |
| **Industry** | Writers' strike, DVR milestone, genre trend | Season number, random rolls |
| **Competitive** | Rival poaches your star, rival show flops | Talent loyalty, rival AI actions |
| **Audience** | Fan campaign to save show, cult following forms | Ratings below cancellation line + high quality |
| **Financial** | Advertiser boycott, prestige CPM boost | Content rating conflicts, Emmy wins |

**Event JSON Structure:**

```json
{
    "eventID": "scandal_actor_01",
    "category": "Talent",
    "triggerCondition": {
        "actorVolatility": ">= 8",
        "randomChance": 0.10
    },
    "descriptionTemplate": "{actorName} was arrested for DUI. Tabloids are everywhere. What do you do?",
    "choices": [
        {
            "text": "Issue public support statement",
            "consequences": [
                { "type": "viewership", "modifier": 0.92, "duration": 2 },
                { "type": "advertiserConfidence", "delta": -10 }
            ]
        },
        {
            "text": "Fire the actor immediately",
            "consequences": [
                { "type": "showQuality", "delta": -10 },
                { "type": "recasting", "duration": 4 }
            ]
        },
        {
            "text": "Stay silent and let it blow over",
            "consequences": [
                { "type": "viewership", "modifier": 1.08, "duration": 1 },
                { "type": "viewership", "modifier": 0.95, "duration": 3 }
            ]
        }
    ]
}
```

Load all events from JSON at startup. Fire based on trigger conditions.

---

## 5. Save System Design

### 5.1 Save Data Structure

PREMIERE has complex state:
- 200+ show cards (active + cancelled + completed)
- 50+ talent entities with relationship history
- 3 rival network states
- 12 seasons x 35 weeks = 420 week records of ratings data
- Player's budget, network identity scores, Emmy history

**Save file format:** JSON (human-readable for debugging, moddable by power users)

**Save data hierarchy:**

```
SaveGame.json
├─ MetaData (version, timestamp, player name, season number)
├─ NetworkState
│   ├─ Budget (current allocations, historical profit/loss)
│   ├─ Identity (prestige, popularity, innovation, reliability, profitability scores)
│   └─ EmmyHistory (wins by year)
├─ Shows
│   ├─ ActiveShows (currently on air)
│   ├─ CancelledShows (historical data)
│   └─ CompletedShows (in syndication)
├─ Talent
│   ├─ Showrunners (stats, loyalty, history)
│   └─ Actors (stats, contracts, scandals)
├─ RivalNetworks
│   ├─ AmeriNet (schedule, budget, talent)
│   ├─ CrowneBroadcasting
│   └─ PacificTelevision
├─ EventHistory (player choices logged for legacy scoring)
└─ SimulationState (current week, season, era modifiers)
```

**Example JSON snippet:**

```json
{
    "metaData": {
        "version": "1.0.2",
        "timestamp": "2026-03-15T14:32:10Z",
        "playerName": "Executive_47",
        "currentSeason": 5,
        "currentWeek": 12
    },
    "networkState": {
        "budget": {
            "total": 185000000,
            "development": 38000000,
            "marketing": 30000000,
            "talent": 97000000,
            "operations": 20000000
        },
        "identity": {
            "prestige": 72,
            "popularity": 58,
            "innovation": 45,
            "reliability": 80,
            "profitability": 65
        }
    },
    "shows": [
        {
            "id": "show_00234",
            "title": "Badge: Special Crimes",
            "genre": "Procedural",
            "qualityRating": 78,
            "episodesAired": 42,
            "currentSlot": { "day": 3, "slot": 1 },
            "showrunnerID": "showrunner_00089",
            "cast": ["actor_00312", "actor_00445"],
            "ratingHistory": [8.2, 8.5, 8.1, 7.9, ...]
        }
    ],
    "talent": {
        "showrunners": [
            {
                "id": "showrunner_00089",
                "name": "Rebecca Stern",
                "talentLevel": 82,
                "ego": 65,
                "loyalty": 45,
                "emmyWins": 1,
                "showHistory": ["show_00234", "show_00107"]
            }
        ]
    }
}
```

### 5.2 Save/Load Implementation

**Saving:**

```csharp
public class SaveManager : MonoBehaviour
{
    public void SaveGame(string filename)
    {
        SaveData data = new SaveData();

        // Serialize all systems
        data.metaData = CollectMetaData();
        data.networkState = NetworkManager.Instance.Serialize();
        data.shows = ShowDatabase.Instance.SerializeAll();
        data.talent = TalentManager.Instance.Serialize();
        data.rivalNetworks = CompetitorManager.Instance.SerializeAll();
        data.eventHistory = EventManager.Instance.GetHistory();
        data.simulationState = SimulationController.Instance.Serialize();

        // Write to JSON
        string json = JsonConvert.SerializeObject(data, Formatting.Indented);
        string path = Path.Combine(Application.persistentDataPath, filename);
        File.WriteAllText(path, json);

        Debug.Log($"Game saved to {path}");
    }

    public void LoadGame(string filename)
    {
        string path = Path.Combine(Application.persistentDataPath, filename);

        if (!File.Exists(path))
        {
            Debug.LogError($"Save file not found: {path}");
            return;
        }

        string json = File.ReadAllText(path);
        SaveData data = JsonConvert.DeserializeObject<SaveData>(json);

        // Version check
        if (data.metaData.version != Application.version)
        {
            Debug.LogWarning("Save file version mismatch. Attempting migration...");
            data = MigrateSaveData(data);
        }

        // Deserialize all systems
        NetworkManager.Instance.Deserialize(data.networkState);
        ShowDatabase.Instance.DeserializeAll(data.shows);
        TalentManager.Instance.Deserialize(data.talent);
        CompetitorManager.Instance.DeserializeAll(data.rivalNetworks);
        EventManager.Instance.RestoreHistory(data.eventHistory);
        SimulationController.Instance.Deserialize(data.simulationState);

        Debug.Log($"Game loaded from {path}");
    }
}
```

**Autosave:**

Autosave at three points:
1. End of every week (quick autosave)
2. End of every season (full autosave)
3. Before major decisions (cancellation, talent negotiation)

Keep 3 rotating autosave slots to prevent corruption from killing all progress.

**Save file size estimate:**
- 200 shows x 2KB each = 400KB
- 50 talent x 1KB each = 50KB
- 420 weeks of ratings data x 0.5KB = 210KB
- Metadata + misc = 50KB

**Total: ~700KB per save file.** Completely reasonable. JSON compression (gzip) could cut this to ~200KB if needed, but unnecessary.

---

## 6. Performance Budget & Optimization Strategy

### 6.1 Target Hardware Specs

**Minimum Spec:**
- CPU: Intel i5-6500 / AMD Ryzen 3 1200 (4 cores, 2016-era)
- RAM: 4GB
- GPU: Integrated graphics (Intel HD 530 or better)
- Storage: 2GB

**Recommended Spec:**
- CPU: Intel i5-9400 / AMD Ryzen 5 2600
- RAM: 8GB
- GPU: Any discrete GPU (this is a 2D game)
- Storage: 2GB SSD

**Target Framerate:**
- 60 FPS rock-solid on recommended spec
- 30 FPS minimum on minimum spec
- No frame drops during card drag or stat recalculation

### 6.2 Performance Budget

| System | CPU Budget (ms/frame @ 60 FPS) | Notes |
|---|---|---|
| **Render** | 8ms | UI rendering, card sprites, text |
| **Simulation** | 2ms | Only during week simulation; zero during player interaction |
| **Input** | 1ms | Drag detection, click handling |
| **UI Updates** | 3ms | Stat recalculation, number ticker animations |
| **Audio** | 0.5ms | Music, UI sounds |
| **Overhead** | 2ms | GC, Unity engine overhead |
| **Total** | 16.5ms (60 FPS) | Target: 14ms to leave headroom |

**Critical path:** Card drag -> adjacency recalculation -> UI update must complete in under 5ms. This is the hot path. Profile it first.

### 6.3 Optimization Strategies

**1. Batch UI Updates**

Don't update every card's UI every frame. Use dirty flags:

```csharp
public class ShowCardUI : MonoBehaviour
{
    private bool isDirty = false;

    public void MarkDirty()
    {
        isDirty = true;
    }

    private void LateUpdate()
    {
        if (isDirty)
        {
            RefreshUI();
            isDirty = false;
        }
    }
}
```

Only cards affected by a placement are marked dirty. Unaffected cards don't update.

**2. Cache Competitor Schedules Per Frame**

Don't query rival networks 21 times per frame during adjacency calculation:

```csharp
private Dictionary<(int day, int slot), List<ShowData>> competitorCache;

private void OnBeginFrame()
{
    // Cache all competitor shows once per frame
    competitorCache = new Dictionary<(int day, int slot), List<ShowData>>();

    for (int day = 0; day < 7; day++)
    {
        for (int slot = 0; slot < 3; slot++)
        {
            competitorCache[(day, slot)] = GetCompetitorShows(day, slot);
        }
    }
}
```

**3. Object Pooling for UI Cards**

21 slots + bench area = ~30 card UI objects. Don't instantiate/destroy them. Pool them:

```csharp
public class CardPool : MonoBehaviour
{
    private Queue<ShowCardUI> pool = new Queue<ShowCardUI>();

    public ShowCardUI Get()
    {
        if (pool.Count > 0)
            return pool.Dequeue();
        else
            return Instantiate(cardPrefab);
    }

    public void Return(ShowCardUI card)
    {
        card.gameObject.SetActive(false);
        pool.Enqueue(card);
    }
}
```

**4. Simulation Optimization**

Week simulation (84 shows x 4 networks) must complete in under 200ms:

```csharp
// DON'T do this (slow):
foreach (var show in allShows)
{
    float viewership = SimulateViewership(show);
    // 84 iterations x 15ms each = 1260ms
}

// DO this (fast):
Parallel.ForEach(allShows, show =>
{
    show.viewership = SimulateViewership(show);
});
// 84 iterations parallelized across 4 cores = ~315ms / 4 = 79ms
```

Use Unity's Job System or C#'s `Parallel.ForEach` for simulation. Rating calculations are independent and parallelizable.

**5. Text Rendering Optimization**

TextMeshPro is fast, but 21 cards x 8 text fields = 168 text objects. Use:
- Texture atlases for consistent font rendering (one draw call per font)
- Disable "Extra Padding" in TMP settings (reduces memory)
- Use "Static" text fields for non-changing labels

**6. Memory Management**

Avoid GC spikes:
- Pre-allocate lists (`List<ShowData> results = new List<ShowData>(capacity: 21);`)
- Use `StringBuilder` for text concatenation
- Cache frequently-accessed components (`TMP_Text text = GetComponent<TMP_Text>();` in Start, not every frame)
- Avoid `LINQ` in hot paths (use `for` loops)

### 6.4 Profiling Plan

Profile these scenarios every milestone:

1. **Cold start:** New game load time (target: under 5 seconds)
2. **Card drag:** Drag one card across the grid, drop in new slot. FPS should never drop below 60.
3. **Full grid recalculation:** Change one card, all 21 slots recalculate. Target: under 5ms.
4. **Week simulation:** Simulate one week for all networks. Target: under 200ms.
5. **Season load:** Load a save game from Season 10 with 150 shows in history. Target: under 3 seconds.

Use Unity Profiler to identify bottlenecks. If any scenario exceeds budget, optimize that path before moving forward.

---

## 7. Platform Considerations

### 7.1 PC (Steam)

**Primary platform.** Optimize for mouse + keyboard.

**Input:**
- Mouse drag-and-drop for card placement
- Scroll wheel for zoom (if board gets crowded)
- Hotkeys: Spacebar (simulate week), Esc (cancel drag), 1-7 (jump to day), S (save), L (load)

**Resolution support:**
- Minimum: 1280x720
- Recommended: 1920x1080
- UI scales with resolution (anchored canvas, not fixed pixel positions)

**Steam features to integrate:**
- Steam Cloud saves (sync save files across devices)
- Steam Achievements (50+ achievements: "Win 10 Emmys", "Survive Writers' Strike", "Cancel a show with 10M viewers")
- Steam Workshop (future: moddable show templates, custom talent pools)
- Steam Deck verified badge (see below)

### 7.2 Steam Deck

**Secondary platform.** Must be fully playable without keyboard.

**Input mapping:**
- Left stick: cursor movement
- Right stick: scroll
- A button: select/confirm
- B button: cancel
- X button: open inbox
- Y button: simulate week
- L1/R1: cycle through cards
- Touchscreen: native drag-and-drop (best experience)

**Performance target:**
- 60 FPS at 800p (Steam Deck native resolution)
- Battery life: 4+ hours (this is not a demanding game)

**UI adjustments:**
- Card text must be readable at 7 inches (minimum font size: 14pt)
- Buttons must be at least 48x48 pixels (thumb-friendly)
- Larger hit zones for drag targets

**Testing:** Validate on Steam Deck before launch. Use Deck's built-in FPS overlay to confirm performance.

### 7.3 Console Ports (Future)

Not v1.0, but plan for it:

**Switch:**
- Touchscreen works in handheld mode
- Controller cursor in docked mode
- Larger UI fonts for TV play
- Performance target: 30 FPS stable

**PlayStation / Xbox:**
- Controller-only input (no touchscreen)
- D-pad for grid navigation
- Triggers for card selection
- Requires UX redesign for "pick up card without mouse"

**Technical barrier:** The drag-and-drop UI is mouse-native. Console port requires a "cursor mode" where the player moves a cursor with analog stick, then holds A to "grab" a card, then moves cursor to drop zone. Doable, but not trivial. Delay until PC version proves market fit.

---

## 8. Build Pipeline & Tools

### 8.1 Build Pipeline

**Version control:** Git + GitHub (or GitLab)

**Branch strategy:**
- `main`: Stable builds only (tagged releases)
- `develop`: Active development branch
- `feature/*`: Individual feature branches (merge into develop)

**Build automation:** Unity Cloud Build or GitHub Actions

**Build targets:**
- Windows 64-bit (primary)
- macOS (Intel + Apple Silicon)
- Linux (Ubuntu 20.04 LTS)
- Steam Deck (validated via SteamOS)

**Build frequency:**
- Nightly builds from `develop` (automated)
- Weekly playtesting builds (manual trigger)
- Release candidates tagged from `main`

**CI/CD Pipeline:**

```yaml
# .github/workflows/build.yml
name: Build PREMIERE

on:
  push:
    branches: [develop, main]
  pull_request:
    branches: [develop]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2

      - name: Cache Unity Library
        uses: actions/cache@v2
        with:
          path: Library
          key: Library-${{ hashFiles('Assets/**') }}

      - name: Build Windows
        uses: game-ci/unity-builder@v2
        with:
          targetPlatform: StandaloneWindows64

      - name: Build macOS
        uses: game-ci/unity-builder@v2
        with:
          targetPlatform: StandaloneOSX

      - name: Build Linux
        uses: game-ci/unity-builder@v2
        with:
          targetPlatform: StandaloneLinux64

      - name: Upload Artifacts
        uses: actions/upload-artifact@v2
        with:
          name: PREMIERE-Build
          path: build/
```

### 8.2 Developer Tools

**1. Show Template Editor (Custom Unity Window)**

A custom editor window for creating GenreTemplate ScriptableObjects:

```csharp
public class ShowTemplateEditor : EditorWindow
{
    [MenuItem("PREMIERE/Show Template Editor")]
    public static void ShowWindow()
    {
        GetWindow<ShowTemplateEditor>("Show Templates");
    }

    private void OnGUI()
    {
        // UI for editing genre templates
        // - Premise component dropdowns
        // - Stat range sliders
        // - Demo profile presets
        // - "Generate 10 Test Shows" button to validate template
    }
}
```

**2. Ratings Simulator (Testing Tool)**

A standalone tool to test the ratings engine without playing the game:

```csharp
public class RatingsSimulator : EditorWindow
{
    [MenuItem("PREMIERE/Ratings Simulator")]
    public static void ShowWindow()
    {
        GetWindow<RatingsSimulator>("Simulate Ratings");
    }

    private void OnGUI()
    {
        // Set up a test scenario:
        // - Drop down: select 4 shows
        // - Input fields: quality, star power, marketing
        // - Button: "Simulate 10 Weeks"
        // - Output: Line graph of viewership over time
    }
}
```

**3. Balance Spreadsheet Exporter**

Export all show stats to CSV for balance analysis in Excel/Google Sheets:

```csharp
[MenuItem("PREMIERE/Export Balance Data")]
public static void ExportBalanceData()
{
    StringBuilder csv = new StringBuilder();
    csv.AppendLine("ShowTitle,Genre,QualityRating,AudienceFloor,AudienceCeiling,CPE");

    var allShows = Resources.LoadAll<ShowData>("Shows");
    foreach (var show in allShows)
    {
        csv.AppendLine($"{show.showTitle},{show.genre},{show.qualityRating}," +
                       $"{show.audienceFloor},{show.audienceCeiling},{show.costPerEpisode}");
    }

    File.WriteAllText("balance_export.csv", csv.ToString());
    Debug.Log("Balance data exported to balance_export.csv");
}
```

**4. Event Debugger**

A window to manually trigger any event for testing:

```csharp
public class EventDebugger : EditorWindow
{
    [MenuItem("PREMIERE/Event Debugger")]
    public static void ShowWindow()
    {
        GetWindow<EventDebugger>("Event Debugger");
    }

    private void OnGUI()
    {
        // Dropdown: select event type
        // Button: "Fire Event"
        // Log: shows last 10 events fired with consequences
    }
}
```

### 8.3 Asset Pipeline

**Folder structure:**

```
Assets/
├── Scripts/
│   ├── Core/          (GameController, SaveManager)
│   ├── Systems/       (BoardSystem, RatingsEngine, TalentManager, etc.)
│   ├── Data/          (ShowData, GenreTemplate, SeasonCalendar)
│   ├── UI/            (ShowCardUI, BoardGridUI, InboxUI)
│   └── Utilities/     (Extensions, helpers)
├── Prefabs/
│   ├── UI/            (ShowCardPrefab, SlotPrefab, InboxItemPrefab)
│   └── Systems/       (Singleton manager prefabs)
├── Data/
│   ├── Shows/         (ShowData ScriptableObjects)
│   ├── Genres/        (GenreTemplate ScriptableObjects)
│   ├── Talent/        (ShowrunnerData, ActorData)
│   └── Events/        (Event JSON files)
├── UI/
│   ├── Sprites/       (Card backgrounds, icons, buttons)
│   ├── Fonts/         (TextMeshPro fonts)
│   └── Layouts/       (UI prefab variants for different resolutions)
└── Audio/
    ├── Music/         (Menu theme, gameplay theme, endgame theme)
    └── SFX/           (Card snap, ticker sound, phone ring, applause)
```

**Asset sources:**
- UI sprites: Custom art (flat, clean, 2000s corporate aesthetic)
- Icons: Font Awesome or custom (genre icons, stat indicators)
- Fonts: Google Fonts (Roboto for UI, Merriweather for headlines)
- Audio: Royalty-free from Epidemic Sound or custom composition

**Localization plan (future):**
All text stored in JSON:

```json
{
    "en": {
        "board_title": "The Board",
        "simulate_week": "Simulate Week",
        "cancel_show": "Cancel Show"
    },
    "de": {
        "board_title": "Die Tafel",
        "simulate_week": "Woche simulieren",
        "cancel_show": "Show abbrechen"
    }
}
```

Not v1.0, but plan for it. English-first for initial launch.

---

## 9. Technical Risk Assessment

### 9.1 High-Risk Areas

**RISK 1: UI Performance During Drag (Severity: Critical)**

**Problem:** Real-time adjacency recalculation while dragging a card could cause frame drops if not optimized.

**Mitigation:**
- Throttle recalculations to every 100ms during drag (not every frame)
- Use dirty flags to update only affected cards
- Profile on minimum spec hardware early (week 2 of development)
- If still slow: reduce precision of calculations during drag, full precision only on drop

**Fallback:** Disable live updates during drag; only recalculate on drop. Less satisfying, but functional.

**RISK 2: Procedural Show Generation Feels Repetitive (Severity: High)**

**Problem:** By Season 8, player has seen 300+ pilots. If generation feels formulaic, engagement drops.

**Mitigation:**
- Build 200+ premise templates with variable substitution (target: 1,000+ unique combinations)
- Implement "weird pilot" roll (10% of pool are genre mashups or oddball concepts)
- Track generated premises and bias against recent duplicates
- Playtest pilot generation in isolation: generate 500 pilots, have testers rate "how many felt samey"

**Fallback:** Supplement procedural generation with 50 hand-written "signature pilots" that appear rarely as high-quality standouts.

**RISK 3: Save File Corruption (Severity: High)**

**Problem:** Complex game state (200+ entities, 420 weeks of data) increases risk of save corruption.

**Mitigation:**
- Use JSON (human-readable, easier to debug than binary)
- Implement save file versioning and migration system
- Keep 3 rotating autosaves (so corruption doesn't wipe all progress)
- Write unit tests for serialization/deserialization of every major system
- Include "Repair Save File" utility that validates structure and fills missing data with defaults

**Fallback:** Cloud save backup via Steam Cloud. If local save corrupts, pull from cloud.

**RISK 4: Ratings Engine Balance Is Opaque (Severity: Medium)**

**Problem:** If the player can't understand WHY a show's ratings are what they are, the strategic layer collapses into guessing.

**Mitigation:**
- Show detailed breakdowns on hover: "Organic: 5.2M, Lead-In: +2.1M, Competition: -1.4M, Final: 5.9M"
- Provide a "Ratings Explainer" tooltip for every stat
- Build a testing tool (Ratings Simulator) to validate that outcomes match designer intent
- Playtest with spreadsheet players (the min-maxers) and ask: "Can you predict why this happened?"

**Fallback:** Add an optional "Advisor" NPC who explains ratings results in plain language ("Your show lost because AmeriNet's procedural crushed you in the 18-49 demo").

**RISK 5: Late-Game DVR Shift Feels Unfair (Severity: Medium)**

**Problem:** If DVR adoption guts live ratings and the player has no tools to adapt, Seasons 9-12 feel like punishment.

**Mitigation:**
- Introduce DVR metrics gradually (show them as secondary stats in Season 6, make them primary in Season 9)
- Unlock new strategies: serialized dramas get DVR bonuses, advertisers begin accepting Live+7 numbers
- Provide in-game "industry report" memos that explain the shift and suggest adaptations
- Playtest Seasons 8-10 specifically with players who haven't seen the early game

**Fallback:** Offer a "Short Career" mode (2000-2008) that ends before DVR dominates.

### 9.2 Medium-Risk Areas

**RISK 6: Competitor AI Feels Dumb (Severity: Medium)**

**Problem:** If rival networks make nonsensical decisions, competition feels hollow.

**Mitigation:**
- Give each rival a clear strategic personality (populist, prestige, disruptor)
- AI should make "believable mistakes" not "random mistakes" (e.g., over-investing in a fading genre)
- Playtest: show testers rival schedules without context. Can they describe the rival's strategy?

**Fallback:** Simplify AI to "clone player's successes + random noise." Boring, but functional.

**RISK 7: Event Fatigue (Severity: Medium)**

**Problem:** If the player is bombarded with talent events every week, inbox management becomes tedious.

**Mitigation:**
- Cap events at 3-5 per week max
- Prioritize events: urgent ones appear first, low-priority ones can be deferred
- Provide "Auto-Resolve" option for minor events (game picks the "safe" choice)

**Fallback:** Add event frequency slider in settings (Low/Medium/High).

### 9.3 Low-Risk Areas

**RISK 8: Steam Deck Performance (Severity: Low)**

**Problem:** UI-heavy game might struggle on Deck's limited hardware.

**Mitigation:**
- This is a 2D UI game with minimal rendering. Deck can handle it.
- Profile early on Deck hardware (or Deck emulation via SteamOS VM)
- Reduce texture resolution on Deck if needed (2K -> 1K sprites)

**Fallback:** Cap at 30 FPS on Deck (still playable for a turn-based sim).

**RISK 9: Console Port Viability (Severity: Low)**

**Problem:** Drag-and-drop UI doesn't translate to controller.

**Mitigation:**
- Not v1.0 scope. Solve this only if PC version succeeds.
- Prototype "cursor mode" where analog stick moves a cursor + A button to grab/drop cards

**Fallback:** PC/Steam Deck only. Console port is optional.

---

## 10. Development Milestones (Tech Perspective)

### Phase 1: Prototype (Months 1-3)

**Goal:** Prove the core loop feels good.

**Deliverables:**
- The Board UI (drag-and-drop with placeholder cards)
- Adjacency calculation system (lead-in bonuses visible in real-time)
- Basic ratings engine (simulate one week for player network only)
- 10 hand-written test shows (no procedural generation yet)

**Success criteria:**
- Playtester can schedule 10 shows across 7 nights
- Adjacency recalculation happens without frame drops
- Tester can explain why they placed a show in a specific slot

**Tech risks validated:**
- UI performance during drag
- Adjacency math is correct and readable

---

### Phase 2: Vertical Slice (Months 4-6)

**Goal:** One full season (September to May) is playable start to finish.

**Deliverables:**
- Full season loop (35 weeks with sweeps events)
- Week simulation (ratings reveal, events, player response phase)
- Pilot pipeline (procedural show generation, 25 pilots per season)
- Basic talent system (showrunners with loyalty tracking, no actors yet)
- Simple economy (revenue calculation, budget allocation)
- Save/load (full game state serialization)

**Success criteria:**
- Playtester completes one season (2-4 hours)
- Tester can describe their network's "identity" (prestige vs. populist)
- Tester wants to play a second season immediately

**Tech risks validated:**
- Procedural generation feels varied
- Save/load works reliably
- Week simulation completes in under 200ms

---

### Phase 3: Full Feature Set (Months 7-12)

**Goal:** All systems online. 12-season career playable.

**Deliverables:**
- All 5 core systems complete (Board, Ratings, Pipeline, Talent, Ledger)
- 3 rival networks with distinct AI strategies
- Full talent system (actors, contracts, scandals, poaching)
- Event system (50+ event types with player choices)
- Era progression (2000-2012 with industry shifts)
- UI polish (animations, transitions, sound design)
- Emmy ceremony and annual review cutscenes

**Success criteria:**
- Playtester completes 3+ seasons (6-12 hours)
- Tester identifies at least one "emergent story" (e.g., "I cancelled my favorite show because it was bleeding money")
- Competitor AI makes believable strategic decisions

**Tech risks validated:**
- AI doesn't feel dumb
- Late-game (Seasons 8-12) is engaging, not exhausting

---

### Phase 4: Content & Balance (Months 13-16)

**Goal:** Tune, balance, and content-fill.

**Deliverables:**
- 200+ show premise templates (across 24 genre/subgenre combos)
- 100+ talent personalities (showrunners + actors)
- 80+ event types (talent, industry, competitive, audience, financial)
- Balance pass on all economy numbers (CPM, CPE, margins)
- Full audio suite (music, SFX)
- Localization prep (extract all strings to JSON)

**Success criteria:**
- Playtester completes a full 12-season career (25+ hours)
- Tester rates replayability as high ("I want to try a different strategy")
- Zero game-breaking bugs in save/load or simulation

**Tech risks validated:**
- Show generation doesn't feel repetitive after 300+ pilots
- Balance is tuned (no dominant strategy)

---

### Phase 5: Polish & Shipping (Months 17-20)

**Goal:** Ship v1.0 to Steam.

**Deliverables:**
- Steam integration (Cloud saves, achievements, workshop prep)
- Steam Deck optimization (controller support, performance validation)
- Trailer, key art, store page
- Day-one patch readiness (hotfix pipeline)

**Success criteria:**
- Game runs at 60 FPS on recommended spec, 30 FPS on minimum spec
- Zero critical bugs in QA testing
- Store page has 5,000+ wishlists before launch

---

## 11. Team Structure & Roles

**Team size:** 4-6 people

| Role | Responsibilities | Skills |
|---|---|---|
| **Lead Programmer (1)** | Core systems architecture, ratings engine, save system, team coordination | C#, Unity, systems design, performance optimization |
| **Gameplay Programmer (2)** | Board system, pilot generation, talent web, event system | C#, Unity, data structures, AI scripting |
| **UI Programmer (1)** | UI Toolkit implementation, drag-and-drop, animations, responsive design | C#, Unity UI, UX design, DOTween |
| **Tools Programmer (1)** | Editor tools, balance exporters, testing utilities, build pipeline | C#, Unity Editor, CI/CD |
| **Systems Designer (1)** | Balance tuning, economy formulas, event authoring, playtesting coordination | Excel/Sheets, game balance, data entry |

**External contracts (not full-time):**
- **Audio Designer:** Music + SFX (contract work, ~2 months)
- **Visual Designer:** UI art, card templates, icons (contract work, ~3 months)
- **QA Tester Pool:** 10-20 testers for milestone playtests (volunteer + paid)

**Why this team size?**

PREMIERE is data-heavy, not content-heavy. We're not building 3D environments, animation systems, or networked multiplayer. We're building simulation systems, UI, and data pipelines. A small, focused team can ship this in 18-20 months.

Larger teams don't ship faster — they ship slower due to communication overhead. Keep the team lean.

---

## 12. Post-Launch Technical Roadmap

### 12.1 Patch 1.1 (Month 1 Post-Launch)

**Focus:** Bug fixes and balance tuning based on player feedback.

**Expected issues:**
- Balance: certain genres or strategies are over/under-powered
- Save corruption: edge cases we didn't catch in QA
- UI: minor usability issues (tooltips unclear, buttons too small on Deck)

**Plan:**
- Hotfix critical bugs within 48 hours
- Balance patch within 2 weeks (based on aggregate player data)
- Add optional "Advisor Mode" if players report confusion about ratings

### 12.2 Patch 1.2 (Month 3 Post-Launch)

**Focus:** Quality-of-life improvements.

**Features:**
- Fast-forward button (skip weeks with no player input)
- "Rewind to last season" option (if player regrets a decision)
- More granular stat breakdowns (on-hover tooltips)
- Additional achievements

### 12.3 DLC / Expansion Ideas (Month 6+)

**Only if base game succeeds. Do not build these until v1.0 ships and proves market fit.**

**Expansion 1: The Streaming Wars (2013-2020)**
- Extend timeline into the Netflix era
- New competitor: StreamFlix (no scheduling grid, releases full seasons at once)
- New mechanics: binge-watching metrics, international markets
- New event: talent exodus to streaming

**Expansion 2: Classic Era (1980s-1990s)**
- Prequel era with different rules (no DVR, different genres, 3-network oligopoly)
- New genre templates (family sitcoms, primetime soaps)
- Historical events (cable TV birth, Fox network launch)

**Mod Support (Steam Workshop):**
- Expose show templates, genre configs, event JSONs to players
- Players can create custom TV eras, genres, or talent pools
- Most successful mods get officially integrated

**Console Ports:**
- Switch, PlayStation, Xbox (only if PC version sells 50k+ units)
- Requires UX redesign for controller-based card selection

---

## 13. Conclusion: The Technical Thesis

PREMIERE is a management sim where the core challenge is not graphical fidelity or mechanical complexity — it's *information architecture*. The player needs to read a dozen stats at a glance, watch numbers ripple across interconnected systems, and feel like they're moving physical cards on a board.

The technology serves one goal: **make the strategic depth legible.**

**What this means in practice:**
- Unity gives us fast iteration on UI
- ScriptableObjects give us data-driven design (balance without recompiling)
- JSON saves give us human-readable state (debuggable, moddable)
- Parallel simulation gives us fast ratings calculation
- Event-driven architecture gives us decoupled systems (testable, maintainable)

**What this does NOT require:**
- Custom engine (Unity is faster)
- 3D rendering (delete it)
- Network code (N/A)
- GPT integration (too slow, too expensive, too unpredictable)
- Blockchain/NFT nonsense (absolutely not)

**The tech is simple. The data model is the complexity. The UI is the challenge.**

Ship the Board first. If dragging a card and watching numbers ripple doesn't feel satisfying, nothing else matters. Build that in week one. Test it in week two. If it works, build the rest of the game around it. If it doesn't, iterate until it does.

What's the loop? The loop is The Board.

Where's the tech risk? Real-time UI updates and procedural generation novelty.

How do we ship on time? Lean team, clear milestones, cut ruthlessly.

Let's build it.

-- BYTE
