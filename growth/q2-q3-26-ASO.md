> Living tracker for the 90-day ASO & TOFU recovery effort.
> Canonical spec: [`growth/q2-q3-26-ASO.md`](https://github.com/ZoogHQ/.github/blob/main/growth/q2-q3-26-ASO.md)
>
> Check items off as they ship. Add to the Decision log section as you make calls. Add to Open questions as new ones come up.
>
> **Revised May 18, 2026** — Product / engineering / loop items moved to new tracker: **Q2–Q3 2026 Product Growth Loops**.

---## Q2–Q3 2026 ASO & TOFU Recovery Plan

**Created:** May 14, 2026 · **Revised:** May 18, 2026
**Status:** Active
**Owner:** Marketing + Product

---

## Context

Top of funnel collapsed across the past 9 months. App Store installs dropped from a Sep 2024 peak of ~29,000/mo to ~860/mo in April 2026 — a 97% decline. The collapse was driven by stacked failures:

1. **App Store visibility broke late August 2025.** Competitor ASO activity (Khan Academy Kids description rewrite Aug 27, HOMER screenshots Aug 25) expanded their match surface for category keywords while Zoog's listing stood frozen — zero ASO-relevant metadata changes in the entire 12-month window. Apple's algorithm shifted ranking to actively-iterated competitors.
2. **Long-tail keyword universe collapsed late March / early April 2026.** Total ranked keywords dropped from ~120 to ~35. Possibly tied to Apple's March 2026 search ads expansion that pushed organic results down the page. *Update May 2026: no corresponding product-side event signature; treating as App-Store-search-side only.*
3. **Install → paid conversion compressed January 2026.** Meta paused; channel mix shifted to organic (4.4% sub CR vs Meta's 9.4%). Explained, not a funnel break.

Star rating (4.9★) stayed intact — that's the moat to lean on, not the cause.

**Strategic shift:** the listing isn't broken because we broke it. We need to **actively change metadata, build CPPs, ship In-App Events, and submit featuring nominations** — match the cadence competitors set. Sitting on the same listing is the problem.

### Diagnostic update (May 2026)

Investigation of the share-loop funnel using Amplitude clarified the install attribution and surfaced separate product issues:

- **The share loop produces approximately 30% of new creators** today (filtered: New Users firing `Opened using deep link` [view OR recId], then `Click Start Recording` within 30 days). Higher than initially estimated; lower than trailing-12mo numbers suggest because the loop has decayed.
- **The viral coefficient (k)** is approximately **1.4–1.5** when measured correctly — meaningfully above replacement (k>1) but not runaway. Earlier estimates of k ≈ 1.05 were based on undercounted measurement.
- **The April 22–25 long-tail keyword collapse** does not appear in product-side events (Recording Page, deep-link opens, Click Start Recording). Likely visible only in App Store impressions/ranking. P0 investigation deprioritized; this is now an Open Question rather than a blocking diagnostic.
- **The real product-side declines** (Watch → Start Recording, Web Reaction Rate, Request Rate) are caused by changes filed in the new **Q2–Q3 2026 Product Growth Loops** plan. Not ASO issues.

ASO recovery work therefore proceeds with two updates: (1) install volume targets are conservative against current run rate, since meaningful loop recovery depends on the Product Growth Loops fixes; (2) ASO is correctly the dominant install channel post-Meta-pause (~77% of installs) and should be prioritized accordingly.

---

## North-star metrics (90-day target)

| Metric | Today (May 2026) | 90-day target |
|---|---:|---:|
| AppTweak visibility score | -98 | -50 |
| Total ranked keywords | ~35 | 70–90 |
| App Store CR (Imp → DL) | 1–2% | 2.5–3.5% |
| Monthly App Store installs | ~860 | 1,800–2,500 |
| **New creators acquired via App Store (30d post-install)** | (establish baseline) | track + grow |
| In-App Events shipped in 90 days | 0 | 2 (Father's Day + Summer Reading) |
| CPPs live | 0 | 4 |

Revisions vs. original v1 targets: install target reduced from 5,000–8,000 (not supported by benchmarks) to 1,800–2,500 (2–3× current is what credible ASO recovery + 1 featuring placement produces). CR target reduced from 4–6% to 2.5–3.5%. CPP count reduced from 8 to 4. IAE count reduced from "1–2 always running" to "2 shipped in 90 days."

---

## Workstreams

Three parallel tracks. Each has a Week-1 deliverable.

### A. App Store Listing Refresh
### B. Custom Product Pages (CPPs) — 4 personas
### C. In-App Events — Father's Day + Summer Reading
### D. Featuring Nominations
### E. Apple Search Ads (ASA) Hygiene

*Featured-tab segmentation moved to Q2–Q3 2026 Product Growth Loops plan.*

---

## Week 1 (May 12–18) ✅ partially shipped

**Quick wins — most are minutes, all ship this week.**

### A. Listing Refresh
- [ ] Set promotional text (currently empty since Mar 20, 2026) — tie to Father's Day teaser
- [ ] Begin draft of new subtitle (3 variants for future PPO test — defer until install volume supports it)
- [ ] Begin draft of new description following Children-doc 4-arc story (Spark → Hook → Co-create → Child reads)

### B. Custom Product Pages
- [ ] Inventory current CPPs in App Store Connect (expected: 0)
- [ ] Outline CPP taxonomy: **4 use-case CPPs only** — Grandparent Creator, New-Baby/New-Grandparent, Birthday Stories, Long-Distance Family

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

### Cross-cutting measurement
- [ ] **Audit dashboards filtering on `type=view`** — every chart should use `view OR recId` where the warm receive path matters. The Jul 2025 rename + Sep 4 isDeferred instrumentation have been distorting trends for ~9 months.
- [ ] **Document the corrected canonical share-loop metric:**
  ```
  Amplitude New Users segment +
  Opened using deep link (type IN view, recId) →
  Click Start Recording (within 30 days)
  ```

### Tooling
- [ ] Downgrade AppTweak from Grow to Essential ($299 → $99/mo)
- [ ] Confirm Apple PPO is enabled (App Store Connect → Product Page Optimization)
- [ ] Confirm Custom Product Pages module is enabled

---

## Week 2 (May 19–25)

### A. Listing Refresh
- [ ] Finalize new description (final 3,500–4,000 char version)
- [ ] Submit new metadata version to App Store Connect (description ships first; subtitle queued for future PPO test)
- [ ] Update keywords field (100 chars) to add high-intent terms not already covered in name/subtitle: `personalized,grandparent,storybook,bedtime,birthday,family,reading,gift`

### D. Featuring Nominations
- [ ] Submit Summer Reading featuring nomination (target Jun 22 onwards, ~5-week lead)

### Cross-track
- [ ] Pull AppTweak visibility baseline (anchor for measuring lift)
- [ ] Document current screenshot set / preview video for variant comparison

---

## Weeks 3–4 (May 26 – Jun 8) — CPPs (4 personas)

Build the four use-case CPPs from the Children-doc arc. Each needs unique screenshots, copy, and a destination URL.

- [ ] **CPP 1: The Grandparent Creator**
  - [ ] Lead screenshot: grandparent recording for grandchild
  - [ ] Headline: "Personalized Stories from Grandma & Grandpa"
  - [ ] Use as landing page for grandparent-intent ASA campaign (Q3)
- [ ] **CPP 2: New Baby / New Grandchild**
  - [ ] Target the moment when the persona forms (first-time grandparent)
  - [ ] Tie to maternity/paternity content channels
- [ ] **CPP 3: Birthday Stories**
  - [ ] "Happy Birthday" is top-share-rate title at 78%
  - [ ] Lead with personalized birthday card
  - [ ] Use for `birthday story for kids` / `personalized birthday video` keywords
- [ ] **CPP 4: The Long-Distance Family**
  - [ ] Target: military families, immigrant families, divorced families, distant grandparents
  - [ ] Use as landing for relevant content marketing / press

Each: ~1 day design + 2–5 days Apple review. All four shipped by end of Week 4.

### C. In-App Events
- [ ] Father's Day event goes live Jun 7

---

## Weeks 5–6 (Jun 9–22)

### A. Listing Refresh
- [ ] PPO test deferred (insufficient install volume for statistical significance at 860/mo)
- [ ] Refresh promotional text monthly (calendar reminder)

### C. In-App Events
- [ ] Set up second event: **"Summer Reading"** (runs Jun 22 – Jul 31)
  - [ ] Submit for review by Jun 18

### E. ASA
- [ ] Hold on new keyword groups (grandparent-intent, competitor-defense) until brand defense + 2 proven categories are humming at consistent ROAS

### D. Featuring Nominations
- [ ] Submit Back-to-School featuring nomination (target mid-August)

### Invalidation gate (Jun 22)
- [ ] **Check AppTweak visibility score.** If still at -98 with no upward movement by Jun 22, the listing-refresh hypothesis is wrong. Pause CPP work beyond the 4 shipped; escalate to a deeper Apple-side investigation; consider Apple developer relations outreach. Failure mode is recalibration, not stop.

---

## Weeks 7–12 (Jun 23 – Aug 3) — Compound, measure, decide

### A. Listing Refresh
- [ ] Refresh promotional text (monthly cadence)

### C. In-App Events
- [ ] Summer Reading event live through Jul 31

### D. Featuring Nominations
- [ ] Halloween nomination if Father's Day / Summer Reading featuring lands

### Measurement
- [ ] First post-refresh visibility report — measure lift vs Apr 2026 baseline
- [ ] AppTweak monthly competitor scan — flag any major competitor ASO moves
- [ ] Cross-reference paid CR by source (App Store Connect Sources view) — confirm CR is recovering on App Store Search
- [ ] **Track new metric: creators acquired via App Store (30d post-install).** Use Amplitude with the canonical share-loop measurement filter.

---

## Steady-state cadence (after Week 12 / Aug 4 onwards)

- [ ] **Metadata refresh** every 30–45 days (subtitle, screenshot, or description tweak)
- [ ] **In-App Event** always running, tied to next occasion or AI-pipeline content release
- [ ] **Featuring nomination** every 6–8 weeks for upcoming moments
- [ ] **CPP additions** 1–2 new ones per month as use cases warrant — start once first 4 prove out
- [ ] **Competitor metadata check** monthly via AppTweak
- [ ] **AppTweak alert** on visibility-score downgrade (set threshold at -60)

---

## Parallel tracks (filed elsewhere)

| Track | Status |
|---|---|
| Featured-tab segmentation | **Moved to Q2–Q3 2026 Product Growth Loops** |
| Smart App Banner on web viewer | Not yet scoped |
| Open Graph card personalization on shared links | Not yet scoped |
| App Clip evaluation | Decide post Product Growth Loops fixes (Q3) |
| AI-pipeline release marketing playbook | Defer to Month 2 |

---

## Tool stack (target ~$120/mo total)

- **Apple PPO** (free, native) — A/B test icon / screenshots / preview video (paused; insufficient install volume)
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
| 2026-05-14 | Defer App Clip work to Q3 | Bigger scope than current sprint can absorb; not gating recovery. *Updated May 18: re-evaluate post Product Growth Loops fixes.* |
| 2026-05-18 | Move product/loop items to a separate plan (Product Growth Loops) | Diagnostic investigation showed the watch→start and request-rate declines are product/eng caused (Nov 6 incentive modal, Sep 4 iOS bug), not ASO factors. Different owners, different fixes. |
| 2026-05-18 | Reduce CPP count from 8 to 4 | Ship the four highest-conviction personas first; validate before expanding. Avoids over-spending design time on unproven destinations. |
| 2026-05-18 | Deprioritize April 22–25 keyword collapse investigation | No corresponding product-side event in Amplitude. Likely measurement-side or App-Store-search-side only. Address in normal cadence, not as a P0. |
| 2026-05-18 | Revise install target to 1,800–2,500/month | Original 5,000–8,000 implied 6–9× lift from ASO alone; not supported by benchmarks. Realistic ASO + featuring recovery is 2–3× current. |
| 2026-05-18 | Add "creators acquired via App Store (30d)" as a north-star | Ties ASO measurement to viral loop input. Recovering ASO grows new creators, which compounds back into loop volume. |

---

## Open questions

- [ ] Did anything specific change around April 22–25, 2026? (AppTweak anomaly score spiked to 6.72 — biggest non-noise spike of the year. No matching product-side event; likely App Store search-side only.)
- [ ] What drove the June 6, 2025 anomaly score of 29.25? (Year's biggest spike — possible Apple feature placement, viral moment, or tracking artifact worth understanding for replication)
- [ ] Should we test re-introducing Meta on a recovered chapter-1 paywall lineup before LTV/CAC fully recovers? (Currently deferred per "stay paid-light" decision)
- [ ] Do we need a separate Android ASO plan? (This document is iOS-focused. AppsFlyer data shows iOS dominates installs, but Android merits its own scan.)
- [ ] After the Product Growth Loops fixes ship, what's the share-loop install contribution post-correction? (Measurable post-iOS-fix + corrected dashboards.)
- [ ] Does ASA brand defense have headroom to expand, or is `zoog` budget already maxed?
- [ ] What's the true CR (impression → tap → download) in App Store Connect today, broken down by Search vs Browse vs Web Referrer vs App Referrer? (Need access to App Store Connect to answer.)
- [ ] Should we evaluate App Clip post-Product-Growth-Loops fixes? Now that cold-install path will be measurable, can decide on Apple-Clip ROI cleanly.

---

## Cross-references

- **Q2–Q3 2026 Product Growth Loops** — product/eng-side loop fixes (incentive modal rollback, iOS deferred-deep-link, cross-device handoff)
- **Q2–Q3 2026 SEO & Landing Page** → [#19](https://github.com/ZoogHQ/.github/issues/19)
- **Q2–Q3 2026 Organic Social** → [#22](https://github.com/ZoogHQ/.github/issues/22)
- ZoogIOS commit `15f7f203d` — Sep 4, 2025 — iOS deferred-deep-link handler (with bug, tracked in Product Growth Loops)
- ZoogFrontEnd commit `b6c3195` — Nov 6, 2025 — incentive sharing task (regression, tracked in Product Growth Loops)
- Children doc strategic narrative → `https://zooghq.github.io/DataRoom/Children/`
