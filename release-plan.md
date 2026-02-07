# PREMIERE — Release Plan

**Version:** 1.0
**Author:** SHIP (Release Manager)
**Status:** Pre-Production Release Planning
**Target Platform:** PC (Steam), Steam Deck
**Target Launch:** TBD (Month 20 of development cycle)

---

## 0. SHIP's Note

Let me be clear about something. Launch day is not a celebration. Launch day is a test. A test of every decision you made for 20 months. A test of whether you caught the bugs that matter. A test of whether your store page converts. A test of whether your build works on a clean machine with a fresh install. A test of whether you planned for the chaos.

I have seen launch days go sideways in every possible way. Builds that worked locally but crashed on Intel GPUs. Store pages that went live with placeholder text. Review codes sent to the wrong addresses. Achievements that didn't unlock. Saves that corrupted. Patches that made things worse.

Every single one of those disasters was preventable. Every single one happened because someone said "we'll handle that later" or "it works on my machine" or "first impressions don't matter that much."

First impressions are permanent. You get one launch. One wave of reviews. One moment when press and streamers are paying attention. Botch it, and you spend six months digging out of a hole. Nail it, and the game sells itself.

This document exists to make launch day boring. If nothing goes wrong, I did my job.

What's the goal? Zero surprises on launch day.

What's the plan? Checklists. Testing. Redundancy. Rollback procedures. Automation where possible. Documentation where not.

Let's make this launch so smooth it's forgettable.

---

## 1. Master Launch Checklist

This is the master timeline from code complete to post-launch monitoring. Every task has an owner, a deadline, and a verification step. If it's not on the checklist, it doesn't happen.

### 1.1 Launch Minus 12 Weeks: Code Complete & Gold Candidate

**Milestone:** Last feature commit. All systems implemented. Content complete.

| Task | Owner | Deadline | Verification |
|---|---|---|---|
| Feature freeze declared | Lead | L-12w | Git branch `gold-candidate` created from `develop` |
| All core systems implemented and integrated | Engineering | L-12w | Playthrough of full 12-season career completes without crash |
| All 200+ show templates authored | Design | L-12w | Pilot generator test: 500 pilots generated, no duplicates, no invalid stats |
| All 80+ events authored and tested | Design | L-12w | Event debugger: all events fire correctly with all choice paths |
| All UI screens implemented | UI/UX | L-12w | Walkthrough of every menu, screen, and popup |
| Save/load system stress-tested | Engineering | L-12w | 100 save/load cycles on Season 12 save file, zero corruption |

**Deliverable:** Gold Candidate Build v0.9.0

**Rollback Plan:** If any critical system is incomplete, delay launch by 4 weeks. No exceptions. Do not ship incomplete features.

---

### 1.2 Launch Minus 10 Weeks: QA Phase 1 (Internal Testing)

**Milestone:** Internal QA catches critical bugs. Balance tuning begins.

| Task | Owner | Deadline | Verification |
|---|---|---|---|
| QA test plan authored | QA Lead | L-10w | Test plan document covers all systems, all platforms, all edge cases |
| 10 internal testers assigned | QA Lead | L-10w | Each tester completes at least one 3-season playthrough |
| Critical bug triage (crashes, save corruption, soft locks) | Engineering | L-10w | Zero P0 bugs remain. All P1 bugs have fixes in progress. |
| Balance data exported and analyzed | Design | L-10w | Economy spreadsheet reviewed: no dominant strategies, prestige/popularity tension verified |
| Performance profiling on minimum spec hardware | Engineering | L-10w | 60 FPS on recommended spec, 30 FPS on minimum spec, zero frame drops during card drag |
| Steam Deck performance validation | Engineering | L-10w | Game runs at 60 FPS at 800p on Steam Deck hardware or emulation |

**Deliverable:** Gold Candidate Build v0.9.5 (first patch applied)

**Rollback Plan:** If P0 bugs remain (crashes, save corruption), delay external QA. Do not send broken builds to external testers.

---

### 1.3 Launch Minus 8 Weeks: QA Phase 2 (External Testing)

**Milestone:** External playtesters validate gameplay loop, find edge cases, report clarity issues.

| Task | Owner | Deadline | Verification |
|---|---|---|---|
| 20 external playtesters recruited | QA Lead | L-8w | Tester pool includes min spec users, Steam Deck users, accessibility testers |
| External test build distributed via Steam Playtest | Engineering | L-8w | Build uploaded to Steam backend, playtest group created, keys sent |
| Feedback survey deployed | QA Lead | L-8w | Survey asks: clarity of mechanics, balance, bugs, "would you buy this?" |
| Bug reports triaged daily | QA Lead | L-8w | All reported bugs logged in tracker, prioritized, assigned |
| Balance adjustments based on aggregate data | Design | L-8w | If 70%+ of players pursue same strategy, rebalance. If ratings feel random, clarify feedback. |
| Localization string extraction complete | Engineering | L-8w | All UI text, event text, tutorial text extracted to JSON for future localization |

**Deliverable:** Release Candidate Build v1.0.0-rc1

**Rollback Plan:** If external testers report confusion about core mechanics, delay launch for tutorial pass. Do not ship a game players can't understand.

---

### 1.4 Launch Minus 6 Weeks: Platform Configuration (Steamworks Setup)

**Milestone:** Steam store page configured. Achievements, trading cards, cloud saves implemented.

| Task | Owner | Deadline | Verification |
|---|---|---|---|
| **Steam App ID created** | Release Manager | L-6w | App ID registered on Steamworks, dev build uploaded to `default` branch |
| **Store page drafted** | Marketing | L-6w | Capsule art, screenshots, trailer, description, tags, pricing all finalized |
| **Age rating acquired (IARC)** | Release Manager | L-6w | IARC questionnaire completed, rating certificate received (likely E10+ or T) |
| **Steam Achievements configured** | Engineering | L-6w | 50+ achievements authored in Steamworks, all unlock conditions tested |
| **Steam Trading Cards configured** | Art/Marketing | L-6w | 5 card designs submitted, badge/emoticon/background art provided |
| **Steam Cloud Saves enabled** | Engineering | L-6w | Save files sync across devices, tested on two machines with same account |
| **Steam Deck verified badge pursued** | Engineering | L-6w | Deck compatibility checklist completed, submitted for Valve review |
| **Regional pricing configured** | Release Manager | L-6w | Pricing set for all regions (use Steam's recommended pricing tool) |

**Deliverable:** Steamworks configuration complete, store page in "Coming Soon" state

**Rollback Plan:** If Steamworks configuration fails (rejected age rating, missing assets), delay store page reveal by 2 weeks.

---

### 1.5 Launch Minus 4 Weeks: Marketing & Pre-Launch

**Milestone:** Store page goes live. Wishlist campaign begins. Press outreach.

| Task | Owner | Deadline | Verification |
|---|---|---|---|
| **Store page goes live (Coming Soon)** | Marketing | L-4w | Store page visible on Steam, wishlist button active |
| **Announcement trailer released** | Marketing | L-4w | Trailer uploaded to YouTube, shared on Twitter/Reddit, embedded on store page |
| **Press kit distributed** | Marketing | L-4w | 50+ gaming press outlets contacted with review code offer, press kit link |
| **Influencer outreach** | Marketing | L-4w | 20+ streamers/YouTubers contacted with early access offer |
| **Launch date announced** | Marketing | L-4w | Launch date locked, communicated on store page, social media, press kit |
| **Demo build decision made** | Design/Marketing | L-4w | If demo: upload to Steam, set availability. If no demo: marketing plan adjusted. |
| **Discord server launched** | Marketing/Community | L-4w | Community hub for wishlists, FAQ, feedback gathering |

**Deliverable:** Public awareness campaign live, wishlist count tracking begins

**Rollback Plan:** If trailer reception is poor (low engagement, negative comments), delay launch and rework marketing messaging.

---

### 1.6 Launch Minus 2 Weeks: Review Code Distribution & Final Testing

**Milestone:** Press and influencers receive review codes. Final build testing on clean machines.

| Task | Owner | Deadline | Verification |
|---|---|---|---|
| **Final build uploaded to Steam (`default` branch)** | Engineering | L-2w | Build identical to launch build, tested on clean install |
| **Review codes generated (100 keys)** | Release Manager | L-2w | Steam keys generated, spreadsheet tracking recipient/outlet/date sent |
| **Review codes sent to press** | Marketing | L-2w | 50+ press outlets receive keys, embargo date communicated (launch day) |
| **Review codes sent to influencers** | Marketing | L-2w | 20+ streamers/YouTubers receive keys, encouraged to stream on launch day |
| **Clean machine testing (Windows/Mac/Linux)** | QA Lead | L-2w | Three testers install from Steam on fresh OS installs, verify zero dependency issues |
| **Day-one patch prepared (if needed)** | Engineering | L-2w | If critical bugs found in final testing, patch build ready to deploy on launch day |
| **Launch day communication templates prepared** | Marketing | L-2w | Social media posts, Discord announcements, email to wishlist pre-written |

**Deliverable:** Review build in hands of press/influencers, final build verified on clean machines

**Rollback Plan:** If clean machine testing reveals critical issues (missing DLLs, broken saves, launch crashes), delay launch by 1 week. Do not ship a broken build.

---

### 1.7 Launch Day: Go Live

**Milestone:** Game releases on Steam. Monitoring begins.

| Task | Owner | Time (UTC) | Verification |
|---|---|---|---|
| **Set Steam release live** | Release Manager | 10:00 AM PST (18:00 UTC) | Store page switches from "Coming Soon" to "Buy Now" |
| **Monitor Steam backend for issues** | Release Manager | 10:00-12:00 | Check for depot issues, download problems, DRM failures |
| **Social media launch announcement** | Marketing | 10:05 | Tweet, Discord, Reddit posts go live |
| **Monitor player reports (Discord, Steam forums, Reddit)** | Community Manager | 10:00-20:00 | First 10 hours: triage bug reports, respond to questions, flag critical issues |
| **Monitor review scores** | Marketing | 12:00-24:00 | Track Steam reviews, Metacritic (if applicable), influencer coverage |
| **Hotfix deployment (if needed)** | Engineering | On-demand | If critical bug reported by 10+ players, deploy patch within 4 hours |
| **Sales data check** | Release Manager | 20:00 | Compare launch day sales to wishlist conversion rate (target: 10-15%) |

**Deliverable:** Game is live. Players are playing. Monitoring is active.

**Rollback Plan:** If catastrophic issue discovered (game unplayable, mass refunds), pull build from Steam, issue public statement, deploy hotfix within 12 hours.

---

### 1.8 Launch Plus 1 Week: Post-Launch Monitoring & Patch 1.01

**Milestone:** Aggregate player feedback. Deploy first patch.

| Task | Owner | Deadline | Verification |
|---|---|---|---|
| **Bug report aggregation** | QA Lead | L+3d | All reported bugs logged, prioritized, duplicates merged |
| **Balance data analysis** | Design | L+5d | Analyze player strategies from telemetry (if implemented) or community feedback |
| **Patch 1.01 authored** | Engineering | L+7d | Fixes for top 10 reported bugs, balance tweaks if needed |
| **Patch 1.01 deployed to Steam** | Engineering | L+7d | Patch live on all platforms, patch notes published on Steam, Discord, social |
| **Review response campaign** | Marketing/Community | L+7d | Respond to negative reviews with acknowledgment, fixes promised. Thank positive reviews. |
| **Sales/review performance report** | Release Manager | L+7d | Report to team: units sold, review score, wishlist conversion, refund rate, press coverage |

**Deliverable:** First patch deployed, community feels heard, baseline metrics established

**Rollback Plan:** If patch introduces new bugs, roll back to launch build and re-test patch before re-deploying.

---

### 1.9 Launch Plus 1 Month: Patch 1.1 (Quality of Life)

**Milestone:** Quality-of-life improvements based on player feedback.

| Task | Owner | Deadline | Verification |
|---|---|---|---|
| QoL feature requests prioritized | Design | L+2w | Community feedback analyzed, top 5 QoL requests identified |
| QoL features implemented | Engineering | L+4w | Features like fast-forward button, stat tooltips, advisor mode added |
| Patch 1.1 deployed | Engineering | L+4w | Patch live, changelog published |
| Additional achievements added (if relevant) | Design | L+4w | 10+ new achievements to re-engage existing players |

**Deliverable:** Players feel the game is improving post-launch. Community retention.

---

## 2. Build Pipeline Documentation

### 2.1 Build Environments

| Environment | Purpose | Branch | Auto-Deploy? |
|---|---|---|---|
| **Development** | Active development, unstable | `develop` | Yes (nightly) |
| **Staging** | Internal QA testing | `staging` | Yes (weekly) |
| **Release Candidate** | External QA, press preview | `release-candidate` | Manual |
| **Production** | Live on Steam | `main` | Manual only |

### 2.2 Build Workflow

**Step-by-step from code commit to Steam:**

1. **Code Commit to `develop`**
   - Developer pushes feature branch to GitHub
   - PR reviewed, merged into `develop`
   - GitHub Actions triggers nightly build

2. **Nightly Build (Automated)**
   - Unity Cloud Build or GitHub Actions compiles Windows/Mac/Linux builds
   - Build uploaded to internal file server
   - QA team notified via Slack/Discord

3. **Weekly Staging Build**
   - On Fridays, `develop` merged into `staging`
   - Automated build triggered
   - Staging build deployed to private Steam branch `qa-test`
   - Internal testers download from Steam, test over weekend

4. **Release Candidate Build (Manual)**
   - When gold candidate is ready, `staging` merged into `release-candidate`
   - Manual build triggered by Lead Programmer
   - Build uploaded to Steam branch `rc-test`
   - External playtesters receive access via Steam Playtest
   - Build locked (no further commits until testing complete)

5. **Production Build (Manual, Double-Checked)**
   - When RC passes all tests, `release-candidate` merged into `main`
   - **Two engineers verify the commit SHA matches RC build**
   - Manual build triggered with version tag (e.g., `v1.0.0`)
   - Build uploaded to Steam branch `default`
   - **Build tested on three clean machines (Windows/Mac/Linux) before setting live**

### 2.3 Build Signing & DRM

**Windows Code Signing:**
- Purchase code signing certificate (Sectigo, DigiCert)
- Sign all `.exe` and `.dll` files to avoid Windows SmartScreen warnings
- Test signed build on clean Windows 10/11 machines

**Steam DRM:**
- Enable Steamworks DRM wrapper (light protection, prevents casual piracy)
- Do NOT use aggressive third-party DRM (Denuvo, etc.) — management sim audience hates it

**No DRM on GOG (if future platform):**
- If GOG release happens post-launch, ship DRM-free build
- Trust the audience. Goodwill > piracy paranoia.

### 2.4 Build Checklist (Pre-Upload)

Before uploading ANY build to Steam, verify:

- [ ] Build number incremented in `Application.version`
- [ ] All debug UI disabled (cheats, dev console, profiler overlay)
- [ ] All test data removed (placeholder shows, debug events)
- [ ] Splash screen displays correctly (Unity logo, studio logo, game logo)
- [ ] Save file versioning updated (if save format changed)
- [ ] Crash reporter enabled and sending to backend (if implemented)
- [ ] EULA and privacy policy links functional (if applicable)
- [ ] All third-party library licenses included in `Licenses.txt`

**If any box is unchecked, DO NOT UPLOAD.**

---

## 3. Platform Configuration Checklists

### 3.1 Steamworks Configuration

**Store Page Checklist:**

- [ ] **App Name:** PREMIERE (check for trademark conflicts)
- [ ] **Short Description:** 100 characters max, hook-focused
- [ ] **Long Description:** 2000 characters, covers fantasy, loop, features, comparables
- [ ] **Capsule Images:**
  - [ ] Main capsule (616x353)
  - [ ] Small capsule (231x87)
  - [ ] Header capsule (460x215)
  - [ ] Library header (1920x620)
  - [ ] Library capsule (600x900)
- [ ] **Screenshots:** 10 images, 1920x1080, showing The Board, ratings screen, pilot pool, talent inbox, Emmy ceremony
- [ ] **Trailer:** 1-2 minutes, uploaded to Steam video hosting
- [ ] **System Requirements:**
  - [ ] Minimum: Intel i5-6500, 4GB RAM, Integrated GPU, 2GB storage
  - [ ] Recommended: Intel i5-9400, 8GB RAM, Any GPU, 2GB SSD
- [ ] **Supported Languages:** English (UI and audio) — add more post-launch
- [ ] **Controller Support:** Full controller support (Steam Deck verified)
- [ ] **Tags:** Simulation, Strategy, Management, Tycoon, Singleplayer, Indie, 2000s, Television, Choices Matter
- [ ] **Categories:** Single-player, Steam Achievements, Full controller support, Steam Cloud, Steam Deck Verified
- [ ] **Pricing:** $19.99 USD base price (regional pricing auto-calculated via Steam tool)
- [ ] **Release Date:** Set 4 weeks before launch, update to exact date at L-4w

**Achievements Checklist (50+ achievements):**

Example achievements (implement all via Steamworks SDK):

- [ ] "Greenlight Your First Show" — Unlock: greenlight any pilot
- [ ] "Win Your First Emmy" — Unlock: win Emmy in any category
- [ ] "Survive November Sweeps" — Unlock: complete November sweeps without losing a show
- [ ] "Cancel a Hit" — Unlock: cancel a show with 8M+ viewers
- [ ] "The Prestige Network" — Unlock: Prestige score > 80
- [ ] "The Populist Network" — Unlock: Popularity score > 80
- [ ] "Complete a Full Career" — Unlock: play from 2000 to 2012
- [ ] "50 Shows Greenlit" — Unlock: greenlight 50 pilots across career
- [ ] "The Auteur Whisperer" — Unlock: maintain 3 showrunners at Loyalty > 70 simultaneously
- [ ] "Survive the Writers' Strike" — Unlock: complete 2007-2008 season without bankruptcy

**Steam Cloud Configuration:**

- [ ] Enable Steam Cloud in Steamworks
- [ ] Specify save file paths (Unity's `Application.persistentDataPath`)
- [ ] Max cloud storage: 100MB per user (save files are ~700KB each, supports ~140 saves)
- [ ] Test: save on Machine A, load on Machine B with same Steam account

**Steam Trading Cards Configuration:**

- [ ] Design 5 card artworks (show cards from the game: procedural, drama, comedy, reality, prestige)
- [ ] Submit card art to Steamworks (512x512 PNG)
- [ ] Design badge, emoticon, profile background art
- [ ] Set card drop rate (default: 50% of total cards drop during normal play, rest via trading)

**Steam Deck Verification Checklist:**

Test on actual Steam Deck hardware or use Deck development kit:

- [ ] Game launches without external dependencies (keyboard, mouse)
- [ ] All UI readable at 7-inch screen size (minimum font: 14pt)
- [ ] Native 16:10 resolution supported (1280x800)
- [ ] Controller input fully mapped (no mouse required)
- [ ] Touchscreen drag-and-drop works natively
- [ ] Performance: 60 FPS at 800p, or locked 30 FPS if needed
- [ ] Battery life: 4+ hours
- [ ] No graphical glitches (text rendering, UI scaling)
- [ ] Suspend/resume works (game pauses, state preserved)
- [ ] Cloud saves sync when docking/undocking

Submit Deck verification request to Valve 4 weeks before launch. Expect 2-week review turnaround.

---

### 3.2 Age Rating (IARC)

**Why IARC:** International Age Rating Coalition questionnaire is free and provides ratings for multiple regions (ESRB, PEGI, USK, etc.) via Steam.

**Process:**
1. Log into Steamworks
2. Navigate to IARC questionnaire
3. Answer questions about content:
   - Violence: None (management sim, no on-screen violence)
   - Sex/Nudity: None
   - Language: Mild (references to "controversial content" in show descriptions, no profanity in UI)
   - Drugs/Alcohol: References only (actor scandal events mention DUI, rehab)
   - Gambling: None
   - Online interaction: None (single-player only)

**Expected Rating:**
- **ESRB:** E10+ (Everyone 10 and older) or T (Teen) — depends on how explicit scandal events are
- **PEGI:** 7 or 12
- **USK:** 6 or 12

**Timeline:** Submit L-6w, receive certificate within 1 week. If rating is unexpectedly high (M/18+), review content and edit if needed.

---

### 3.3 DLC & Microtransaction Plan (v1.0: None)

**Launch with zero DLC, zero microtransactions, zero season pass.**

Post-launch expansions (6+ months after launch, only if base game succeeds):
- Expansion 1: The Streaming Wars (2013-2020 era)
- Expansion 2: Classic Era (1980s-1990s)

**Pricing:** $9.99 per expansion, or $14.99 bundle if both.

Do NOT plan DLC before launch. Launch a complete game. Earn trust. Then expand.

---

## 4. Rollback & Hotfix Procedures

### 4.1 What Counts as a Hotfix-Worthy Issue

**Critical (Deploy within 4 hours):**
- Game crashes on launch for 20%+ of players
- Save corruption affecting new saves
- Achievements not unlocking
- Game unwinnable due to soft lock
- Major visual glitch (UI unreadable, cards invisible)

**High Priority (Deploy within 24 hours):**
- Progression blocker affecting 5%+ of players
- Balance issue making game trivial or impossible
- Specific hardware incompatibility (e.g., Intel GPU crash)

**Medium Priority (Deploy in Patch 1.01, 1 week post-launch):**
- Minor bugs (typos, tooltip errors, animation glitches)
- QoL requests (missing hotkeys, unclear tooltips)

**Low Priority (Deploy in Patch 1.1, 1 month post-launch):**
- Feature requests
- Cosmetic polish

### 4.2 Hotfix Deployment Workflow

**Step 1: Triage (0-30 minutes)**
- Community Manager logs issue in bug tracker
- Engineering Lead confirms severity
- If critical: proceed to Step 2
- If not critical: schedule for next patch

**Step 2: Fix & Test (1-3 hours)**
- Engineer reproduces bug locally
- Applies fix on hotfix branch (branched from `main`)
- Tests fix on clean install
- Second engineer verifies fix

**Step 3: Build & Upload (30 minutes)**
- Manual build triggered with version increment (e.g., `v1.0.1`)
- Build uploaded to Steam branch `hotfix-test`
- QA Lead tests on clean machine

**Step 4: Deploy to Production (15 minutes)**
- Hotfix build promoted to `default` branch on Steam
- Patch notes published on Steam, Discord, Twitter
- Community Manager announces fix

**Step 5: Monitor (2 hours)**
- Engineering Lead monitors player reports
- Verify fix resolves issue
- Verify no new issues introduced

**Total Time: 4 hours from report to live.**

### 4.3 Rollback Procedure (If Patch Breaks Game)

**Scenario:** Hotfix introduces worse bug than it fixed.

**Rollback Workflow:**

1. **Immediate:** Revert Steam `default` branch to previous build version
   - Log into Steamworks
   - Navigate to Builds tab
   - Set previous build as live
   - Publish change
   - **Downtime: 5 minutes**

2. **Communication:** Post public statement immediately
   - "We've identified an issue with today's patch. We've rolled back to the previous version while we investigate. Your saves are safe. We'll have a fix within 12 hours."
   - Post on Steam news, Discord, Twitter

3. **Fix the fix:** Re-test hotfix, identify what broke, apply second fix

4. **Re-deploy:** Follow hotfix workflow again, double-test this time

**This is why we keep 3 rotating autosave slots.** If a patch corrupts saves, players can load a pre-patch save.

---

## 5. Launch Day Timeline (Hour-by-Hour)

**Date:** TBD (set at L-4w)
**Launch Time:** 10:00 AM PST / 18:00 UTC (standard Steam release time)

### Hour-by-Hour Runbook

**09:00 - Pre-Launch Check**
- Release Manager logs into Steamworks
- Verifies `default` branch is set to launch build
- Verifies release date/time is correct
- Verifies store page is ready to switch from "Coming Soon" to live
- Engineering Lead on standby, ready to deploy hotfix if needed

**10:00 - GO LIVE**
- Release Manager sets release live in Steamworks
- Refresh store page: confirm "Buy Now" button appears
- Marketing posts launch announcement on Twitter, Discord, Reddit
- Community Manager pins launch thread on Discord

**10:05 - Initial Monitoring**
- Check Steam backend for download issues
- Monitor Discord #bug-reports channel
- Monitor Steam community forums
- Monitor r/PREMIERE (if subreddit exists)

**10:30 - First Player Reports**
- Community Manager logs any issues reported in first 30 minutes
- Engineering Lead triages reports: critical vs. minor

**12:00 - Midday Check**
- Release Manager checks Steam sales dashboard: units sold, wishlists remaining
- Check for first Steam reviews (positive/negative ratio)
- Check if any press reviews went live

**14:00 - Streamer Coverage Check**
- Marketing monitors Twitch/YouTube for streamer coverage
- Clip any highlight moments for social media

**16:00 - Afternoon Triage**
- QA Lead compiles all reported bugs (aim for pattern detection: "5 players report same crash on Intel GPUs")
- If critical bug pattern detected: begin hotfix workflow

**18:00 - Evening Review**
- Release Manager reports to team: sales, review score, top bugs, overall sentiment
- Decision point: deploy hotfix tonight or wait until morning?

**20:00 - End of Day 1**
- Community Manager posts "Thank you for playing" message on Discord/Twitter
- Engineering Lead remains on-call for critical issues overnight

**Next Morning:**
- Review overnight reports
- Deploy Patch 1.01 within 7 days if needed

---

## 6. Post-Launch Monitoring Plan

### 6.1 Metrics to Track (Daily for First Week, Weekly Thereafter)

**Sales & Revenue:**
- Units sold (Steam dashboard)
- Revenue (gross, net after Steam's 30% cut)
- Refund rate (target: under 10%)
- Wishlist conversion rate (target: 10-15% convert to sales in first week)

**Player Engagement:**
- Average playtime (Steam metrics)
- Median playtime (50% of players should play 3+ hours in first session if loop works)
- Achievement unlock rates (if 90%+ don't unlock "Greenlight Your First Show", tutorial is broken)

**Reviews & Sentiment:**
- Steam review score (target: 85%+ positive, "Very Positive")
- Number of reviews (more reviews = more visibility in algorithm)
- Metacritic score (if critics review it)
- Top complaints from negative reviews (triage into patches)

**Technical Health:**
- Crash rate (Steam collects crash logs if integrated)
- Save corruption reports (target: zero)
- Bug report volume (should decline week-over-week as patches deploy)

**Community Health:**
- Discord activity (daily active users)
- Reddit sentiment (if community forms)
- Support ticket volume (Steam support + Discord DMs)

### 6.2 What to Watch For (Red Flags)

**Critical Red Flags (Fix Immediately):**
- Refund rate above 20% → game is broken or mismarketed
- Review score below 70% → fundamental design or technical issue
- Crash reports spiking on specific hardware → driver incompatibility, deploy hotfix
- "Unplayable" appearing in multiple reviews → soft lock or progression blocker

**Warning Flags (Address in Patch 1.01):**
- Median playtime under 1 hour → tutorial is bad or game isn't engaging
- Specific achievement unlock rate under 50% → achievement is bugged or too hard
- Consistent complaint theme in reviews (e.g., "UI is too small") → QoL fix needed

**Good Signals:**
- Refund rate under 5% → players are keeping the game
- Review score above 85% → strong reception
- Median playtime above 3 hours → loop is working
- Streamers returning for multiple sessions → replayability confirmed

### 6.3 Communication Cadence

**First Week:**
- Daily Discord update from Community Manager (bug fix status, patch ETA, thank players)
- Respond to every negative Steam review with acknowledgment (not defensiveness)
- Post patch notes within 24 hours of any hotfix

**First Month:**
- Weekly development update (what's being worked on for Patch 1.1)
- Bi-weekly community spotlight (feature player strategies, funny moments)

**Ongoing:**
- Monthly patch or content update
- Transparency about what's next (no radio silence for 3+ months)

---

## 7. Age Ratings Deep Dive

### 7.1 Content Descriptors for IARC Questionnaire

**Violence:**
- **None.** This is a management sim. No on-screen violence. References to crime (police procedurals in show descriptions) but no depiction.

**Sexual Content:**
- **None.** No nudity, no sexual situations. Show descriptions may reference "romantic tension" or "love triangle" but nothing explicit.

**Language:**
- **Mild.** No profanity in UI or dialogue. Scandal events may reference adult themes ("DUI arrest", "rehab") but no explicit language.

**Drugs/Alcohol:**
- **References Only.** Actor scandal events may mention "DUI", "substance abuse", "rehab stint". No depiction of drug use.

**Gambling:**
- **None.** No in-game gambling, loot boxes, or randomized purchases.

**Online Interaction:**
- **None.** Single-player game. No chat, no user-generated content, no multiplayer.

**Expected Rating:**
- **ESRB: E10+ or T** — Likely E10+ (mild themes), possibly T if scandal events are detailed
- **PEGI: 7 or 12** — Likely 12 (mild bad language, implied violence in show descriptions)
- **USK: 6 or 12** — Likely 6 (no violence, mild themes)

### 7.2 If Rating Comes Back Higher Than Expected

**Scenario:** IARC returns M (Mature 17+) or PEGI 16 rating.

**Response:**
1. Review flagged content in IARC feedback
2. Edit or remove flagged content (e.g., tone down scandal event descriptions)
3. Re-submit questionnaire
4. Wait for updated rating

**Do NOT ship with M/16+ rating if content is actually E10+/T.** High age rating limits audience and signals wrong tone.

---

## 8. Lessons from Past Launches (What Not to Do)

### 8.1 Case Study: The Bad Launch

**What Happened:**
- Game launched with placeholder text on store page ("TODO: Write description here")
- Day-one build crashed on Intel integrated GPUs (40% of minimum spec users)
- Achievements didn't unlock due to Steamworks API not initialized
- First patch deployed within 12 hours... and corrupted all saves
- Review score tanked to 60%, never recovered
- Studio spent 6 months firefighting instead of building new content

**Lessons:**
- Test on clean machines with varied hardware
- Never deploy a patch without testing save compatibility
- Store page must be final 2 weeks before launch (no last-minute edits)
- If you ship broken, first impressions are permanent

### 8.2 Case Study: The Good Launch

**What Happened:**
- Game launched with polished store page, 10k wishlists
- Day-one build ran flawlessly on min spec to high-end hardware
- Achievements unlocked correctly
- First reviews were positive (90%+ on Steam)
- Minor bugs reported, patched within 3 days with no new issues
- Review score stayed above 85%, game sold 50k units in first month

**Lessons:**
- Test on varied hardware early and often
- Clean machine testing catches 90% of launch-day issues
- Respond fast to player feedback (but don't rush patches)
- Positive launch momentum compounds (algorithm favors well-reviewed games)

**PREMIERE will be a Good Launch.** That's the goal. That's the standard.

---

## 9. Contingency Plans (When Things Go Wrong)

### 9.1 Scenario: Catastrophic Launch Bug

**Example:** Game crashes on launch for 50%+ of players due to missing DLL dependency.

**Response:**
1. **Immediate (0-1 hour):**
   - Engineering Lead identifies root cause (e.g., missing Visual C++ Redistributable)
   - Hotfix prepared: bundle redistributable with installer or add dependency check
2. **Communication (1 hour):**
   - Post on Steam news, Discord, Twitter: "We've identified a launch issue affecting some players. Fix is in progress. ETA: 3 hours."
3. **Deploy (2-4 hours):**
   - Hotfix uploaded to Steam
   - Players notified via Steam update
4. **Monitor (4-8 hours):**
   - Verify crash reports drop to zero
   - Respond to every affected player who reported the bug

**Cost:** Bad first day reviews, but recoverable if fixed fast. Transparency and speed earn back trust.

### 9.2 Scenario: Review Bomb (Negative Reviews for Non-Game Reasons)

**Example:** Game gets review-bombed because players don't like the price, or because of unrelated drama.

**Response:**
1. **Do NOT panic.** Steam flags review bombs and filters them from score.
2. **Do NOT argue with reviewers.** Acknowledge concerns, stay professional.
3. **If price is the issue:** Consider if pricing is actually too high. Adjust if data supports it.
4. **If drama is unrelated:** Stay silent, let it pass. Engaging amplifies it.

**Steam's review bomb detection is effective.** Focus on legitimate feedback, ignore noise.

### 9.3 Scenario: Sales Underperform Expectations

**Example:** Game sells 500 units in first week. Expected 5,000.

**Response:**
1. **Diagnose (Week 1):**
   - Is marketing the issue? (Low visibility, bad trailer, unclear store page)
   - Is the game the issue? (Reviews mention design flaws, unclear mechanics)
   - Is the market the issue? (Genre saturation, bad timing)
2. **Iterate (Month 1):**
   - If marketing: rework trailer, run discount campaign, pitch to more press
   - If game: deploy QoL patches addressing top complaints, re-launch with "major update"
   - If market: pivot to different audience (e.g., target streamers for viral moments)
3. **Long-term (Month 3+):**
   - If sales don't recover: accept it, learn from it, move to next project
   - Do NOT throw good money after bad (no expensive ad campaigns for a game that didn't find market fit)

**Not every game is a hit. That's okay. Ship it, learn from it, ship the next one better.**

---

## 10. Success Criteria (What Does a Good Launch Look Like?)

### 10.1 Week 1 Targets

**Sales:**
- 5,000 units sold (baseline for indie management sim)
- 10-15% wishlist conversion rate
- Under 10% refund rate

**Reviews:**
- 100+ Steam reviews (more reviews = algorithm boost)
- 85%+ positive ("Very Positive" rating)
- Top positive themes: "addictive loop", "strategic depth", "unique premise"
- Top negative themes: minor bugs, QoL requests (not fundamental design complaints)

**Technical:**
- Zero P0 bugs (crashes, save corruption, unwinnable states)
- Fewer than 5 P1 bugs reported
- Hotfix deployed within 7 days if needed

**Community:**
- 500+ Discord members
- Active daily discussion (players sharing strategies, screenshots)
- At least 3 streamers covering the game on Twitch/YouTube

### 10.2 Month 1 Targets

**Sales:**
- 15,000 units sold (sustained interest beyond launch spike)
- Revenue covers development cost (break-even at ~$200k gross = ~$140k net after Steam cut)

**Reviews:**
- 300+ Steam reviews
- 85%+ positive maintained
- Metacritic score (if critics reviewed it): 75+

**Technical:**
- Patch 1.01 deployed, addressing top bugs
- Patch 1.1 in development, QoL features incoming

**Community:**
- 1,000+ Discord members
- Player-created content emerging (strategy guides, tier lists, challenge runs)
- Press coverage from at least 5 major outlets (PC Gamer, RPS, IGN, Eurogamer, etc.)

### 10.3 What "Success" Means Long-Term

**6 Months:**
- 50,000 units sold
- Revenue supports team salaries + next project
- Community is self-sustaining (players helping each other, mods emerging)
- Expansion DLC greenlit (The Streaming Wars)

**1 Year:**
- 100,000 units sold
- Positive ROI (made significantly more than development cost)
- Legacy: "PREMIERE is the definitive TV network management sim"

**If we hit these targets, we succeeded.** If we don't, we learn why and we ship the next one smarter.

---

## 11. Final Pre-Launch Checklist (The Big One)

This is the checklist I walk through 48 hours before launch. If anything is unchecked, we delay.

### Build & Platform

- [ ] Final build uploaded to Steam `default` branch
- [ ] Build tested on 3 clean machines (Windows 10, Windows 11, macOS, Linux)
- [ ] All platforms launch without errors
- [ ] Save/load tested on all platforms
- [ ] Steam Achievements unlock correctly
- [ ] Steam Cloud saves sync across devices
- [ ] Steam Deck verified badge received (or pending)
- [ ] No debug UI, no test data, no placeholder text in build

### Store & Marketing

- [ ] Store page final (no typos, all assets present)
- [ ] Trailer embedded and playing correctly
- [ ] Screenshots show best moments (The Board, ratings, talent, Emmy ceremony)
- [ ] Age rating certificate received and displayed
- [ ] Regional pricing set for all regions
- [ ] Launch date and time locked in Steamworks
- [ ] Press kit distributed to 50+ outlets
- [ ] Review codes sent to press and influencers
- [ ] Social media posts pre-written and scheduled

### Documentation & Support

- [ ] Patch notes template prepared
- [ ] FAQ posted on Discord and Steam forums
- [ ] Support email monitored (or Discord DM system ready)
- [ ] Hotfix workflow documented and team trained
- [ ] Rollback procedure tested (revert to previous build on Steam)

### Team Readiness

- [ ] Engineering Lead on-call for launch day
- [ ] Community Manager monitoring Discord/Steam forums starting at launch
- [ ] Marketing ready to post announcements at 10:00 AM PST
- [ ] QA Lead ready to triage bug reports
- [ ] Release Manager ready to execute rollback if catastrophic issue arises

**If every box is checked, we launch. If even one is not, we delay. No exceptions.**

---

## 12. Post-Launch Roadmap (Months 1-6)

**Month 1:**
- Patch 1.01 (bug fixes)
- Patch 1.1 (QoL improvements)
- Monitor reviews, sales, refunds
- Respond to community feedback

**Month 2:**
- Additional achievements (if players request)
- Minor balance tweaks based on player data
- Begin planning Expansion 1 (only if base game hits 15k units sold)

**Month 3:**
- Announce Expansion 1: The Streaming Wars (2013-2020 era)
- Community poll: what features do you want in the expansion?

**Month 6:**
- Release Expansion 1 ($9.99)
- Launch sale on base game (20% off) to drive new players
- Console port feasibility study (only if PC version sold 50k+ units)

**Year 1:**
- Release Expansion 2: Classic Era (1980s-1990s)
- Steam Workshop support (moddable show templates, custom talent)
- PREMIERE: Complete Edition bundle (base game + both expansions, $34.99)

**Do NOT plan beyond Year 1 until launch proves market fit.**

---

## 13. Closing Note from SHIP

You have 20 months to build this game. You have 20 hours on launch day to prove it works. The ratio is not fair. That's the job.

Every decision in this document exists to compress 20 months of work into a launch that Just Works. No surprises. No scrambling. No "we'll fix it later." Later is too late. First impressions are permanent.

Test on clean machines. Test on minimum spec hardware. Test on Steam Deck. Test save/load until you're bored of testing it. Test achievements. Test the store page. Test the build pipeline. Test the hotfix workflow. Test the rollback procedure.

Then test again.

Launch day is not the end of development. It's the beginning of a relationship with players. They bought your game. They trusted you. Honor that. Fix bugs fast. Communicate clearly. Don't go silent for three months. Don't promise features you can't deliver. Ship patches that improve the game, not patches that break saves.

If something goes wrong on launch day — and something always goes wrong — you have two choices. Panic, or execute the plan. This document is the plan. Follow it.

Make launch day boring. Make it so smooth that nobody notices how much work it took to make it smooth. That's the goal. That's success.

What's the rollback plan? Test it before you need it.

What's the hotfix procedure? Document it now, not when you're firefighting.

What's the last commit before gold? Lock the branch. No exceptions.

Let's ship this clean.

-- SHIP

---

**End of Release Plan**
**Document Status:** Living document, update as decisions are made
**Owner:** SHIP (Release Manager)
**Last Updated:** 2026-02-07
**Next Review:** At milestone: Code Complete (L-12w)
