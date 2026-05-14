# Q2–Q3 2026 ASO & TOFU Recovery Plan

**Created:** May 14, 2026
**Status:** Active
**Owner:** Marketing + Product

---

## Context

Top of funnel collapsed across the past 9 months. App Store installs dropped from a Sep 2024 peak of ~29,000/mo to ~860/mo in April 2026 — a 97% decline. The collapse was driven by three independent failures stacked on top of each other:

1. **App Store visibility broke late August 2025.** Competitor ASO activity (Khan Academy Kids description rewrite Aug 27, HOMER screenshots Aug 25) expanded their match surface for category keywords while Zoog's listing stood frozen — zero ASO-relevant metadata changes in the entire 12-month window. Apple's algorithm shifted ranking to actively-iterated competitors.
2. **Long-tail keyword universe collapsed late March / early April 2026.** Total ranked keywords dropped from ~120 to ~35. Possibly tied to Apple's March 2026 search ads expansion that pushed organic results down the page.
3. **Install → paid conversion compressed January 2026.** Meta paused; channel mix shifted to organic (4.4% sub CR vs Meta's 9.4%). Explained, not a funnel break.

Star rating (4.9★) stayed intact — that's the moat to lean on, not the cause.

**Strategic shift:** the listing isn't broken because we broke it. We need to **actively change metadata, build CPPs, ship In-App Events, and submit featuring nominations** — match the cadence competitors set. Sitting on the same listing is the problem.

---

## North-star metrics (90-day target)

| Metric | Today (May 2026) | 90-day target |
|---|---:|---:|
| AppTweak visibility score | -98 | -30 to -50 |
| Total ranked keywords | ~35 | 100+ |
| App Store CR (Imp → DL) | 1–2% | 4–6% |
| Monthly App Store installs | ~860 | 5,000–8,000 |
| In-App Events active | 0 | 1–2 always running |
| CPPs live | 0 | 8 |

---

## Workstreams

Five parallel tracks. Each has a Week-1 deliverable so we don't get stuck waiting for any single one.

### A. App Store Listing Refresh
### B. Custom Product Pages (CPPs)
### C. In-App Events
### D. Featuring Nominations
### E. Apple Search Ads (ASA) Hygiene

Plus a **Featured-tab segmentation** track on the engineering side, already filed as a backlog issue with `needs-specs`.

---

## Week 1 (May 12–18)

**Quick wins — most are minutes, all ship this week.**

### A. Listing Refresh
- [ ] Set promotional text (currently empty since Mar 20, 2026) — tie to Father's Day teaser
- [ ] Begin draft of new subtitle (3 variants for upcoming PPO test)
- [ ] Begin draft of new description following Children-doc 4-arc story (Spark → Hook → Co-create → Child reads)

### B. Custom Product Pages
- [ ] Inventory current CPPs in App Store Connect (expected: 0)
- [ ] Outline CPP taxonomy: 4 use-case + 4 occasion + 4 paid-campaign landing pages

### C. In-App Events
- [ ] Set up first event: **"Stories from Dad"** (Father's Day, runs Jun 7–21, 2026)
  - [ ] Event copy: name (30 chars), short desc (50 chars), long desc (120 chars)
  - [ ] Event hero image / video
  - [ ] Event type: Special Event
  - [ ] Submit for Apple review (allow ~3 days)

### D. Featuring Nominations
- [ ] Submit Father's Day nomination via App Store Connect → Promote your app
  - [ ] Lead with: 4.9★ / 20K+ ratings, AR filters, grandparent creator angle
  - [ ] Target placement window: Jun 14–21

### E. ASA Hygiene
- [x] Re-enable `zoog` brand keyword (DONE)
- [ ] Re-enable `zoog magical storytime` brand keyword
- [ ] Pause zero-paid keywords: `reading app for kids`, `read aloud kids`, `bookful`, `kids reading games`, `children story app`, `bedtime stories` (if 0 paid), `interactive kids stories` (if 0 paid)
- [ ] Increase budget on `zoog` (brand defense, ~603% ROAS) and `kids books` / `storybook app` (proven category)

### Featured Tab Merchandising (parallel cleanup)
- [ ] Drop dead featured slots: Did You Know? Earth Day, Did You Know? The North Star, Happy Cinco De Mayo, The Three Little Pigs, Pinocchio, Sparkle's Rainbow Adventure, Morning Routine: Brushing Teeth
- [ ] Add to featured: Happy Birthday, Happy Birthday Song, Brave Little Kiki, Winnie the Pooh

### Tooling
- [ ] Downgrade AppTweak from Grow to Essential ($299 → $99/mo)
- [ ] Confirm Apple PPO is enabled (App Store Connect → Product Page Optimization)
- [ ] Confirm Custom Product Pages module is enabled

---

## Week 2 (May 19–25)

### A. Listing Refresh
- [ ] Finalize new description (final 3,500–4,000 char version)
- [ ] Submit new metadata version to App Store Connect (description ships first; subtitle queued for PPO)
- [ ] Update keywords field (100 chars) to add high-intent terms not already covered in name/subtitle: `personalized,grandparent,storybook,bedtime,birthday,family,reading,gift`

### D. Featuring Nominations
- [ ] Submit Summer Reading featuring nomination (target Jun 22 onwards, ~5-week lead)

### Cross-track
- [ ] Pull AppTweak visibility baseline (anchor for measuring lift)
- [ ] Document current screenshot set / preview video for variant comparison

---

## Weeks 3–4 (May 26 – Jun 8) — CPPs Tier 1

Build the four use-case CPPs from the Children-doc arc. Each needs unique screenshots, copy, and a destination URL.

- [ ] **CPP 1: The Grandparent Creator**
  - [ ] Lead screenshot: grandparent recording for grandchild
  - [ ] Headline: "Personalized Stories from Grandma & Grandpa"
  - [ ] Use as landing page for grandparent-intent ASA campaign
- [ ] **CPP 2: Stories the Whole Family Shares**
  - [ ] Lead screenshot: child watching + reacting
  - [ ] Headline: "The App Your Whole Family Will Love"
  - [ ] Use as landing page for general family / parent campaigns
- [ ] **CPP 3: Read Together**
  - [ ] Lead screenshot: adult + child co-creating with AR filter
  - [ ] Headline: "Read Together. Learn Together. Stay Connected."
  - [ ] Use for "family reading" / "read-aloud" intent
- [ ] **CPP 4: Watch Your Child Become a Reader**
  - [ ] Lead screenshot: child holding device, reading independently
  - [ ] Headline: "From Bedtime Stories to First Reader"
  - [ ] Use for early-literacy intent

Each: ~1 day design + 1 day Apple review. All four shipped by end of Week 4.

### C. In-App Events
- [ ] Father's Day event goes live Jun 7

---

## Week 5 (Jun 9–15) — First PPO Test

### A. Listing Refresh
- [ ] **Launch first PPO test:** subtitle (3 variants vs control)
  - [ ] Variant A: emphasize "Personalized" + "Family"
  - [ ] Variant B: emphasize "Grandparent" persona explicitly
  - [ ] Variant C: emphasize social proof ("Loved by 20,000+ Families · 4.9★")
  - [ ] Apple distributes 90/10 traffic; auto-detects winner over 4–6 weeks

### C. In-App Events
- [ ] Set up second event: **"Summer Reading"** (runs Jun 22 – Jul 31)
  - [ ] Submit for review by Jun 18

### E. ASA
- [ ] Add grandparent-intent keyword group: `gifts for grandkids`, `grandparent app`, `grandma app`, `app for grandparents`, `stories for grandkids`
  - [ ] Link to CPP 1 (Grandparent Creator)
- [ ] Add competitor-defense keyword group: `caribu`, `bookful`, `vooks`, `homer kids`
  - [ ] Conservative bids; defensive, not aggressive

### D. Featuring Nominations
- [ ] Submit Back-to-School featuring nomination (target mid-August)

---

## Weeks 6–8 (Jun 16 – Jul 6) — CPPs Tier 2

Build the 4 occasion + lifecycle CPPs.

- [ ] **CPP 5: Birthday Stories** (Happy Birthday is your top-share-rate title at 78%)
  - [ ] Lead with personalized birthday card
  - [ ] Use for `birthday story for kids` / `personalized birthday video` keywords
- [ ] **CPP 6: Holiday Cards** (rotating; design once, swap hero asset per holiday)
  - [ ] Initial holidays: Christmas, Hanukkah, Valentine's Day, Easter, Mother's/Father's Day
- [ ] **CPP 7: The Long-Distance Family**
  - [ ] Target: military families, immigrant families, divorced families, distant grandparents
  - [ ] Use as landing for relevant content marketing / press
- [ ] **CPP 8: New Baby / New Grandchild**
  - [ ] Target the moment when the persona forms (first-time grandparent)
  - [ ] Tie to maternity/paternity content channels

### C. In-App Events
- [ ] Summer Reading event live through Jul 31
- [ ] Set up third event: **"Back to School"** (runs Aug 12–Sep 5)

---

## Weeks 9–12 (Jul 7 – Aug 3) — Compound

### A. Listing Refresh
- [ ] Apply PPO test winner to default subtitle
- [ ] **Launch second PPO test:** screenshots (test new screenshot order or new lead screenshot)
- [ ] Refresh promotional text monthly (calendar reminder)

### B. CPPs Tier 3 — Paid campaign landing pages
- [ ] **CPP 9:** Meta-campaign landing (when Meta reactivates)
- [ ] **CPP 10:** ASA brand-keyword landing (`zoog`, `zoog stories`)
- [ ] **CPP 11:** ASA category-keyword landing (`storybook app`, `kids books`)
- [ ] **CPP 12:** Influencer / press landing

### C. In-App Events
- [ ] Back-to-School event live Aug 12+
- [ ] Set up Halloween event (runs Oct 12–Nov 1)

### D. Featuring Nominations
- [ ] Submit Halloween nomination (target late October)
- [ ] Submit Holiday season nomination (target December)

### Measurement
- [ ] First post-refresh visibility report — measure lift vs Apr 2026 baseline
- [ ] AppTweak monthly competitor scan — flag any major competitor ASO moves
- [ ] Cross-reference paid CR by source (App Store Connect Sources view) — confirm CR is recovering on App Store Search

---

## Steady-state cadence (after Week 12 / Aug 4 onwards)

- [ ] **Metadata refresh** every 30–45 days (subtitle, screenshot, or description tweak)
- [ ] **In-App Event** always running, tied to next occasion or AI-pipeline content release
- [ ] **PPO test** always running
- [ ] **Featuring nomination** every 6–8 weeks for upcoming moments
- [ ] **CPP additions** 1–2 new ones per month as use cases warrant
- [ ] **Competitor metadata check** monthly via AppTweak
- [ ] **AppTweak alert** on visibility-score downgrade (set threshold at -60)

---

## Parallel engineering tracks (not strictly ASO but inside broader TOFU)

| Track | Status |
|---|---|
| Featured-tab segmentation (iOS + Cloud Functions) | Filed as backlog issue, `needs-specs` |
| Smart App Banner on web viewer | Not yet scoped |
| Open Graph card personalization on shared links | Not yet scoped |
| App Clip on web viewer | Larger scope, defer to Q3 |
| AI-pipeline release marketing playbook (PR + email + In-App Event + push per release) | Defer to Month 2 |

---

## Tool stack (target ~$120/mo total)

- **Apple PPO** (free, native) — A/B test icon / screenshots / preview video
- **Apple Custom Product Pages** (free, native) — up to 70 use-case landing pages
- **Apple In-App Events** (free, native) — recurring event placements
- **AppTweak Essential** ($99/mo) — keyword + competitor monitoring
- **Figma** (free) — screenshot design
- **PickFu** (~$20/mo budget) — pre-launch screenshot validation
- **Claude / ChatGPT** ($20/mo) — copy drafting

Avoid: SplitMetrics Optimize, Storemaven, Sensor Tower, data.ai — all enterprise-priced and not needed at this stage.

---

## Decision log

| Date | Decision | Rationale |
|---|---|---|
| 2026-05-14 | Re-enable `zoog` brand ASA keyword | 603% ROAS, 7.87% paid CR — highest in portfolio. Brand defense was off, conceding traffic to competitors. |
| 2026-05-14 | Downgrade AppTweak Grow → Essential | Diagnostic phase complete. Essential covers all monitoring needs; save $200/mo. |
| 2026-05-14 | Stay paid-light (no Meta reactivation in Q2) | Per existing GTM posture. Re-evaluate after listing recovery in Q3. |
| 2026-05-14 | Defer App Clip work to Q3 | Bigger scope than current sprint can absorb; not gating recovery. |

---

## Open questions

- [ ] Did anything specific change around April 22–25, 2026? (AppTweak anomaly score spiked to 6.72 — biggest non-noise spike of the year, aligns with the long-tail keyword collapse)
- [ ] What drove the June 6, 2025 anomaly score of 29.25? (Year's biggest spike — possible Apple feature placement, viral moment, or tracking artifact worth understanding for replication)
- [ ] Should we test re-introducing Meta on a recovered chapter-1 paywall lineup before LTV/CAC fully recovers? (Currently deferred per "stay paid-light" decision)
- [ ] Do we need a separate Android ASO plan? (This document is iOS-focused. AppsFlyer data shows iOS dominates installs, but Android merits its own scan.)
