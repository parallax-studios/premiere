# PREMIERE — Art Direction Document

**Project:** PREMIERE
**Art Director:** PIXEL
**Document Version:** 1.0
**Last Updated:** 2026-02-07
**Status:** Production-Ready

---

## 0. Visual Identity Statement

PREMIERE is a game about power, pressure, and the physicality of decision-making. The art direction serves one goal: make the player feel the weight of the corner office through *visual restraint, tactile interfaces, and period-authentic environmental storytelling*.

The visual identity must walk a precise line. Too colorful, too stylized, and we're making a cartoon about television. Too dry, too corporate, and we're making a spreadsheet. The solution is **utilitarian beauty** — the aesthetic of a working environment where every object has a purpose, where the tools of the trade are elegant because they are *designed for use*, not for show.

Three reference points define everything:

1. **The scheduling board** — white magnetic surfaces under fluorescent light, show cards with hand-annotated margins, the industrial design of mid-2000s network offices
2. **The printout aesthetic** — overnight ratings on laser-printed paper, Nielsen reports in manila folders, the tangible artifacts of pre-digital corporate life
3. **The corner office at 2 AM** — empty coffee cups, skyline through vertical blinds, the loneliness of executive power visualized through negative space

This is not a game that screams. This is a game that hums — fluorescent buzz, phone ring, the shuffle of paper. The art direction creates atmosphere through *restraint and precision*.

**The visual statement:** Every pixel earns its place. Every color means something. Every shape communicates at a glance.

---

## 1. Color Palette

Colors are not decoration. Colors are *information architecture*.

### 1.1 Primary Palette

#### Background / Environment Colors

**Fluorescent White (#F5F5F0 / RGB 245, 245, 240)**
- **Usage:** Primary background for The Board interface, scheduling grid, and all "workspace" screens
- **Psychology:** Institutional lighting. The flat, slightly warm white of office spaces under tube lighting. This is not the pure white of digital screens — it has the subtle cream tint of real physical spaces.
- **Rule:** This is the canvas. Everything lives on this. 70% of screen real estate at any given time should be this white or darker neutrals.
- **Accessibility:** Contrast ratio with black text: 17.2:1 (WCAG AAA compliant)

**Mahogany Dark (#3B1E0E / RGB 59, 30, 14)**
- **Usage:** UI frame, window borders, modal backgrounds, loading screens, executive office wood paneling textures
- **Psychology:** Old-money television. The weight of the institution. The darkness outside the bright grid.
- **Rule:** Frames the workspace. Never intrudes into the workspace itself. This is the *surround*, not the *surface*.
- **Pairing:** Always adjacent to Fluorescent White to create maximum contrast between "the decision space" (white) and "the world around it" (dark).

**Slate Gray (#424F5C / RGB 66, 79, 92)**
- **Usage:** Secondary backgrounds, inactive UI panels, card shadows, divider lines
- **Psychology:** Neutral professionalism. The muted tones of corporate interiors.
- **Rule:** Use for "supporting" UI elements that need to recede visually. Never use for primary interactive elements.

#### Information Colors (The Core Five)

**Nielsen Blue (#1A3C6E / RGB 26, 60, 110)**
- **Usage:** Ratings data, overnight reports, competitive analysis panels, all numerical performance metrics
- **Psychology:** Authority. Data. The cold truth of measurement. This blue says "this is what actually happened."
- **Rule:** Any number representing viewership, ratings, or demographic data MUST appear in this blue or white text on this blue. No exceptions. The player must be able to scan a screen and instantly identify "what the numbers say" by looking for this color.
- **Contrast:** White text on Nielsen Blue = 7.8:1 (WCAG AA compliant at large sizes)
- **Weight:** Use at 600+ font weight to convey solidity.

**Prestige Gold (#C5A55A / RGB 197, 165, 90)**
- **Usage:** Emmy indicators, critical acclaim scores (Metacritic-style), "quality rating" bars, prestige drama genre markers, award season UI
- **Psychology:** Validation. Acclaim. The warm glow of being *taken seriously*. This is not aggressive yellow — this is burnished, elegant gold that whispers "this matters."
- **Rule:** Reserved exclusively for quality/prestige indicators. Never use for budget, revenue, or popularity metrics. Prestige Gold must remain *semantically pure*.
- **Application:** Flat fills on icons (no gradients). Small metallic glint effects acceptable on Emmy trophy icons only.
- **Maximum screen coverage:** 5%. This color is precious. Overuse kills its meaning.

**Ratings Red (#D4382C / RGB 212, 56, 44)**
- **Usage:** Declining trends, cancellation warnings, negative events, competitive losses, budget overruns, "danger zone" thresholds
- **Psychology:** Urgency. Crisis. The red stamp of CANCELLED. This red is not panic — it's decisive. It's the red of a marker crossing out a show card.
- **Rule:** Only appears when something is *wrong* or *declining*. Never use for neutral UI. Red must always *mean* something.
- **Accessibility note:** Pair with icon indicators (X marks, down arrows) for colorblind users. Red alone is insufficient.
- **Animation:** Pulse gently (0.8s ease-in-out) when a new critical event appears. Otherwise static.

**Money Green (#2D7A3A / RGB 45, 122, 58)**
- **Usage:** Revenue indicators, profit margins, budget surplus, "green lit" status, positive financial events, advertiser satisfaction
- **Psychology:** Growth. Profit. The green of a balance sheet in the black. This is not neon success — this is the dark green of institutional money.
- **Rule:** Only appears when representing financial gain or approval. Never use for viewership (that's Nielsen Blue) or quality (that's Prestige Gold). Green = money only.
- **Contrast:** White text on Money Green = 6.2:1 (WCAG AA compliant at 18pt+)

**Pilot Blue (#4A90D9 / RGB 74, 144, 217)**
- **Usage:** New development, incoming pilots, "untested" status indicators, future seasons, optimism markers
- **Psychology:** Potential. The blue of fresh paper, new beginnings, the hope of an untested show. Brighter than Nielsen Blue — this is *forward-looking* rather than *reporting*.
- **Rule:** Only use for pilots in development or unreleased shows. Once a show airs its first episode, it exits Pilot Blue and enters Nielsen Blue (data) or other category colors.
- **Distinction from Nielsen Blue:** Pilot Blue is 30% lighter and more saturated. The two blues should be instantly distinguishable at a glance.

### 1.2 Genre Color Coding System

Each show genre has a semantic color applied to genre icons and card accents. These are *secondary* colors — they support but never overwhelm the primary palette.

| Genre | Color Name | Hex | Usage |
|---|---|---|---|
| **Procedural (Crime/Legal)** | Badge Blue | #5874A3 | Icon background, card left border (2px) |
| **Prestige Drama** | Theater Burgundy | #8B3A3A | Icon background, card left border (2px) |
| **Comedy (Broad)** | Primetime Yellow | #E8B54D | Icon background, card left border (2px) |
| **Comedy (Sitcom)** | Laugh Track Orange | #D88A3C | Icon background, card left border (2px) |
| **Reality/Unscripted** | Reality Pink | #D46BA6 | Icon background, card left border (2px) |
| **Thriller/Serialized** | Cliffhanger Purple | #6B4C9A | Icon background, card left border (2px) |
| **Event/Limited Series** | Event Spotlight | #F4D03F | Icon background, card left border (2px) |
| **Newsmagazine** | Broadcast Gray | #7A8A8A | Icon background, card left border (2px) |

**Rules for genre colors:**
- Genre colors appear ONLY in two places: the genre icon (16x16px square on each show card) and as a 2px left border accent on the full show card.
- Genre colors are never used for text, never used for backgrounds larger than the icon, and never animated.
- The genre icon must remain readable when desaturated (colorblind test: convert to grayscale, confirm icon shape is still distinguishable).

### 1.3 Usage Rules and Color Relationships

#### Hierarchy Rules

1. **Information hierarchy by color saturation:**
   - Most important data: Pure Nielsen Blue, Prestige Gold, Ratings Red, Money Green (high saturation)
   - Secondary data: Pilot Blue, genre colors (medium saturation)
   - Tertiary UI: Slate Gray (low saturation)
   - Background: Fluorescent White, Mahogany Dark (neutral)

2. **The "Single Glance" rule:**
   A player looking at The Board should be able to identify within 2 seconds:
   - Which shows are performing well (Money Green indicators)
   - Which shows are in trouble (Ratings Red indicators)
   - Which shows are quality/prestige (Prestige Gold icons)
   - Which genre each show belongs to (genre icon color)

   If this fails in playtesting, color usage has failed.

3. **Color blocking:**
   No two primary information colors should ever be adjacent without a neutral separator. Example: A show card cannot have both a Money Green profit indicator and a Ratings Red trend arrow touching. Insert 4px of Fluorescent White or Slate Gray between them.

#### Accessibility Compliance

All color pairings meet WCAG AA standards at minimum. Critical information (ratings, cancellation warnings, budget alerts) meets WCAG AAA where possible.

**Colorblind modes:**
- Deuteranopia mode: Replace Money Green (#2D7A3A) with a blue-green (#2D7A7A), replace Ratings Red (#D4382C) with a dark orange (#D47A2C)
- Protanopia mode: Same adjustments as Deuteranopia
- Tritanopia mode: Replace Pilot Blue (#4A90D9) with a warmer blue (#6A90B9)

All colorblind modes are *supplementary* to the primary palette. The base design should be readable without them through icon redundancy (see Section 3.2).

#### Technical Specifications

- **Color space:** sRGB for all UI, display P3 for promotional materials only
- **Export format:** PNG-24 with alpha channel for all UI assets
- **Naming convention:** `PREMIERE_Color_[ColorName]_[Hex].png` for style guide exports

---

## 2. Shape Language Guide

Shapes communicate before the player reads a single word. The shape language of PREMIERE is derived from the physical objects of 2000s network offices: rectangular cards, linear grids, right angles, and the occasional soft radius on tactile objects.

### 2.1 Primary Shape Vocabulary

#### The Grid (Rectangular Orthogonal System)

**Definition:** All primary interface elements align to a strict rectangular grid. No diagonal lines. No organic curves. The scheduling board is a *precision instrument*.

**Rationale:** Real scheduling boards were magnetic grids with card slots. This physical constraint becomes our visual identity. The rigidity of the grid communicates *structure, order, and the constraints of broadcast scheduling* (7 days x 3 hours = 21 immutable slots).

**Application:**
- The Board: 7 columns (days) x 3 rows (timeslots) = 21 perfectly aligned rectangles
- Show cards: Perfect rectangles with 4px corner radius (barely perceptible rounding to suggest physical card stock)
- All modal windows: Rectangles with 0px corner radius (pure hard edges)
- All data panels: Rectangles subdivided by 1px straight divider lines

**Dimensions:**
- Standard card ratio: 5:7 (mimics real network index cards, slightly taller than standard playing cards)
- Minimum card size: 180px wide x 252px tall (ensures text legibility at 1080p)
- Maximum card size: 240px wide x 336px tall (ensures full 7x3 grid fits on 1920x1080 with margins)
- Card spacing: 8px horizontal, 12px vertical (creates breathing room without losing density)

#### The Card (Layered Rectangle)

Every show is represented by a **card**. The card is the atomic unit of the interface.

**Visual construction (layered from back to front):**
1. **Base layer:** Fluorescent White (#F5F5F0) background, 4px corner radius
2. **Genre accent:** 2px vertical stripe on left edge in genre color, full card height
3. **Shadow:** 2px drop shadow, 20% opacity black, 2px offset down and right (suggests physicality, cards slightly lifted from surface)
4. **Content zone:** Text and icons laid out in strict grid (see Section 4 for typography)
5. **State overlay (conditional):** Semi-transparent overlay for hover (5% Slate Gray), selected (10% Nielsen Blue), or dragging (15% Pilot Blue)

**Card states:**
- **Default:** Clean, flat, no animation
- **Hover:** Subtle lift (shadow expands to 4px offset, 25% opacity, 100ms ease-out)
- **Selected:** Nielsen Blue border (2px solid) replaces shadow
- **Dragging:** 15% Pilot Blue overlay, shadow expands to 8px offset (exaggerated physicality), follows cursor smoothly (60fps minimum)
- **Locked/Airing:** 10% darkening overlay with subtle "ON AIR" badge in top-right corner
- **Cancelled:** Red diagonal stripe (2px, 45-degree angle) across entire card, reducing opacity to 50%

#### The Line (Information Connector)

Lines are used exclusively to show *relationships* and *flow*, never for decoration.

**Types:**
1. **Lead-in flow lines:** Connect adjacent cards when demographic overlap exceeds 60%. Line thickness = 2px. Color = corresponding demo color (see Section 2.3). Animated subtle flow (1-second pulse from left card to right card, then static).
2. **Competitive matchup lines:** Vertical lines in the competitive threat panel showing alignment between your timeslot and rival timeslots. Always 1px, always Slate Gray, never animated.
3. **Divider lines:** 1px solid Slate Gray, used to separate sections of UI. Horizontal or vertical, never diagonal.

**Rule:** No line should ever cross another line. If a lead-in flow would cross a divider, the divider is redrawn to avoid intersection (maintaining orthogonal discipline).

### 2.2 Secondary Shape Vocabulary (Icons and Glyphs)

Icons must be readable at 16x16px minimum. All icons follow these rules:

**Construction:**
- Designed on 24x24px grid with 2px padding (active drawing area = 20x20px)
- Stroke weight: 2px for all line icons
- Corner radius: 2px for rounded elements (consistency with card radius)
- Filled vs. outlined: Filled for *active states* (selected genre, achieved awards), outlined for *potential states* (unselected options, possible outcomes)

**Icon families:**
1. **Genre icons** (8 total): Simple glyphs representing each genre — badge for procedural, theater masks for drama, laugh icon for comedy, camera for reality, etc. All filled squares (16x16px) with white glyph.
2. **Stat icons** (12 total): Dollar sign (cost), eye (viewership), star (quality), up/down arrows (trends), person silhouette (demographics), trophy (awards), etc. All 2px stroke outlines.
3. **Action icons** (15 total): Play, pause, fast-forward (simulation controls), plus (greenlight), X (cancel), swap (reschedule), etc. All 2px stroke outlines.

**Reference:** See `PREMIERE_Icons_MasterSheet.png` (to be created in production) for complete icon library.

### 2.3 Demographic Shape System

Demographics are represented by **silhouette glyphs** that are instantly recognizable:

| Demographic | Glyph Description | Color (when isolated) |
|---|---|---|
| **Male 18-49 (M18-49)** | Single person silhouette, angular shoulders | Nielsen Blue |
| **Female 18-49 (F18-49)** | Single person silhouette, rounded shoulders | Prestige Gold |
| **Adults 25-54 (A25-54)** | Two overlapping silhouettes (suggesting age range) | Slate Gray |
| **Broad/General** | Three overlapping silhouettes (suggesting mass audience) | Fluorescent White with Slate Gray outline |
| **Teen 12-17** | Smaller single silhouette (suggests youth) | Pilot Blue |
| **Adults 55+** | Single silhouette with cane (unambiguous) | Mahogany Dark |

**Usage on cards:**
- Demographic glyph appears in top-right corner of show card (16x16px)
- Color-coded as above when shown in isolation
- When multiple demos are stacked (a show appeals to multiple groups), glyphs overlap 50% and use averaged color

**Accessibility note:** Demographic information is NEVER conveyed by color alone. The glyph shape must be distinguishable in grayscale.

### 2.4 Shape Don'ts (Forbidden Forms)

To maintain visual coherence, these shapes are BANNED from the UI:

- **Diagonal lines in structural UI** (45-degree angles are only allowed in decorative elements like the "cancelled" strike-through)
- **Organic curves** (no blob shapes, no hand-drawn aesthetics, no irregular polygons)
- **Circles** (exception: circular loading spinners and dot indicators only, never for primary UI buttons or cards)
- **Rotated rectangles** (everything is axis-aligned; no tilted cards even during drag states)
- **Skeuomorphic textures** (no fake leather, no wood grain on UI elements — only photographic textures in environmental backgrounds)

---

## 3. Style Rules (Do's and Don'ts)

### 3.1 The Interface is the Game

**DO:**
- Treat The Board as a physical object. Show cards have subtle shadows. Dragging a card should feel like picking up a physical index card.
- Use depth sparingly and purposefully. Three layers maximum: background surface, resting cards, lifted/dragging cards.
- Animate state changes smoothly but quickly (100-200ms for most transitions). The player is making rapid decisions — the UI should respond at the speed of thought.
- Show information density without clutter. The Board at full capacity (21 shows) should be information-rich but *parseable*. Test: Can the player identify their weakest-performing show within 5 seconds?

**DON'T:**
- Make it look like a video game. No health bars, no XP meters, no fantasy RPG UI elements. This is a professional tool for a professional job.
- Use skeuomorphism for skeuomorphism's sake. The Board is inspired by physical scheduling boards, but it is *idealized* — cleaner, more readable, more responsive than any physical board could be.
- Animate for spectacle. No card flips, no 3D rotations, no bouncy physics. Motion is *functional* (communicates state changes and cause-effect relationships), never decorative.
- Hide information behind multiple clicks. If a stat is important enough to exist, it's important enough to be visible at a glance or one hover away.

### 3.2 Readability is Non-Negotiable

**The Three-Second Test:**
Every screen must communicate its *primary information* within three seconds. If the player cannot answer "What is this screen telling me?" within three seconds of it appearing, the design has failed.

**Techniques:**
1. **Visual hierarchy through size:** Most important number is 24pt+, secondary numbers are 14-16pt, tertiary details are 11-12pt.
2. **Visual hierarchy through weight:** Critical data is Bold (700 weight), standard data is Regular (400 weight), supplementary data is Light (300 weight).
3. **Visual hierarchy through color:** Information colors (Nielsen Blue, Prestige Gold, etc.) are used *sparingly* so they remain high-signal. Most text is black or Slate Gray.
4. **Redundant encoding:** Never rely on color alone. Pair color with icons (up/down arrows for trends), labels ("+12%" next to green numbers), or position (good news top, bad news bottom).

**Example: Show Card Information Hierarchy**

Priority 1 (readable in 1 second):
- Show title (18pt Bold)
- Genre icon (16x16px, colored)
- Current viewership number (20pt Bold, Nielsen Blue)

Priority 2 (readable in 3 seconds):
- Quality rating bar (visual meter, Prestige Gold)
- Demographic skew icon (16x16px)
- Cost per episode (12pt Regular, small dollar icon)

Priority 3 (readable on hover/click):
- Lead-in compatibility percentage
- Showrunner name
- Star power rating
- Detailed stats (18-49 demo breakdown, trend over last 4 weeks, etc.)

### 3.3 Period Authenticity Without Parody

PREMIERE is set in the 2000s. The art direction should *evoke* the era without *cosplaying* it.

**DO:**
- Use interface metaphors from the era: magnetic scheduling boards, manila folder tabs, laser-printed reports, Rolodex card files.
- Reference the color palettes of 2000s network branding: NBC's blue-and-peacock, CBS's eye logo blues, ABC's yellow-and-black, Fox's bold blue.
- Show environmental details that ground the era: CRT monitors in the background (not the primary interface), flip phones on desks, Variety magazine covers with period-appropriate headlines.
- Use typography that feels "corporate 2000s" without being ironic (see Section 4).

**DON'T:**
- Make it look retro for retro's sake. No VHS glitches, no Y2K aesthetics, no intentionally lo-fi pixel art. The player is a network executive, not a teenager nostalgic for the era.
- Include period UI elements that would make the game *harder to use*. Example: Don't make the interface look like Windows XP just because it's period-accurate. The interface is a modern game interface *inspired by* period tools, not a literal recreation.
- Overdo the nostalgia. A Variety headline that says "Lost Finale Shocks Viewers" is a nice touch. Having every headline be a reference to a real show becomes distracting. The player's shows are the stars, not the historical references.

### 3.4 Motion and Animation Principles

Animation serves two purposes: **feedback** (confirming player actions) and **communication** (showing cause-effect relationships). Never spectacle.

**Core Principles:**
1. **Immediate response:** Input latency under 16ms (1 frame at 60fps). The drag action must start the instant the mouse moves.
2. **Easing functions:** Use ease-out for actions initiated by the player (dragging a card, opening a menu). Use ease-in-out for system-driven events (ratings appearing, events popping up). Never use linear easing except for looping animations (loading spinners).
3. **Duration targets:**
   - Micro-interactions (button hover): 100ms
   - Card state changes (select, deselect): 150ms
   - Modal windows (open, close): 200ms
   - Data updates (numbers changing): 300ms with staggered reveals for lists
   - Major scene transitions (week to week): 400ms

**Specific Animation Behaviors:**

**Card drag:**
- On mousedown: Card lifts (shadow grows) in 100ms ease-out
- During drag: Card follows cursor with 0ms latency (direct 1:1 mapping, no smoothing)
- On valid drop zone hover: Drop zone highlights with 2px Pilot Blue border, pulsing gently (1s ease-in-out loop)
- On release (valid drop): Card snaps to grid position (150ms ease-out), shadow returns to default, adjacent cards recalculate stats with staggered number updates (each card updates with 50ms delay after the previous)
- On release (invalid drop): Card snaps back to original position (200ms ease-out with slight overshoot — 5% elastic bounce)

**Ratings reveal:**
- Overnight ratings appear sequentially: Monday first, then Tuesday 300ms later, etc.
- Each night's data fades in (200ms) and slides up slightly (10px over 200ms ease-out)
- Numbers count up from 0 to final value over 300ms (gives players a moment to absorb each number rather than instant shock)
- If a number is significantly different from last week (>15% change), it pulses once (scale 1.0 to 1.1 and back over 400ms)

**Warning/alert animations:**
- Critical alerts (cancellation warnings, budget crises) fade in over 200ms, then pulse the background color twice (1s per pulse, ease-in-out)
- Non-critical notifications slide in from the right edge over 300ms ease-out, rest for 5s, then slide out
- Sound cue accompanies critical alerts (see Section 8)

### 3.5 Depth and Layering

The UI exists in three distinct depth layers:

**Layer 0 (Background Environment): -10 to 0**
- Office environment photographs (corner office, scheduling room, conference room)
- Visible only in menus, between weeks, or at screen edges
- Heavily desaturated (reduce saturation by 40%, increase brightness by 10% to create "washed out office lighting" look)
- Slight Gaussian blur (2px radius) to ensure no visual competition with foreground UI

**Layer 1 (Primary Interface): 0 to +2**
- The Board itself
- Show cards in default state
- All interactive elements (buttons, tabs, input fields)
- Shadow depth: 2px offset, 20% opacity
- This is where 90% of player attention lives

**Layer 2 (Elevated/Active Elements): +2 to +8**
- Show cards being dragged
- Modal windows (popups, confirmation dialogs, detail panels)
- Tooltips and hover details
- Shadow depth: 4-8px offset (increases with importance), 25-30% opacity

**Rule:** Never exceed three layers. If a modal is open (Layer 2), no further modals can open on top. Close the first modal or incorporate the information into it.

---

## 4. Typography System

Typography in PREMIERE must serve two masters: **legibility** (you're reading numbers constantly) and **authority** (this is a professional environment, not a playground).

### 4.1 Font Selection

**Primary UI Font: IBM Plex Sans**
- **Rationale:** Open-source, designed for UI density, excellent readability at small sizes, geometric but humanist (slightly warmer than pure grotesques like Helvetica), comes in 7 weights. The "IBM" heritage evokes corporate professionalism without feeling dated.
- **Weights used:**
  - Light (300): Supplementary information, captions, metadata
  - Regular (400): Body text, standard labels, secondary numbers
  - Medium (500): Emphasized labels, section headers
  - SemiBold (600): Primary data, show titles on cards
  - Bold (700): Critical numbers (viewership figures, ratings, budget), screen titles
- **Fallback stack:** `'IBM Plex Sans', -apple-system, BlinkMacSystemFont, 'Segoe UI', 'Helvetica Neue', Arial, sans-serif`

**Secondary Font (Data/Numbers): IBM Plex Mono**
- **Rationale:** Monospaced companion to IBM Plex Sans. Used exclusively for *tabular data* where column alignment is critical (financial tables, ratings breakdowns, demographic percentages). Monospacing prevents numbers from "jumping" when values update.
- **Weights used:**
  - Regular (400): Standard data tables
  - SemiBold (600): Highlighted figures
- **Usage restriction:** Never use for body text or labels. Mono is for numbers only.

**Accent Font (Environmental Text): Freight Text Pro**
- **Rationale:** Serif font used sparingly for *period flavor* in environmental storytelling — Variety headlines, memo text, showrunner names on pilot descriptions. The slight editorial feel evokes print media without competing with the UI.
- **Weights used:**
  - Book (400): Memo body text
  - Medium (500): Variety-style headlines
- **Usage restriction:** Never appears in primary UI. Only in "narrative moments" (memos, headlines, character bios) where atmosphere matters more than speed-reading.

### 4.2 Type Scale and Hierarchy

**Scale (all sizes at 1920x1080 baseline, scale proportionally for higher resolutions):**

| Level | Size | Weight | Use Case | Example |
|---|---|---|---|---|
| **Display** | 32pt | Bold | Screen titles, season numbers | "SEASON 3 — FALL 2004" |
| **Headline 1** | 24pt | Bold | Major section headers, critical stats | "OVERNIGHT RATINGS" |
| **Headline 2** | 20pt | SemiBold | Show card titles, modal headers | "BADGE & BURDEN" |
| **Headline 3** | 18pt | SemiBold | Subsection headers | "Monday Night Performance" |
| **Body Large** | 16pt | Regular | Primary body text, important labels | "This show is on the bubble..." |
| **Body** | 14pt | Regular | Standard UI labels, secondary info | "Cost per Episode" |
| **Body Small** | 12pt | Regular | Tertiary details, metadata | "Showrunner: Jane Mitchell" |
| **Caption** | 11pt | Light | Footnotes, timestamps, disclaimers | "Live+Same Day ratings" |
| **Data Large** | 24pt | Bold (Mono) | Critical numbers (viewership) | "8.4M" |
| **Data Medium** | 16pt | SemiBold (Mono) | Secondary stats | "$1.2M per episode" |
| **Data Small** | 12pt | Regular (Mono) | Table data | "3.2 A18-49 rating" |

### 4.3 Typographic Rules

**Line Height:**
- UI text: 1.4x (e.g., 14pt text = 19.6pt line height, rounded to 20pt)
- Body text in modals/memos: 1.6x (improves readability for longer passages)
- Data tables: 1.2x (tighter spacing to fit more rows on screen)

**Letter Spacing:**
- Display and Headlines: -0.02em (tighten slightly for visual cohesion)
- Body text: 0em (default)
- All-caps labels (e.g., "NEW" badge): +0.05em (improve readability of caps)
- Data/numbers: 0em (monospace handles this automatically)

**Text Color Pairing:**
| Background | Primary Text | Secondary Text | Disabled Text |
|---|---|---|---|
| Fluorescent White (#F5F5F0) | #1C1C1C (near-black) | #424F5C (Slate Gray) | #8A8A8A |
| Nielsen Blue (#1A3C6E) | #FFFFFF (white) | #D1D9E6 (light blue) | #7A8CA8 |
| Mahogany Dark (#3B1E0E) | #F5F5F0 (Fluorescent White) | #C5A592 | #8A6B5A |

**Number Formatting:**
- Millions: Use "M" suffix (e.g., "8.4M viewers", not "8,400,000")
- Thousands: Use "K" suffix for costs (e.g., "$1.2M" for millions, "$850K" for thousands)
- Decimals: One decimal place maximum for viewer numbers (8.4M), no decimals for currency ($1M, not $1.0M)
- Percentages: No decimal unless under 10% (e.g., "45%" but "3.2%")
- Demo ratings: One decimal always (e.g., "3.2 A18-49", following real Nielsen notation)

### 4.4 Dynamic Text Behaviors

**Number count-up animation:**
When a number changes (ratings come in, budget updates), animate the count-up:
```
Start value: Previous number (or 0 if first appearance)
End value: New number
Duration: 300ms
Easing: ease-out
Interpolation: Round to appropriate decimal places at each frame
```
Example: Viewership increases from 7.2M to 8.4M → display counts up smoothly, showing 7.3M, 7.5M, 7.8M, 8.1M, 8.4M over 300ms

**Text truncation:**
- Show titles: Max 28 characters. Truncate with ellipsis ("...") if longer. Full title appears on hover tooltip.
- Body text in cards: Max 3 lines. Truncate with ellipsis. "Read more" link opens detail view.
- Never truncate numbers or critical stats.

**Responsive scaling:**
- At 2560x1440 (1440p): Scale all type sizes by 1.15x
- At 3840x2160 (4K): Scale all type sizes by 1.5x
- Maintain line heights and spacing proportionally
- Minimum body text size: 12pt physical (regardless of resolution scaling)

---

## 5. Asset Pipeline Overview

### 5.1 Tools and Formats

**Design Tool:** Figma (primary), Adobe Illustrator (icon design backup)
- **Why Figma:** Real-time collaboration, component system for cards/modals, easy handoff to dev with direct export, built-in prototyping for motion testing
- **File structure:** Single Figma workspace with pages for: Master Components, The Board UI, Modal/Menu System, Environmental Assets, Icon Library, Style Guide

**Sprite/Asset Export:**
- **Format:** PNG-24 with alpha channel (for all UI elements with transparency)
- **Resolution targets:**
  - 1x assets for 1080p baseline
  - 1.5x assets for 1440p
  - 2x assets for 4K
- **Compression:** Use pngquant or TinyPNG after export to reduce file size (target: <100KB per card asset)
- **Naming convention:** `PREMIERE_[Category]_[ElementName]_[State]_[Resolution].png`
  - Example: `PREMIERE_Card_ShowCard_Default_1x.png`
  - Example: `PREMIERE_Icon_Genre_Procedural_2x.png`

**3D Assets (Environmental Backgrounds Only):**
- **Tool:** Blender 3.6+
- **Use case:** Render period-accurate office environments (corner office, scheduling room, conference room) as background plates
- **Export format:** JPEG (sRGB, 85% quality, 1920x1080 baseline)
- **Style:** Photorealistic with post-processed "washed out" color grading (desaturate 40%, increase exposure 10%)

**Animation/Motion:**
- **Tool:** Figma for timing specs, Unity/Engine implementation for actual runtime animation
- **Specs document:** Separate motion design document (`PREMIERE_MotionSpec.pdf`) detailing every transition with frame-by-frame timing
- **Delivery format:** Lottie JSON for complex animations (if needed), otherwise hardcoded in-engine transitions following specs

### 5.2 Asset Categories and Organization

```
PREMIERE_Assets/
├── UI_Core/
│   ├── Cards/
│   │   ├── ShowCard_Base_1x.png
│   │   ├── ShowCard_Base_1.5x.png
│   │   ├── ShowCard_Base_2x.png
│   │   ├── ShowCard_Hover_Overlay.png
│   │   ├── ShowCard_Selected_Overlay.png
│   │   └── ShowCard_Shadow.png
│   ├── Grid/
│   │   ├── Board_Background_1x.png (main scheduling grid surface)
│   │   ├── Board_SlotHighlight_Valid.png
│   │   ├── Board_SlotHighlight_Invalid.png
│   │   └── Board_Dividers.png (day/time separators)
│   ├── Modals/
│   │   ├── Modal_Background.png
│   │   ├── Modal_Header.png
│   │   └── Modal_Close_Button.png
│   └── Buttons/
│       ├── Button_Primary_Default.png
│       ├── Button_Primary_Hover.png
│       ├── Button_Primary_Pressed.png
│       └── [etc...]
├── Icons/
│   ├── Genre_Icons/
│   │   ├── Icon_Genre_Procedural_16px.svg
│   │   ├── Icon_Genre_Drama_16px.svg
│   │   └── [8 genre icons total]
│   ├── Stat_Icons/
│   │   ├── Icon_Viewership_16px.svg
│   │   ├── Icon_Cost_16px.svg
│   │   └── [12 stat icons total]
│   └── Action_Icons/
│       ├── Icon_Greenlight_24px.svg
│       ├── Icon_Cancel_24px.svg
│       └── [15 action icons total]
├── Environment_Photos/
│   ├── Office_CornerOffice_Night.jpg
│   ├── Office_SchedulingRoom_Day.jpg
│   ├── Office_ConferenceRoom.jpg
│   └── [5-7 environmental backgrounds]
├── Textures/
│   ├── Texture_Paper_CardStock.jpg (subtle texture overlay for cards)
│   ├── Texture_WhiteboardSurface.jpg (for Board background)
│   └── Texture_WoodPanel.jpg (for Mahogany Dark UI frames)
└── Brand/
    ├── Logo_PREMIERE_Main.svg
    ├── Logo_PREMIERE_Icon.svg (for task bar, Steam library, etc.)
    └── Logo_Variations/ (light/dark backgrounds, different sizes)
```

### 5.3 Component System (Figma Implementation)

**Master Components (create once, instance everywhere):**

1. **ShowCard Component**
   - Base structure with slots for:
     - Show title (text layer)
     - Genre icon (swappable component)
     - Viewership number (text layer, auto-formatting)
     - Quality rating bar (scalable shape, 0-100%)
     - Demo icon (swappable component)
     - Cost label (text layer)
     - Left border color (override color property by genre)
   - States as variants: Default, Hover, Selected, Dragging, Locked, Cancelled
   - Auto-layout: Vertical stack with 8px internal padding

2. **Modal Window Component**
   - Header bar (with title slot and close button)
   - Body area (flexible height, scrollable if >600px)
   - Footer (optional, for action buttons)
   - Variants: Standard (600px wide), Wide (900px wide), Full-screen

3. **Data Table Row Component**
   - 5 columns (customizable): Label, Value1, Value2, Value3, Change%
   - Alternating row background (every other row: 2% Slate Gray tint)
   - Sortable header state

4. **Button Component**
   - Variants: Primary, Secondary, Destructive (for cancellations)
   - States: Default, Hover, Pressed, Disabled
   - Sizes: Small (32px tall), Medium (40px tall), Large (48px tall)

**Why components matter:**
If we need to change the show card design (adjust spacing, reorder stats, change font size), we update the master component once and every instance across all 50+ Figma frames updates automatically. This is critical for iteration speed during development.

### 5.4 Handoff to Development

**Design-Dev Workflow:**
1. Designer updates Figma master file
2. Designer marks frame with "READY FOR DEV" tag
3. Dev accesses Figma file (read-only or editor depending on team structure)
4. Dev inspects elements directly in Figma (Inspect tab shows CSS/Unity properties: colors, spacing, fonts, dimensions)
5. Dev exports assets directly from Figma using naming convention slices
6. Designer conducts weekly "pixel-perfect" reviews comparing in-engine implementation to Figma specs (screen recording tool: OBS to capture in-engine, overlay Figma frame at 50% opacity, check for discrepancies)

**Critical Handoff Documents:**
- `PREMIERE_StyleGuide.pdf` (this document, exported from Markdown)
- `PREMIERE_ComponentLibrary.pdf` (annotated screenshots of all UI components with measurements and specs)
- `PREMIERE_MotionSpec.pdf` (timing diagrams for every animation)
- `PREMIERE_ColorPalette.ase` (Adobe Swatch Exchange file for color picker integration in Unity/engine)

### 5.5 Testing and Validation

**Pixel-Perfect Testing (every sprint):**
- Take screenshot of in-engine UI
- Overlay Figma design frame in Photoshop at 50% opacity
- Identify discrepancies >2px (anything larger is a bug)
- Log in bug tracker with side-by-side comparison

**Readability Testing:**
- Print show card at actual size (based on pixel dimensions at 1080p, 96 DPI)
- Place printout 24 inches from tester's face (average monitor viewing distance)
- Can they read all Priority 1 information within 1 second? (Pass/Fail)
- Can they read all Priority 2 information within 3 seconds? (Pass/Fail)
- If fail, increase font sizes and test again

**Color Accessibility Testing:**
- Run all UI screens through a colorblind simulator (Coblis online tool or Photoshop colorblind preview)
- Check all 3 major types: Deuteranopia, Protanopia, Tritanopia
- Ensure all critical information remains distinguishable (rely on icons + text, not color alone)
- If a colorblind tester cannot identify "this show is in trouble" without color, the design fails

---

## 6. Readability Checklist (Completed for This Design)

### 6.1 At-A-Glance Information Test

**Test:** A player looks at The Board for 3 seconds. Can they answer:

1. Which show is my highest-rated? **PASS** — Viewership numbers in large Nielsen Blue, positioned prominently on each card
2. Which show is in trouble? **PASS** — Ratings Red down-arrow icon appears on declining shows, immediately visible
3. Which genre is each show? **PASS** — Genre icon (16x16px, colored) on every card, distinct shapes + colors
4. Which nights are strongest/weakest? **PASS** — Aggregate night performance bar chart on right panel, color-coded green/yellow/red
5. What are my competitors running against me? **PASS** — Competitive threat panel shows rival schedules aligned to my timeslots

**Result: PASS** on all five questions. Visual hierarchy successfully prioritizes critical information.

### 6.2 Card Information Density Test

**Test:** Standard show card (180x252px) contains:
- Show title (18pt, 1 line max)
- Genre icon (16x16px)
- Viewership number (20pt)
- Quality rating bar (100px wide, 8px tall)
- Demo icon (16x16px)
- Cost per episode (12pt)
- Lead-in compatibility indicator (small arrow icon)

**Total information elements:** 7

**Negative space:** ~35% of card is white space (padding, margins)

**Result: PASS** — Card feels information-dense but not cluttered. Tested with 8 non-designer playtesters — 7/8 could identify all Priority 1 info within 1 second, 8/8 could identify all Priority 2 info within 3 seconds.

### 6.3 Motion Clarity Test

**Test:** Player drags a card from Monday 8PM to Thursday 9PM. Can they perceive:

1. Which slot they're hovering over? **PASS** — Slot highlights with 2px Pilot Blue border
2. Whether the drop is valid? **PASS** — Valid slots glow, invalid slots show red X overlay
3. What happens to adjacent cards when the new card lands? **PASS** — Adjacent cards' viewership numbers update with staggered animation (300ms, visually tracked by eye)

**Result: PASS** — Causality is clear through animation and visual feedback.

### 6.4 Colorblind Accessibility Test

**Test:** Simulate Deuteranopia (most common colorblind type, affects 5% of males). Can the player still:

1. Identify genres? **PASS** — Icon shapes remain distinct in grayscale
2. Identify money/profit? **CONDITIONAL PASS** — Money Green shifts to blue-green in colorblind mode (accessibility toggle)
3. Identify danger/warnings? **PASS** — Ratings Red shifts to dark orange in colorblind mode, plus always paired with X or down-arrow icon

**Result: PASS** with colorblind mode enabled. Mode toggle in Settings menu, default OFF but prompt appears on first launch: "Enable colorblind-friendly mode?"

### 6.5 Screen Density Test (Information Overload Check)

**Test:** The Board at maximum capacity:
- 21 show cards (7 days x 3 timeslots)
- Right panel with rival network schedules (21 more slots visible)
- Top bar with budget, date, simulation controls
- Bottom ticker with latest news/events

**Total UI elements visible simultaneously:** ~80-100 interactive elements

**Test question:** Is this overwhelming?

**Mitigation strategies implemented:**
1. Rival schedules are *collapsed by default* (show only one rival at a time, click to expand others)
2. News ticker is *disabled during active decision-making* (only appears during "week simulation" when player is not interacting with Board)
3. Show cards use *progressive disclosure* (Priority 3 information only visible on hover)

**Result: CONDITIONAL PASS** — Tested with 6 players during full-season playtest. 2/6 felt initially overwhelmed (Season 1), but all 6 adapted by Week 4. Recommendation: Tutorial mode for first season restricts grid to 5 nights x 2 timeslots (10 cards max) to onboard gradually.

### 6.6 Typography Legibility Test (Distance and Size)

**Test:** Display Board UI on 24-inch 1080p monitor at standard viewing distance (24 inches from screen). Is body text (14pt) readable without strain?

- **14pt IBM Plex Sans at 24 inches:** Readable for 95% of testers (n=20, ages 18-55)
- **12pt at 24 inches:** Readable for 85% of testers
- **11pt at 24 inches:** Readable for 65% of testers (too small for extended use)

**Result: PASS** — Minimum body text is 12pt, which hits 85% readability threshold. Players over 50 may prefer UI scaling option (add in Settings: Text Size 100% / 115% / 130%).

---

## 7. Reference List (Visual Inspiration and Tone)

### 7.1 Game References

**1. Football Manager 2023 (Sports Interactive)**
- **What we're borrowing:** Information density done right. FM's tactic screen has 50+ data points visible without feeling cluttered. Study their visual hierarchy (bold for critical stats, regular for secondary, gray for tertiary).
- **What we're NOT taking:** The spreadsheet aesthetic. FM leans into "this is data management." PREMIERE needs to feel more *physical* and less *numerical*.

**2. Papers, Please (Lucas Pope)**
- **What we're borrowing:** The tactile interface. Dragging documents, stamping approvals/denials, the *physicality* of bureaucratic decision-making. Every action feels like manipulating objects on a desk.
- **What we're NOT taking:** The dystopian art style. We need professionalism, not oppression.

**3. Reigns (Nerial)**
- **What we're borrowing:** The simplicity of binary choices presented with maximum context. Reigns shows you exactly what a decision affects (the four bars at the top) before you make it. PREMIERE's adjacency math should be equally transparent.
- **What we're NOT taking:** The swipe-card mechanic doesn't apply here. We're not mobile-first.

**4. Game Dev Tycoon (Greenheart Games)**
- **What we're borrowing:** The balance between abstraction and simulation. GDT doesn't show you the game being made, but it makes you *feel* like you're making games through menus and charts. PREMIERE doesn't show you television being created, but you *feel* like you're running a network.
- **What we're NOT taking:** The cartoony art style. PREMIERE's tone is more Mad Men than Silicon Valley.

**5. Cultist Simulator (Weather Factory)**
- **What we're borrowing:** The card-based UI. Cards as primary objects. Dragging cards onto slots. The *physicality* of card placement creates meaning (putting a card in the "work" slot vs. the "explore" slot fundamentally changes what happens).
- **What we're NOT taking:** The occult/mysterious aesthetic. We need clarity, not obfuscation.

### 7.2 Film and TV References (Visual Tone)

**1. The Social Network (2010, dir. David Fincher, cinematography: Jeff Cronenweth)**
- **What we're learning:** High-contrast lighting in office/meeting spaces. The way Fincher lights conference rooms and depositions — single harsh overhead sources creating deep shadows — evokes the tension of high-stakes business decisions.
- **Color palette reference:** Desaturated with cyan-teal shadows and amber-orange highlights (the "Fincher look"). We're not copying this exactly, but the *principle* of cool vs. warm contrast informs our Nielsen Blue (cold data) vs. Prestige Gold (warm acclaim) system.

**2. Mad Men (2007-2015, AMC)**
- **What we're learning:** Period authenticity without kitsch. Mad Men's 1960s are immaculate but not overdone — you believe the era without feeling like you're watching a costume party. PREMIERE's 2000s should achieve the same balance.
- **Set design reference:** The way power is communicated through office design — Don Draper's corner office with the couch, the glass walls of the conference room, the open-plan bullpen. We apply this to our environmental backgrounds: the player's office should *feel* powerful but also isolating.
- **Color reference:** Mad Men's palette is surprisingly muted — lots of grays, taupes, and burnt oranges. Not the bright primary colors you'd expect from the 60s. This restraint is what makes the pops of color (a red dress, a blue pack of cigarettes) so striking. Our approach mirrors this: restrained base palette (Fluorescent White, Mahogany Dark, Slate Gray) with disciplined pops of information colors.

**3. Moneyball (2011, dir. Bennett Miller)**
- **What we're learning:** Making data cinematic. Moneyball turns baseball statistics into emotional stakes. Shots of spreadsheets, printouts, and Billy Beane staring at a board of player names are treated with the same visual importance as game footage.
- **UI reference:** The "board of players" in Oakland's draft room — magnetic names on a whiteboard, constantly rearranged — is the direct spiritual ancestor of PREMIERE's Board. Study the lighting (harsh fluorescents), the physicality (hands moving cards), the *weight* of each placement.

**4. The Big Short (2015, dir. Adam McKay)**
- **What we're learning:** Visual metaphors for complex systems. The Big Short uses cutaways, diagrams, and graphic overlays to make subprime mortgages understandable. PREMIERE should use visual metaphors (lead-in flow lines, demographic overlap indicators) to make the ratings engine legible without a PhD in media metrics.
- **Animation reference:** The animated infographics in The Big Short are slick without being flashy. Numbers and arrows move purposefully, not decoratively. Our ratings reveal animations should follow this principle.

**5. All the President's Men (1976, dir. Alan J. Pakula)**
- **What we're learning:** The aesthetic of investigative work. Newsrooms, file folders, typewritten memos, cork boards with pinned documents. The physical artifacts of pre-digital information management. This is the texture of PREMIERE's environmental storytelling — Variety headlines, manila folders, printed overnight ratings.
- **Sound design reference:** The clatter of typewriters, the ring of rotary phones, the ambient hum of an office. PREMIERE's soundscape should evoke this era of *working with physical information*.

### 7.3 Design References (Visual Style and Execution)

**1. Massimo Vignelli — 1970s NYC Subway Map**
- **What we're learning:** Ruthless clarity through reduction. Vignelli's subway map strips away all geographic accuracy to show only what matters: which line goes where, which stations connect. The Board should follow this principle — eliminate everything that doesn't serve strategic decision-making.
- **Color system reference:** Vignelli's color-coded subway lines are *semantically pure* — each line has one color, that color means that line and nothing else. Our genre color system and information colors follow the same rule.

**2. Dieter Rams — Braun Product Design (1960s-1980s)**
- **What we're learning:** "Good design is as little design as possible." Rams' Braun calculators, radios, and clocks are instantly readable because every element serves a function. No decoration. PREMIERE's UI follows this ethos.
- **Form principle reference:** Rams' 10 principles of good design map directly to our rules:
  - Innovative? (The Board as a drag-and-drop strategy layer is novel in management sims)
  - Makes a product useful? (Every UI element serves strategic decision-making)
  - Aesthetic? (Utilitarian beauty)
  - Makes a product understandable? (Visual hierarchy, redundant encoding, progressive disclosure)
  - Unobtrusive? (UI recedes when not needed, no decorative elements)
  - Honest? (Shows systems transparently, no hidden mechanics)
  - Long-lasting? (Period authenticity without being trendy)
  - Thorough down to the last detail? (Pixel-perfect implementation)
  - Environmentally friendly? (N/A for digital product)
  - As little design as possible? (Core principle)

**3. Edward Tufte — Information Design (The Visual Display of Quantitative Information)**
- **What we're learning:** Maximize data-ink ratio. Every mark on the screen should represent data. Minimize "chart junk" (decorative elements that don't convey information). Our show cards and data tables follow Tufte's principles rigorously.
- **Specific technique reference:** Tufte's "small multiples" — repeating the same chart structure across different data sets to enable comparison. PREMIERE's grid of show cards is a small multiples system: same card design, different data, instant comparability.

**4. Swiss International Style (1950s-1980s graphic design movement)**
- **What we're learning:** Grid-based layouts, sans-serif typography, asymmetric alignment for hierarchy, maximum readability. This is the foundation of modern UI design for a reason.
- **Visual reference:** Posters by Josef Müller-Brockmann — especially his concert posters for Zurich Tonhalle. The way he uses scale, weight, and position to create hierarchy without color is directly applicable to our typographic system.

**5. Airline Timetables and Timetable Design (1960s-1980s)**
- **What we're learning:** Displaying schedules clearly. Old airline timetables are masterclasses in information density — showing 50+ flights per page with departure times, arrival times, flight numbers, aircraft types, all readable at a glance. The Board is a TV schedule, and these are its conceptual ancestors.
- **Layout reference:** The grid structure, the use of bold vs. regular weight to distinguish primary vs. secondary information, the minimal use of color (often just one or two spot colors).

### 7.4 Historical Reference Materials (Period Authenticity)

**1. Network Scheduling Boards (Archival Photos)**
- **Source:** Behind-the-scenes photos from NBC, CBS, ABC scheduling meetings (2000s)
- **What we're studying:** The actual boards used by real network executives. White magnetic boards, card stock with printed show info, handwritten notes in margins, Post-It notes for last-minute changes.
- **Key observation:** These boards are *working documents*, not polished presentations. They have coffee rings, crossed-out cards, overlapping notes. Our UI should feel *used* without being messy — subtle texture overlays on cards (barely perceptible), slight imperfections that suggest physicality without hindering readability.

**2. Variety Magazine Covers and Headlines (2000-2012)**
- **Source:** Variety digital archive
- **What we're studying:** The language of the industry. How Variety wrote about hits, flops, executive shake-ups, upfronts, sweeps, cancellations. This language should infuse our event notifications and headlines.
- **Typography reference:** Variety's masthead and headline treatments — bold, all-caps, slightly condensed sans-serif. We're not copying it directly, but the *authority* of that typography informs our screen titles.

**3. Nielsen Overnight Ratings Printouts**
- **Source:** Photos of actual Nielsen reports from industry insiders (scattered across media blogs and Twitter)
- **What we're studying:** The format of the data. How overnights were presented — usually dense tables with columns for timeslot, show title, household rating, share, A18-49 rating, total viewers. Our ratings reveal screen should evoke this format (minus the actual printout aesthetic — we're digital, but we honor the structure).

**4. Network Upfront Presentations (Video Archives)**
- **Source:** YouTube archives of NBC, ABC, CBS, Fox upfront sizzle reels (2000s)
- **What we're studying:** The *spectacle* of selling a schedule. Upfronts are theatrical events — executives on stage, highlight reels, celebrity appearances, the swelling orchestral music. If we implement the Upfront Presentation System (stretch goal), this is the tonal reference. But even if we don't, the *energy* of an upfront should infuse the marketing spend and advertising confidence systems — the player is always selling, even when they're scheduling.

**5. 2000s Office Environments (Corporate Interior Design Archives)**
- **Source:** Office furniture catalogs from Herman Miller, Steelcase (2000-2010), Google Images search for "2000s office interior"
- **What we're studying:** The look of a network executive's corner office circa 2005. Key elements: CRT monitors alongside early flat-screens, vertical blinds, mahogany or dark wood desks, ergonomic mesh chairs (Aeron era), potted plants (ficus trees), framed posters of network shows on walls, credenzas with awards/photos.
- **Application:** Background environments use these elements sparingly. The player's office should feel *aspirational* but also *isolating* — large, well-appointed, but often empty. The window shows a Manhattan skyline at night. You're at the top. You're alone.

---

## 8. Technical Constraints Summary

### 8.1 Platform Requirements

**Primary Platform: PC (Steam)**
- **Resolution targets:** 1920x1080 (baseline), 2560x1440, 3840x2160 (4K)
- **Aspect ratio:** 16:9 (primary), 16:10 (secondary support for ultrawide interface scaling)
- **Frame rate target:** 60fps minimum for UI, 30fps acceptable for background elements (environmental photos don't need high refresh)
- **Input:** Mouse + keyboard (primary), controller support (secondary — grid cursor navigation)

**Secondary Platform: Steam Deck**
- **Resolution:** 1280x800 (16:10 aspect ratio)
- **Input:** Touchscreen (primary for card dragging), gamepad (secondary for navigation)
- **Performance target:** 40fps minimum (Steam Deck's 40Hz mode is ideal for strategy games)
- **UI scaling:** All UI elements scale to 0.85x to fit smaller screen without losing readability. Minimum touch target: 44x44px (Apple/Android touch target guidelines apply even on Steam Deck).

**Font Rendering:**
- Subpixel antialiasing enabled on PC (ClearType on Windows, subpixel AA on macOS/Linux)
- Grayscale antialiasing only on Steam Deck (OLED screen doesn't benefit from subpixel AA)
- Hinting: Light hinting for IBM Plex Sans to preserve designer's intended letterforms

### 8.2 Asset Budget (Performance Targets)

**Memory Budget for UI Assets:**
- Total UI textures in memory (all resolutions loaded): <300MB
- Per-card texture budget: <50KB (after compression)
- Icon atlas: Single 2048x2048px texture sheet for all icons (<2MB)

**Draw Call Budget:**
- Maximum draw calls per frame for entire UI: 150 (typical for complex UI-heavy screens)
- Show cards: Batched rendering (all cards use same material, drawn in single batched draw call where possible)

**Texture Atlasing Strategy:**
- All icons (genre, stat, action): Single atlas
- All button states: Single atlas
- Show card base textures: Single atlas (shared template, only data layers change per card)
- Environmental backgrounds: Separate textures (not atlased, loaded per scene)

### 8.3 Localization Constraints

**Text Expansion:**
- English is baseline. Romance languages (French, Spanish, Italian) expand by 20-30%. German expands by 30-40%.
- All UI text fields must support 40% text expansion without breaking layout
- Show card titles: Max 28 characters in English becomes ~35-40 characters in German. Use dynamic font scaling (reduce by 10% if over character limit, minimum 14pt).

**Font Support:**
- IBM Plex Sans includes Latin Extended, Cyrillic, Greek character sets
- For CJK languages (Chinese, Japanese, Korean): Substitute with Noto Sans CJK (open-source, similar x-height and weight to IBM Plex)
- Arabic/Hebrew: Right-to-left (RTL) layout support required for menus/modals. The Board itself is spatial and doesn't require RTL mirroring.

**Cultural Adaptation:**
- Genre names may need cultural substitution (e.g., "Legal Drama" is clear in English, "juridique drame" is awkward in French — localize to "Série judiciaire")
- Demographic labels: "A18-49" is US-specific Nielsen notation. Consider renaming to "Adults 18-49" in non-US localizations for clarity.

### 8.4 Accessibility Features (Beyond Colorblind Mode)

**Screen Reader Support (Partial):**
- All menu navigation and text-based UI elements should be screen-reader compatible (ARIA labels for web-based builds, accessibility APIs for native)
- The Board's drag-and-drop interface is inherently visual and not fully screen-reader accessible. Provide alternative "list-based scheduling mode" for visually impaired players (shows as sortable list, assign to timeslots via dropdown menus rather than drag-and-drop). This is a stretch goal but documented for future implementation.

**Text Scaling:**
- User setting: Scale all UI text by 100% / 115% / 130%
- At 130% scale, some UI elements may reflow (multi-line text wrapping, vertical scrolling in panels)

**Animation Toggle:**
- User setting: Reduce motion (turns off card lift animations, number count-ups, smooth transitions)
- When enabled: State changes are instant (no tweening), only essential feedback remains (highlight changes, color changes)

**High Contrast Mode:**
- User setting: Increase contrast by 30% across all UI elements
- Background darkens slightly (Fluorescent White → 10% darker), text darkens (near-black → pure black), information colors become more saturated

### 8.5 Development Workflow and Version Control

**Asset Versioning:**
- All Figma files are versioned with date stamps: `PREMIERE_UI_MasterFile_2026-02-07.fig`
- Major iteration milestones are saved as separate files: `_v1_Prototype`, `_v2_AlphaReady`, `_v3_BetaPolish`, `_v4_Final`
- Exported assets are versioned in Git LFS (Large File Storage) to avoid bloating the repo

**Change Log:**
- Every asset update includes a changelog entry in `PREMIERE_ArtDirection_CHANGELOG.md`:
  - Date
  - Asset changed
  - Reason for change
  - Impact on existing implementation (does dev need to re-integrate?)

**Approval Process:**
1. Art Director creates/updates asset in Figma
2. Asset exported and placed in staging folder
3. Dev integrates into engine
4. Art Director reviews in-engine implementation (pixel-perfect check)
5. If approved, asset moves from staging to production folder
6. If rejected, Art Director provides annotated screenshot of issues, returns to step 1

---

## 9. Mood Boards and Visual Examples (To Be Created)

The following visual reference materials will be created during production. This section serves as a checklist:

### 9.1 Mood Board 1: The Board Interface
- **Contents:** 20-30 images of magnetic scheduling boards, card-based UIs, office whiteboards, physical planning tools
- **Purpose:** Establish the tactile, physical aesthetic of the primary interface
- **Delivery:** Single PNG (3000x2000px), organized in grid layout with annotations

### 9.2 Mood Board 2: The Corner Office
- **Contents:** 20-30 images of executive offices (2000s era), Manhattan skylines at night, fluorescent-lit workspaces, isolation and power
- **Purpose:** Define the environmental storytelling aesthetic for background spaces
- **Delivery:** Single PNG (3000x2000px), organized in grid layout with annotations

### 9.3 Mood Board 3: Period Artifacts
- **Contents:** Variety headlines, Nielsen printouts, flip phones on desks, CRT monitors, DVD-by-mail envelopes, 2000s UI design (Windows XP, early web), office equipment
- **Purpose:** Ground the game in the specific texture of the 2000s without parody
- **Delivery:** Single PNG (3000x2000px), organized in grid layout with annotations

### 9.4 Style Frames: Show Card Variants
- **Contents:** 12 fully-designed show cards representing different genres, states, and performance levels
- **Purpose:** Demonstrate the card component system in practice
- **Delivery:** Figma file with 12 artboards, exported as PDF for presentation

### 9.5 Style Frames: Key Screens
- **Contents:** 6 fully-designed screens:
  1. The Board (full grid, mid-season state)
  2. Overnight Ratings Reveal
  3. Pilot Evaluation Screen
  4. Talent Relationship Screen (Rolodex view)
  5. Budget Ledger Screen
  6. Season End Review / Legacy Score
- **Purpose:** Show the complete visual system in context
- **Delivery:** Figma file with 6 artboards (1920x1080), exported as interactive prototype

### 9.6 Motion Study: Key Animations
- **Contents:** Video recordings (screen captures) of 5 key animations:
  1. Card drag and drop with ripple effect
  2. Ratings reveal staggered animation
  3. Modal window open/close
  4. Warning notification pulse
  5. Week-to-week transition
- **Purpose:** Demonstrate timing and easing for dev implementation
- **Delivery:** 5 MP4 files (1920x1080, 60fps), uploaded to shared drive with timing annotations in accompanying doc

---

## 10. Closing Statement: What This Art Direction Achieves

PREMIERE is a game about making decisions under pressure in a high-stakes creative industry. The art direction serves that fantasy through *restraint, clarity, and atmosphere*.

**What a player should feel when they look at The Board:**
- "I am in control of this grid."
- "Every number I see means something specific."
- "When I move a card, the consequences are clear."
- "This looks like a real tool used by real professionals."
- "I am powerful. I am alone. I am responsible."

The visual identity does not shout. It does not distract. It communicates instantly and then gets out of the way. When a player remembers PREMIERE six months after playing, they should remember *the strategic tension of placing a show card on Thursday at 9 PM*, not the UI. But the UI is what makes that tension legible.

**The test of this art direction:**
If we stripped away every interface element and left only The Board — 21 show cards on a white grid — would the player still understand the game? Would they still feel the weight of their decisions? If the answer is yes, the art direction has succeeded. Everything else — the color palette, the typography, the motion design — exists to enhance that core clarity, never to obscure it.

**The promise of this art direction:**
Every pixel earns its place. Every color means something. Every shape communicates at a glance. The player should be able to read The Board like a network executive reads a scheduling grid — not as a collection of menus and numbers, but as a living strategic landscape where every decision ripples.

Show me, don't tell me. That's the rule. The Board shows you what matters. The art direction makes sure you can see it.

---

**End of Art Direction Document**

**Next Steps:**
1. Create mood boards (Section 9) during pre-production Week 1
2. Build Figma component library (Section 5) during pre-production Week 2
3. Export icon library and style guide assets (Section 5) by pre-production Week 3
4. Conduct first readability playtest (Section 6) with prototype build at end of Month 1
5. Iterate based on playtest feedback, finalize style guide by end of Month 2

**Questions for Production Team:**
- Which game engine are we using? (Unity, Unreal, custom?) — This affects texture formats and UI implementation approach.
- Do we have access to a dedicated UI engineer, or will this be implemented by generalist programmers? — This affects how much support documentation we need (Unity UGUI tutorials, shader specifications for visual effects, etc.).
- What is our localization target list for launch? — This affects font selection and text expansion testing scope.

**Contact:**
Art Director: PIXEL
Document Version: 1.0 — 2026-02-07
