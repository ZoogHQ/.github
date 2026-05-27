> Living tracker for the 90-day ASO recovery effort.
> Canonical spec: [`growth/q2-q3-26-ASO.md`](https://github.com/ZoogHQ/.github/blob/main/growth/q2-q3-26-ASO.md)
>
> Check items off as they ship. Add to Decision log and Open questions as needed.

# Q2–Q3 2026 ASO Recovery Plan

**Created:** May 14, 2026 · **Revised:** May 25, 2026 (App Store Connect source cross-check)
**Status:** Active
**Owner:** Marketing

---

## Context

App Store installs dropped from a Sep 2024 peak of ~29,000/mo to ~355/mo (May 2026, 99% decline). App Store Connect by-source data identifies the **current bottleneck**:

**Impressions are stable. Tap-through and listing conversion are not.** Since Aug 2025, App Store Search and Browse impressions have held in the ~25–70K/mo range. The bleed is in Imp→PV and PV→DL:

| Source | Imp → PV | PV → DL | Notes |
|---|---:|---:|---|
| App Store Search | **1.1%** (was 4.6% in Mar '25) | 71% (still healthy) | tap-through collapsed; once on page, converts |
| App Store Browse | **1.2%** (was 20.6% in Mar '25) | 3.4% (was 14% in 2024) | both tap-through AND page CR collapsed |
| Web Referrer | 83.9% (definitional) | 36.2% | best-converting source; volume halved (share-loop driven) |
| App Referrer | 79.6% (definitional) | 6.0% | mostly Meta in 2024–25; collapsed when Meta paused |

**App Store Search is now ~57% of first-time downloads** (up from ~13% in Oct 2025) — not because Search got better, but because everything else collapsed. It's the dominant remaining channel and the highest-leverage focus for this plan.

**The diagnosis (revised May 25):** Apple is still showing the listing in search and browse results at roughly historical volumes. People aren't tapping the result, and when they do tap, conversion has degraded (especially on Browse). That's a **tap-through and listing-conversion problem**, not strictly a ranking problem — solvable with the levers we control: app name, subtitle, icon, first screenshot, screenshots 2–5, description above-the-fold, In-App Events for Browse-surface recovery.

**Caveat worth holding:** Apple's "impression" definition counts the listing appearing anywhere in results, regardless of position. So stable impressions are compatible with both (a) ranking intact, listing doesn't compete visually, and (b) ranking dropped, fewer users scroll deep enough to tap. The actions are the same either way; name + subtitle keyword work hedges both.

4.9★ rating is intact — the moat to lean on. The listing isn't broken because we broke it; it's broken because we sat on it while competitors iterated.

**Strategy:** Refresh the metadata that drives tap-through (name, subtitle, icon, first screenshot). Refresh the metadata that drives PV→DL (screenshots 2–5, description top, promotional text). Use In-App Events + featuring as the only available levers for Browse-surface recovery. CPPs serve segmented traffic, not organic tap-through.

---

## North-star metrics (90-day target)

The metrics are framed around the actual bottleneck (tap-through and listing CR), not aggregate CR.

| Metric | Today (May 2026) | 90-day target |
|---|---:|---:|
| ⭐ **App Store Search Imp → PV** (tap-through) | **1.1%** | **3.0–4.0%** (recover toward early-2025 baseline) |
| ⭐ **App Store Browse Imp → PV** (tap-through) | **1.2%** | **5–8%** (will be partly driven by In-App Events) |
| App Store Search PV → DL | 71% | maintain ≥70% (already strong) |
| App Store Browse PV → DL | 3.4% | 8–12% (needs screenshot + description work) |
| AppTweak visibility score | -98 | -50 |
| Total ranked keywords | ~35 | 70–90 |
| Monthly App Store installs (all sources) | ~355 | 900–1,200 (ASO levers only; excludes share-loop or Meta recovery) |
| In-App Events shipped in 90 days | 0 | 2 (Father's Day + Summer Reading) |
| CPPs live | 0 | 4 |
| Featuring placements landed | 0 | ≥1 |

---

## Workstreams

- **A.** Tap-through metadata (name, subtitle, icon, first screenshot) — Imp→PV lever
- **B.** Listing-conversion metadata (screenshots 2–5, description, promotional text) — PV→DL lever
- **C.** In-App Events — Father's Day + Summer Reading (Browse-surface recovery)
- **D.** Featuring Nominations (Browse-surface recovery)
- **E.** Custom Product Pages — 4 personas (segmented traffic, not organic)
- **F.** Apple Search Ads Hygiene

---

## Week 1 (May 12–18) — tap-through fix sprint

### A. Tap-through metadata — **P0**

The current name + subtitle spend 60 characters of the highest-weighted indexed real estate on keywords that don't match Zoog's actual intent (Books, Songs, E-Cards, Bond, Through, Singing). Tap-through can't recover without changing this.

- [ ] **Draft 3–4 app name variants** to replace current "Zoog: Books, Songs, E-Cards" (30 char limit). Anchor on the strongest broad keyword. Candidates:
  - "Zoog: Personalized Storybooks"
  - "Zoog: Stories from Family"
  - "Zoog: Storybooks for Kids"
- [ ] **Draft 3–4 subtitle variants** to replace current "Bond Through Reading & Singing" (30 char limit). Anchor on the second strongest keyword + intent. Candidates:
  - "Stories from Grandma & Grandpa"
  - "Personalized family stories"
  - "Bedtime stories for grandkids"
- [ ] **AppTweak keyword volume + difficulty check** on the candidate keywords (personalized, storybook, storytime, family stories, grandparent). Pick the highest-volume term where Zoog can plausibly reach page 1.
- [ ] **PickFu validation** (~$40): 2 polls — name + subtitle. 50 votes each, parent/grandparent audience.
- [ ] **First screenshot redesign brief.** First screenshot drives tap-through more than any other visual. Goal: in 1 second, communicate "personalized stories from family" with strong copy + face/emotion.
- [ ] **Icon refresh evaluation.** Compare current icon to top-5 search competitors for kids storybook keywords. Decide refresh vs. iterate.

### C. In-App Events (Father's Day — Jun 21 hard deadline)
- [ ] Build "Stories from Dad" event (Father's Day, Jun 7–21)
  - Event copy: name (30 chars), short (50 chars), long (120 chars)
  - Hero image / video
  - Event type: Special Event
  - Submit for review by May 21 (3-day Apple review)

### D. Featuring nominations (lead-time-bound)
- [ ] Submit Father's Day nomination via App Store Connect → Promote your app
  - Hook: 4.9★ / 20K+ ratings, AR filters, grandparent creator angle
  - Target placement: Jun 14–21

### F. ASA
- [x] Re-enable `zoog` brand keyword
- [ ] Re-enable `zoog magical storytime` brand keyword
- [ ] Pause zero-paid keywords: `reading app for kids`, `read aloud kids`, `bookful`, `kids reading games`, `children story app`, `bedtime stories` (if 0 paid), `interactive kids stories` (if 0 paid)
- [ ] Concentrate budget on `zoog` + `kids books` + `storybook app`

### Tooling
- [ ] Downgrade AppTweak Grow → Essential ($299 → $99/mo)
- [ ] Confirm PPO + CPP modules enabled in App Store Connect

---

## Week 2 (May 19–25) — submit + listing-conversion drafts

### A. Tap-through metadata
- [ ] **Finalize name + subtitle** from Week 1 PickFu winner + AppTweak volume check
- [ ] **Submit app version** with new name + subtitle + updated keywords field (100 chars): `personalized,grandparent,storybook,bedtime,birthday,family,reading,gift` (drop terms duplicated by name/subtitle)
- [ ] **Submit first screenshot redesign** as part of the version
- [ ] Set promotional text (empty since Mar 20) — Father's Day teaser

### B. Listing-conversion metadata
- [ ] **Draft description top-3-lines.** These are the only lines visible before "more" — the entire PV→DL lift on description sits here. Children-doc 4-arc story (Spark → Hook → Co-create → Child reads) compressed into first 3 lines.
- [ ] **Draft full description** (3,500–4,000 chars) for the same submission as Week 2 name/subtitle/screenshot.

### D. Featuring
- [ ] Submit Summer Reading nomination (target Jun 22+, 5-week lead)

### Measurement
- [ ] Pull AppTweak visibility baseline + current keyword rankings
- [ ] Snapshot current screenshots / preview video for before-after comparison
- [ ] Set baseline: Imp→PV by source (current: Search 1.1%, Browse 1.2%); PV→DL by source (current: Search 71%, Browse 3.4%)

### E. CPPs
- [ ] Inventory current CPPs in App Store Connect (expected: 0)
- [ ] Finalize CPP taxonomy: Grandparent Creator · New-Baby/New-Grandparent · Birthday Stories · Long-Distance Family

---

## Weeks 3–4 (May 26 – Jun 8) — ship screenshots 2–5 + 4 CPPs

### B. Listing-conversion metadata
- [ ] **Screenshots 2–5 redesign.** Each screenshot answers one objection or feature highlight. Order driven by PV→DL psychology: 1=hook (done Week 2), 2=who-makes-this (grandparent angle), 3=how-it-works (record + AR magic), 4=social proof (4.9★ / reviews), 5=variety/library breadth.
- [ ] **Preview video refresh** (optional Week 4 if capacity): 15–30s vertical, showing the family-record-to-watch loop.

### E. CPPs

Each CPP: ~1 day design + 2–5 days Apple review. All four shipped by end of Week 4.

- [ ] **CPP 1: Grandparent Creator**
  - Lead: grandparent recording for grandchild
  - Headline: "Personalized Stories from Grandma & Grandpa"
  - Use for: grandparent-intent ASA (Q3)
- [ ] **CPP 2: New Baby / New Grandchild**
  - Target the moment the persona forms (first-time grandparent)
  - Use for: maternity/paternity content channels
- [ ] **CPP 3: Birthday Stories**
  - "Happy Birthday" is top-share-rate title
  - Use for: `birthday story for kids`, `personalized birthday video`
- [ ] **CPP 4: Long-Distance Family**
  - Target: military, immigrant, divorced families, distant grandparents
  - Use for: content marketing / press landings

### C. In-App Events
- [ ] Father's Day event live Jun 7

---

## Weeks 5–6 (Jun 9–22) — first measurement read

### A. Tap-through metadata
- [ ] Refresh promotional text monthly (Father's Day → Summer Reading transition)
- PPO (icon / screenshots / preview video A/B) deferred — insufficient install volume for significance; revisit at 3K+/mo. Note: Apple PPO does not support subtitle or description A/B testing — those are sequential changes only.

### C. In-App Events
- [ ] Submit Summer Reading event (runs Jun 22 – Jul 31) by Jun 18

### D. Featuring
- [ ] Submit Back-to-School nomination (target mid-August)

### Measurement — first read on the new listing
- [ ] **Imp → PV by source** (Search, Browse) — was 1.1% / 1.2%. Apple's re-indexing should be reflected within 1–2 weeks of submission. Expect Search to move faster than Browse.
- [ ] **PV → DL by source** — was 71% Search, 3.4% Browse. Screenshot + description changes should lift both.
- [ ] **AppTweak ranked keywords** — should grow as name/subtitle pull in new keyword clusters.

### Invalidation gate (Jun 22)
- [ ] Check primary metrics: **Search Imp→PV** and **Browse Imp→PV**. If both are still ≤1.5% by Jun 22 (no meaningful lift after 3+ weeks of new metadata), the tap-through hypothesis is incomplete — likely a ranking-position issue Apple hasn't reflected in impression volumes, OR the new variants didn't outperform the old. Pause CPPs beyond the 4 shipped; escalate to deeper Apple-side investigation; consider Apple developer relations outreach.
- [ ] Secondary gate: if Search Imp→PV lifted but Browse remained flat, that's expected — Browse needs the In-App Events + featuring to surface. Treat as on-track, not failure.

---

## Weeks 7–12 (Jun 23 – Aug 3)

### A. Tap-through metadata
- [ ] Monthly promotional text refresh
- [ ] **Second submission window (early Jul):** if Week 5–6 reads show subtitle is underperforming, swap with second-place PickFu variant. Subtitle can only change at app submission, so coordinate with eng release cadence.

### C. In-App Events
- [ ] Summer Reading live through Jul 31

### D. Featuring
- [ ] Halloween nomination if Father's Day or Summer Reading featuring landed

### Measurement
- [ ] First post-refresh visibility report — lift vs April 2026 baseline
- [ ] Monthly AppTweak competitor scan — flag major competitor ASO moves
- [ ] Monthly Imp→PV and PV→DL by source — track recovery toward 90-day targets
- [ ] **Cross-reference Web Referrer downloads with Product Growth Loops doc** — Web Ref is the share-loop scorecard there; tracking jointly keeps the two plans aligned

---

## Steady-state cadence (Aug 4 onwards)

- [ ] Metadata refresh every 30–45 days
- [ ] Always one In-App Event running
- [ ] Featuring nomination every 6–8 weeks
- [ ] 1–2 new CPPs per month once first 4 prove out
- [ ] Monthly competitor metadata check via AppTweak
- [ ] AppTweak alert: visibility-score downgrade < -60

---

## Parallel tracks (filed elsewhere or deferred)

| Track | Status |
|---|---|
| Smart App Banner on web viewer | Not yet scoped |
| OG card personalization on share links | Not yet scoped |
| App Clip evaluation | Decide Q3 |
| AI-pipeline release marketing playbook | Defer to Month 2 |

---

## Tool stack (target ~$120/mo)

- **Apple PPO** (free, native) — A/B test icon / screenshots / preview video
- **Apple Custom Product Pages** (free, native) — up to 70 use-case landing pages
- **Apple In-App Events** (free, native)
- **AppTweak Essential** ($99/mo) — keyword + competitor monitoring
- **Figma** (free) — screenshot design
- **PickFu** (~$20/mo) — pre-launch screenshot validation
- **Claude / ChatGPT** ($20/mo) — copy drafting

Avoid: SplitMetrics Optimize, Storemaven, Sensor Tower, data.ai — enterprise-priced, not needed at this stage.

---

## Decision log

| Date | Decision | Rationale |
|---|---|---|
| 2026-05-14 | Re-enable `zoog` brand ASA keyword | 603% ROAS, 7.87% paid CR — highest in portfolio. Brand defense was off, conceding traffic to competitors. |
| 2026-05-14 | Downgrade AppTweak Grow → Essential | Diagnostic phase complete. Save $200/mo. |
| 2026-05-14 | Stay paid-light (no Meta reactivation in Q2) | Existing GTM posture. Re-evaluate Q3 after listing recovery. |
| 2026-05-14 | Defer App Clip to Q3 | Scope too big for current sprint; not gating recovery. |
| 2026-05-18 | Reduce CPP count from 8 to 4 | Ship the four highest-conviction personas; validate before expanding. |
| 2026-05-18 | Defer PPO testing | Insufficient install volume (~355/mo) for statistical significance. Revisit at 3K+/mo. |
| 2026-05-18 | Revise install target 5,000–8,000 → 1,800–2,500 | Original target implied 6–9× lift from ASO alone; not benchmark-supported. Realistic ASO + featuring is 2–3×. |
| 2026-05-25 | Recenter plan on tap-through (Imp→PV), not aggregate CR | App Store Connect source breakdown showed impressions are stable since Aug 2025; tap-through collapsed from 4.6%/20.6% (Search/Browse) to 1.1%/1.2%. The lever set changes: name + subtitle + icon + first screenshot lead; description and remaining screenshots second; CPPs third. |
| 2026-05-25 | Update app name + subtitle as Week 1 P0 | Current "Zoog: Books, Songs, E-Cards" + "Bond Through Reading & Singing" spend 60 chars of the highest-weighted indexed real estate on keywords that don't match Zoog's intent. Highest single ASO lever. |
| 2026-05-25 | Revise 90-day install target 1,800–2,500 → 900–1,200 | Previous target assumed share-loop recovery in the ASO numbers. With share-loop separated to Product Growth Loops doc and Meta resumption out-of-scope, ASO-only realistic target is ~3× of current. |

---

## Open questions

- [ ] Did anything specific change around April 22–25, 2026? AppTweak anomaly spiked; no matching product-side event. Likely App Store search-side only.
- [ ] What drove the June 6, 2025 anomaly score of 29.25? Possible Apple feature placement worth understanding for replication.
- [ ] Re-introduce Meta on a recovered chapter-1 paywall lineup before LTV/CAC fully recovers?
- [ ] Separate Android ASO plan needed? iOS dominates installs but Android merits its own scan.
- [ ] ASA brand defense headroom — is `zoog` budget already maxed?
- [ ] **Ranking position vs impression volume** — Apple's impression count includes any-position appearances. AppTweak ranked-keywords data is the proxy for actual position. Worth periodically cross-referencing: are impressions stable because ranking is intact, or because we still appear deep in long-tail results that fewer users scroll to?

---

## Cross-references

- **Q2–Q3 2026 Product Growth Loops** → [#24](https://github.com/ZoogHQ/.github/issues/24) — product/eng-side loop fixes
- **Q2–Q3 2026 SEO & Landing Page** → [#19](https://github.com/ZoogHQ/.github/issues/19)
- **Q2–Q3 2026 Organic Social** → [#22](https://github.com/ZoogHQ/.github/issues/22)
- Children doc strategic narrative → `https://zooghq.github.io/DataRoom/Children/`
