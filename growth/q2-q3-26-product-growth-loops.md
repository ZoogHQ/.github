# Q2–Q3 2026 Product Growth Loops Plan

**Created:** May 18, 2026 · **Revised:** May 25, 2026 (App Store Connect cross-check; revised attribution)
**Status:** Active
**Owner:** Product + Engineering
**Companion plans:**
- [`q2-q3-26-ASO.md`](https://github.com/ZoogHQ/.github/issues/18) — App Store / ASA / In-App Events / CPPs / Featuring
- [`q2-q3-26-SEO+landing-page-optimization.md`](https://github.com/ZoogHQ/.github/issues/19) — Marketing site, SEO, email, attribution
- [`q2-q3-26-organic-social.md`](https://github.com/ZoogHQ/.github/issues/22) — Organic social channels

---

## Context

The install collapse from ~29K/mo (Sep 2024) to ~355/mo (May 2026) is the product of **three stacked breaks with different causes**. This doc tracks the product / engineering subset; the ASO plan tracks the listing subset.

**Primary driver: Meta wind-down + pause (Nov 2025 – Jan 2026).** App Store Connect App Referrer downloads collapsed from 9,479 (Oct '25) → 3,072 (Nov) → 2,145 (Dec) → 73 (Jan '26) — a 99% collapse. App Referrer is almost entirely Meta-driven traffic (taps from Instagram/Facebook in-app contexts). This is paid-media-driven and out of scope for this plan. It is, however, the dominant cause of the share-loop INPUT collapse: fewer paid installs → fewer creators in the system → fewer shares produced each month → fewer share-loop installs downstream. The share loop didn't fundamentally break; its input volume collapsed.

**Secondary driver: Share-loop conversion-rate degradation.** The share-loop funnel has degraded modestly through 2025 even on a per-cohort basis. The PRIMARY METRIC — Open From Deep Link [New User] → Share — sits at 36.3% and is trending down. This IS a product / engineering issue and is what this plan exists to fix. Two specific, independently fixable regressions contribute:

### Area 1 — Web request-rate degradation (Nov 2025)

On Nov 6, 2025 (ZoogFrontEnd commit `b6c3195` "incentive sharing task"), the web Recording Page request flow was rebuilt to insert an "incentive sharing" modal after the user selects a book to request. The modal occupies the screen, interrupts the natural engagement loop, and either suppresses the `User Requested Content` event from firing reliably or trains recipients to avoid the request action.

**Data signature:**
- Web request rate (Click Play Recording → User Requested Content): **20.6% (Sep '25) → 13.5% (Apr '26)** — a 35% relative drop, stepwise from Nov 2025
- Web like rate (Click Play Recording → User clicks the heart): essentially flat (5.2% → 4.0%) — confirms it's not a global reaction issue
- Mobile request rate (Reactions View → User Requested Content): stable or improving across personas — confirms it's not content quality
- Click Download events Oct→Nov ratio (1,564 → 1,398, -11%) is slightly elevated vs the gentle baseline decline — consistent with the modal contributing a small additional drag

**Scope correction (May 25):** Earlier framing put this Nov 6 regression as a primary driver of install collapse. Cross-check against App Store Connect Web Referrer downloads + Amplitude Click Download events shows the trajectory tracks Meta-driven creator-pool shrinkage much more closely than a single-commit cliff. The modal is still a real regression worth rolling back (highest-leverage product fix on the table; ~35% relative drop on a key funnel step), but its install-volume impact is meaningfully smaller than the Meta-driven input collapse.

**Supporting charts:**
- [Web Reaction Rate — total (Click Play → any reaction)](https://app.amplitude.com/analytics/zoog/chart/vjj0fmf/edit/fkgvu72t)
- [Web Likes rate (Click Play → User clicks the heart)](https://app.amplitude.com/analytics/zoog/chart/kj0tz5d2?sharingId=zg2jh9-A) — control: barely moved
- [Web Requests rate (Click Play → User Requested Content)](https://app.amplitude.com/analytics/zoog/chart/04nsaypt?sharingId=59DZWtQ4) — the 35% drop
- [Mobile Requests by persona (Reactions View → User Requested Content)](https://app.amplitude.com/analytics/zoog/chart/zn63vkhp/edit/zpaa1k0a) — control: stable across personas, rules out content quality

### Area 2 — Share-loop CR per-cohort decline (across 2025)

Independent of input volume, the share-loop's per-cohort conversion has degraded. The PRIMARY METRIC (Open From Deep Link [New User] → Share, 36.3% trending down) is the cleanest signal. Specific inflection points on the new-user web `Recording Page → User selected share option` funnel:

- **Aug 2025:** Firebase Dynamic Links shutdown (Aug 25, 2025). Frontend was mid-migration to AppsFlyer (deeplink.service.ts commits Aug 22 + Sep 4). iOS-side reverts on the same day. Web share-button URL generation may have shifted. Investigation pending (workstream E).
- **Dec 2025:** Possibly the cohort-lagged effect of the Nov 6 incentive modal compounding into share behavior. Also potentially the Dec 7 `reverted runmediflowv2` iOS commit. Investigation pending (workstream E).
- **Feb 2026 onwards:** Steady state of the degraded loop.

### Plus: iOS deferred-deep-link condition bug (Sep 4, 2025)

A separate bug in `AppDelegate+AppsFlyer.swift` (commit `15f7f203d`). The deferred deep-link handler has an inverted condition that suppresses the `Opened using deep link {type: "view", isDeferred: true}` event for most cold installs — and as a side effect, fails to route the user to the recording they were trying to view. Capture rate currently ~65/month vs an estimated 200–400 expected.

**Supporting charts:**
- [Share-loop conversion split by isDeferred (Nov 25 – today)](https://app.amplitude.com/analytics/zoog/chart/yw858t7o?sharingId=O5suxM0j) — isDeferred=true cohort converts much worse and on smaller base than isDeferred=false
- [Total Download clicks vs first-time deep-link opens (the ratio flip)](https://app.amplitude.com/analytics/zoog/chart/4amqn4gt?sharingId=mxpVte8F) — pre-Sep 2025: 1st-time opens > download clicks; post-Sep: the ratio flips
- [Opened using deep link by `type` over time](https://app.amplitude.com/analytics/zoog/chart/sz173rgr?sharingId=KsO0_yd_) — Jul 2025 view→recId rename (measurement artifact, distinct from this bug)
- [isDeferred=true monthly uniques (Sep '25 onward)](https://app.amplitude.com/analytics/zoog/chart/new/4o8szj36) — ~65/month in Apr 2026; the floor the fix should lift

### Plus: cross-device identity gap (structural)

There's no web → iOS device_id handoff in the OneLink URL. Every web visitor and every post-install user lives under separate `amplitude_id` entries with no merge logic outside of post-install email-match sign-in. Cohort analysis across surfaces is materially distorted; the loop's true install contribution is not measurable without a fix.

---

## Install-channel attribution (App Store Connect cross-check)

Cross-referencing App Store Connect's source-attributed downloads with Amplitude validates two things and recasts the diagnosis:

**1. Web Referrer downloads ≈ Recording-Page "Click Download" funnel.** From Nov 2025 onward, App Store Connect Web Referrer Page Views and the Amplitude `User clicks download Zoog` event track each other within ~5%:

| Month | Click DL (Amplitude) | Web Ref PV (ASC) | Web Ref DLs |
|---|---:|---:|---:|
| 2025-10 | 1,564 | 2,174 | 900 |
| 2025-11 | 1,398 | 1,351 | 611 |
| 2025-12 | 1,266 | 1,268 | 454 |
| 2026-01 | 797 | 781 | 277 |
| 2026-04 | 428 | 465 | 150 |
| 2026-05 | 275 | 312 | 113 |

This identity holds because iMessage taps (the dominant share channel) open in Safari → web viewer → "Get the App" → App Store via **Web Referrer**. So Web Referrer downloads in App Store Connect are effectively the share-loop install scorecard, independent of any Amplitude instrumentation. Pre-Nov 2025, Web Ref PV was 15–40% higher than Click DL — some other web source (landing page / blog / smart app banner) was contributing ~300–600 PV/mo and stopped in Nov; worth identifying separately.

**2. App Referrer downloads ≈ Meta-driven installs.** Instagram / Facebook in-app browsers route their taps as App Referrer in App Store Connect. The Oct '25 → Jan '26 collapse (9,479 → 73) tracks Meta wind-down + pause precisely. App Referrer recovery is a paid-media decision and not gated by this plan.

**Implication for measurement:** Going forward, **Web Referrer monthly downloads** are the cleanest install-side scorecard for share-loop health. We don't need to wait on Amplitude instrumentation fixes to track whether the loop is recovering.

---

## Canonical share-loop funnels (new users firing `Opened using deep link` with `type IN view, recId`)

Four saved funnels measure share-loop health, each filtered to Amplitude's "New Users" segment so the cohort is share-loop-attributable.

### Open From Deep Link [New User] → View

The "did the recipient actually engage with what was sent" rate.

- **Latest completed month: 89.1%** of new users firing Opened using deep link go on to Watch Recording View (same-day, 1-day conversion window)
- **Trend:** healthy and stable through Q4 2025, declining from December, **trending back up since April 2026**
- The post-event flow is healthy — when a new user reaches the in-app deep-link step, the experience routes them to the recording reliably
- Chart: [Open From Deep Link [New User] > View](https://app.amplitude.com/analytics/zoog/chart/gx6j5gy7?linkingDashboardId=227vmg5l&sharingId=meht_Lbc)

### Open From Deep Link [New User] → React

The "did the recipient react (like / laugh / wow / hug) to what they watched" rate. This is one of the two engagement signals that captures the Nov 2025 incentive-modal damage.

- **Latest completed month: 6.93%** of new deep-link users go on to fire User reacted to video (3-step funnel: Deep link → Watch → React)
- Chart: [Open From Deep Link [New User] > React](https://app.amplitude.com/analytics/zoog/chart/m3zdpxlx?sharingId=lGqMd4--)

### Open From Deep Link [New User] → Request Content

The "did the recipient ask for another Zoog" rate — leading indicator of healthy loop engagement. The Nov 2025 regression hits hardest here.

- **Latest completed month: ~18%** (3-step funnel: Deep link → Watch → Request)
- **Trend:** trending up — partial recovery signal worth tracking
- Chart: [Open From Deep Link [New User] > Request Content](https://app.amplitude.com/analytics/zoog/chart/rt4w937f?sharingId=unWLNeJT)

### Open From Deep Link [New User] → Share ⭐ **PRIMARY METRIC**

The "did the recipient become a re-sharer themselves" rate — the loop's regenerative output. **This is the metric this plan exists to fix.**

- **Latest completed month: 36.3%** of new deep-link openers go on to User selected share option
- **Trend: declining** — this is the metric that quantifies the loop's regenerative health and where the Nov 2025 + Dec 2025 + Feb 2026 inflections compound
- Split by `isDeferred` shows: cold-install (isDeferred=true) cohort converts much worse (5–28%) than warm-on-first-session (25–41%) — both decline through the year
- Charts:
  - [Open From Deep Link [New User] > Share](https://app.amplitude.com/analytics/zoog/chart/fxcpr11c)
  - [Same funnel split by isDeferred](https://app.amplitude.com/analytics/zoog/chart/yw858t7o?sharingId=O5suxM0j)

> **Suggested dashboard:** group all four into a `Share Loop · Deep Link (New User) Funnels` dashboard alongside the existing `Growth Loops` dashboard ([227vmg5l](https://app.amplitude.com/analytics/zoog/dashboard/227vmg5l)) for ongoing monitoring.

---

## North-star metrics (90-day target)

| Metric | Today (Apr/May 2026) | 90-day target |
|---|---:|---:|
| ⭐ **Open From Deep Link [New User] → Share** (loop CR) | **36.3% (declining)** | **stop the decline, return to growth, reach ≥45%** |
| 🎯 **Web Referrer monthly downloads** (loop channel scorecard) | **113 (May '26)** | **300–400** (recover toward Oct '25 baseline of ~900) |
| Web request rate (mobile-web) | 13.5% | **18–20%** (recover to pre-Nov baseline) |
| Watch → Click Start Recording (new users via deep-link) | 31% | **45–50%** (recover to pre-Nov baseline) |
| Open From Deep Link [New User] → View | 89.1% (recovering) | maintain ≥90% |
| Open From Deep Link [New User] → React | 6.93% | recover toward pre-Nov baseline |
| Open From Deep Link [New User] → Request Content | ~18% (trending up) | continue upward; ≥22% |
| isDeferred=true monthly events (cold-install attribution) | ~65 | **200–400** (post iOS fix) |
| Click handlers with analytics coverage | 2 of 4 | 4 of 4 |
| Cross-device merge rate (web visitor → iOS install) | unknown | measurable + tracked |

> **Note on Web Referrer downloads target.** Pre-collapse baseline was ~900/mo (Oct 2025) before share-loop CR degradation compounded with creator-pool shrinkage from Meta pause. The 300–400 target assumes the Nov 6 modal rollback + iOS DDL fix lift per-cohort CR, but does NOT assume Meta resumption (which would lift the input). Full recovery to ~900/mo requires both.

---

## Workstreams

Five tracks. A is the urgent rollback. B is the iOS code fix. C–E are follow-on improvements.

### A. Web Recording Page UX recovery
### B. iOS deep-link infrastructure
### C. Cross-device identity handoff
### D. Measurement & instrumentation gaps
### E. Diagnostic investigations (Aug + Dec inflections)

---

## Week 1 (May 18–24) — the two urgent fixes

### A. Web Recording Page UX recovery — **P0**

- [ ] **Feature-flag the Nov 6 incentive modal off by default.** Wrap `incentiveModelCreate()` call sites in `video-home.component.ts` (lines ~4527 and ~4547) behind a remote-config flag. Default: disabled.
- [ ] **Deploy to QA, validate** that web request flow completes without the modal interrupting. Confirm `User Requested Content` event fires synchronously with book selection.
- [ ] **Deploy to production.**
- [ ] **Watch dashboards Day 1–7:** request rate, like rate, Watch → Start Recording conversion. Expected lift: requests recover toward 18–20% within 2 weeks.

### B. iOS deep-link infrastructure — **P0**

- [ ] **Fix the inverted condition in `AppDelegate+AppsFlyer.swift`** (commit `15f7f203d`, function `onConversionDataSuccess`). Handle both AppsFlyer payload shapes:
  ```swift
  if let dlValue = installData["deep_link_value"] as? String, dlValue == "view",
     let recId = installData["deep_link_sub1"] as? String {
      // canonical OneLink click + install path
      Analytics.shared.log(.universalLinkReceived(link: "", type: "view", 
          userId: ZoogSession.shared.user?.id, isDeferred: true))
      NotificationCenter.default.post(name: .receiveDeeplinkToOpenBeforeLogin, object: recId)
  } else if let recId = installData["view"] as? String {
      // legacy af_dp-flattened path (currently the only one firing)
      Analytics.shared.log(.universalLinkReceived(link: "", type: "view", 
          userId: ZoogSession.shared.user?.id, isDeferred: true))
      NotificationCenter.default.post(name: .receiveDeeplinkToOpenBeforeLogin, object: recId)
  }
  ```
- [ ] **Submit iOS app version** with the fix. Allow ~24h Apple review + ~3 days for adoption.
- [ ] **Validate via Amplitude:** `Opened using deep link {type=view, isDeferred=true}` monthly volume should rise from ~65 toward 200–400 within 14 days of full adoption.

---

## Weeks 2–3 (May 25 – Jun 7) — measurement gaps + initial diagnostics

### D. Measurement & instrumentation gaps

- [ ] **Add analytics to `openAppStore()`** (`video-home.component.ts:3532`):
  ```typescript
  openAppStore() {
    this.analytic.analyticTrack("User click open in app", {
      ...JSON.parse(localStorage.getItem("amplitudeDefaultProperties")),
      recordingId: this.recId,
      surface: "after_watching_or_seasonal_popup"
    });
    this.deeplinkService.redirectToApp();
  }
  ```
  (Note: this is dead code today — `parent_after_div` is desktop-only with an iOS-only button inside. Adding the analytic prepares for any future revival of the popup.)
- [ ] **Add analytics to `GetAppComponent.ngOnInit`** (`get-app.component.ts:66`) for any direct hits to the `/get/app` route.
- [ ] **Audit Amplitude Custom Event `User clicks download Zoog`** definition to ensure new analytics fire into it.
- [ ] **Dashboards using `type=view` filter** — confirm all critical dashboards use `view OR recId` where appropriate (warm + cold path combined). The Sep 2025 rename has been distorting trends for ~9 months.

### E. Diagnostic investigation — Aug 2025 inflection (Area 2)

- [ ] **Audit the web "User selected share option" event firing path.** What URL does the web share button generate, and did that change around Aug 25, 2025?
- [ ] **Cross-reference frontend commits Aug 15 – Sep 10, 2025** with the share-button code. Look specifically for:
  - Firebase Dynamic Links removal in the share button (if it used DDL pre-shutdown)
  - Changes to the share URL format
  - Changes to event-firing logic in `User selected share option`
- [ ] **Document findings.** Decide whether this is a fixable regression or a structural change that's just observable now.

---

## Weeks 4–6 (Jun 8–28) — A/B re-test + Dec inflection diagnostic

### A. Web Recording Page UX — re-test the incentive modal

- [ ] **Build A/B routing** for the incentive modal via Vercel/Cloudflare or feature flag service.
- [ ] **Run a 2–4 week A/B test** with two cohorts:
  - Control: modal disabled (recovery baseline)
  - Treatment: modal enabled (Nov 6 design)
  - Optional second treatment: redesigned modal (less intrusive — e.g., post-watch toast instead of mid-flow modal)
- [ ] **Primary metric:** requests rate. **Secondary:** likes, Watch → Start Recording, install rate, Day 7 retention.
- [ ] **Decision criteria:** modal must lift downstream sharing AND not degrade requests > 10%. If not, kill it permanently or pivot to a non-intrusive design.

### E. Diagnostic investigation — Dec 2025 inflection (Area 2)

- [ ] **iOS commit audit Nov 1 – Dec 31, 2025.** Look at `Record*`, `Share*`, `MediaFlow*`, `WatchView*` paths. Specifically:
  - `b6c3195` ripple effects in iOS (any iOS-side incentive-related code)
  - Nov 5 `mediaflowcallerv2` rollout (`20468bb73`)
  - Nov 12 `added debug logs` (`382535070`)
  - Dec 7 `reverted runmediflowv2` (`6ae29aaea`)
- [ ] **Verify share-screen UX** for new users on iOS for any regressions in the Nov–Dec window.
- [ ] **Document findings.** Decide whether a fix exists.

---

## Weeks 7–10 (Jun 29 – Jul 26) — cross-device identity

### C. Web → iOS device_id handoff

- [ ] **Frontend (`deeplink.service.ts`):** add Amplitude device_id to the OneLink params. Use either:
  ```typescript
  af_sub1: amplitude.getInstance().options.deviceId,
  // or
  deep_link_sub2: amplitude.getInstance().options.deviceId,
  ```
- [ ] **iOS (`AppDelegate+AppsFlyer.swift`):** on first-launch deferred deep link, read the device_id from AppsFlyer conversion data and call `Amplitude.instance().setDeviceId(<webDeviceId>)` **before the first event fires**.
- [ ] **Validate:** check that the web amplitude_id and post-install iOS amplitude_id are now the SAME for share-loop installs. Cohort analysis (web → install) should now show the full timeline for the same `amplitude_id`.
- [ ] **Rebuild any web→app cohort dashboards** to use the unified identity.

### Continuing measurement

- [ ] **Monthly health check** on the canonical share-loop metric:
  ```
  New Users firing Opened using deep link (view OR recId) 
  → Watch Recording View 
  → Click Start Recording (within 30 days)
  ```

---

## Weeks 11–12 (Jul 27 – Aug 9) — verification + strategic next bets

- [ ] **Verify all targets:** request rate ≥18%, Watch → Start ≥45%, isDeferred=true ≥200/month, cross-device merge tracked
- [ ] **Document share-loop install contribution** with the corrected measurement. Use this to inform Q4 planning.
- [ ] **Decide on App Clip evaluation** (deferred from ASO plan). Now that the cold-install path is fixed and measurable, evaluate whether App Clip is needed or if the existing flow suffices.
- [ ] **Decide on Tier 1 creator-incentivization product spec** (`growth/specs/creator-incentivization-tier1.md`). Originally specced before the diagnostic work; revisit in light of corrected loop math.

---

## Steady-state cadence (after Week 12 / Aug 10 onwards)

- [ ] **Weekly review** of canonical share-loop metric and request rate
- [ ] **Monthly review** of cross-device merge rate, isDeferred=true volume
- [ ] **Any new feature affecting the recording page** must be A/B tested behind a feature flag — never ship without measurement
- [ ] **Quarterly audit** of click handlers and analytics coverage to prevent measurement gaps from recurring
- [ ] **iOS deep-link integration** — verify deferred attribution still works after any iOS SDK upgrade or AppsFlyer SDK upgrade

---

## Decision log

| Date | Decision | Rationale |
|---|---|---|
| 2026-05-18 | Separate product/eng growth loop issues from the ASO plan | Investigation showed the watch→start and request-rate declines are caused by product/eng changes (Nov 6 incentive modal, Sep 4 iOS bug), not by ASO factors. Different owners, different fixes. |
| 2026-05-18 | Feature-flag the Nov 6 incentive modal off | 35% drop in web requests, traced to commit `b6c3195`. Highest-leverage fix on the table. |
| 2026-05-18 | Fix iOS deferred-deep-link condition | Inverted condition in commit `15f7f203d` suppresses most cold-install events. Single-line fix. |
| 2026-05-18 | Defer Web → iOS device_id handoff to Week 7+ | Important strategic improvement but not blocking. Higher-impact fixes ship first. |
| 2026-05-18 | Defer App Clip and Tier 1 creator-incentivization decisions until Aug | Both depend on corrected loop math, which we won't have until the Week 1 fixes have run for ~30 days. |
| 2026-05-25 | Re-attribute App Referrer collapse to Meta wind-down | App Store Connect cross-check showed App Referrer (Instagram/Facebook in-app context) tracked Meta spend precisely. Removes the framing of "the share loop broke as a channel." Share loop CR is degraded (real, fixable here); share loop INPUT collapsed (driven by paid wind-down, not gated by this plan). |
| 2026-05-25 | Adopt Web Referrer monthly downloads as the install-side scorecard for share-loop health | Validated identity: ASC Web Referrer PV ≈ Amplitude Click Download events (~95% alignment Nov '25 onward), driven by iMessage→Safari→App Store path. Gives us a clean install measurement that doesn't depend on Amplitude instrumentation. |

---

## Open questions

- [ ] What does the SECOND treatment look like for the incentive modal A/B test? (Less intrusive design — toast? Post-share confirmation? Card on the home page?)
- [ ] After the iOS deferred-deep-link fix, what's the true cold-install share-loop install volume? (Floor estimate: 200/month. Ceiling: unknown.)
- [ ] Should we add a `Bot/Synthetic` filter to the Recording Page event? Some of the (none)-bucket events may be bot traffic; worth verifying.
- [ ] Cross-device cohort analysis (post-handoff fix) — what does the web visitor → installer → creator funnel actually look like end-to-end? Currently can't see it without merge.
- [ ] iPad gap: auto-popup gates are `(iOS && mobile) || (Mac && tablet)`. Modern iPads identify variously. How big is the iPad cohort and are they falling through?
- [ ] Whether to remove or rebuild the `parent_after_div` and `halloween_div` popups (currently dead code — desktop-gated with iOS-only buttons inside).
- [ ] **Pre-Nov 2025 Web Referrer gap:** Web Ref PV was 15–40% higher than Click Download events through 2025; the gap closed in Nov '25. What was the additional ~300–600 PV/mo source (landing page, blog mentions, smart app banner)? Worth identifying — that's ~10 installs/mo to potentially recover.
- [ ] **iPad-on-Messages share path:** does iMessage on iPad route to Safari (Web Referrer) the same way as iPhone? Affects attribution if iPad share-loop volume is non-trivial.

---

## Cross-references

### Companion plans + specs
- ASO plan → [#18](https://github.com/ZoogHQ/.github/issues/18)
- SEO plan → [#19](https://github.com/ZoogHQ/.github/issues/19)
- Organic social plan → [#22](https://github.com/ZoogHQ/.github/issues/22)
- Tier 1 creator-incentivization spec → `growth/specs/creator-incentivization-tier1.md`
- Children doc strategic narrative → `https://zooghq.github.io/DataRoom/Children/`

### Implicated code commits
- ZoogIOS `b653dbf98` — Jul 6, 2025 — recId rename (measurement artifact, distinct from the bug)
- ZoogIOS `15f7f203d` — Sep 4, 2025 — iOS deferred-deep-link handler **(with the inverted-condition bug)**
- ZoogIOS `22276fe25` — Aug 25, 2025 — revert during Firebase DDL shutdown
- ZoogFrontEnd `cf8c9c9` — Sep 4, 2025 — frontend AppsFlyer params added
- ZoogFrontEnd `b6c3195` — Nov 6, 2025 — **incentive sharing task (regression in Area 1)**
- ZoogFrontEnd `2f660ac` — Nov 6, 2025 — incentive sharing task updated

### Canonical Amplitude charts referenced in this plan

**Canonical share-loop funnels (new users, Deep link → X):**
- [Open From Deep Link [New User] > View](https://app.amplitude.com/analytics/zoog/chart/gx6j5gy7?linkingDashboardId=227vmg5l&sharingId=meht_Lbc)
- [Open From Deep Link [New User] > React](https://app.amplitude.com/analytics/zoog/chart/m3zdpxlx?sharingId=lGqMd4--)
- [Open From Deep Link [New User] > Request Content](https://app.amplitude.com/analytics/zoog/chart/rt4w937f?sharingId=unWLNeJT)
- [Open From Deep Link [New User] > Share](https://app.amplitude.com/analytics/zoog/chart/fxcpr11c)
- [Share funnel split by isDeferred](https://app.amplitude.com/analytics/zoog/chart/yw858t7o?sharingId=O5suxM0j)

**Area 1 — Web request-rate (Nov 2025 regression):**
- [Web Reaction Rate — total](https://app.amplitude.com/analytics/zoog/chart/vjj0fmf/edit/fkgvu72t)
- [Web Likes rate](https://app.amplitude.com/analytics/zoog/chart/kj0tz5d2?sharingId=zg2jh9-A)
- [Web Requests rate](https://app.amplitude.com/analytics/zoog/chart/04nsaypt?sharingId=59DZWtQ4)
- [Mobile Requests by persona (control)](https://app.amplitude.com/analytics/zoog/chart/zn63vkhp/edit/zpaa1k0a)

**iOS deferred-deep-link bug evidence:**
- [Download clicks vs first-time deep-link opens (ratio flip)](https://app.amplitude.com/analytics/zoog/chart/4amqn4gt?sharingId=mxpVte8F)
- [Opened using deep link by type over time (Jul rename)](https://app.amplitude.com/analytics/zoog/chart/sz173rgr?sharingId=KsO0_yd_)
- [isDeferred=true monthly uniques](https://app.amplitude.com/analytics/zoog/chart/new/4o8szj36)

**Volume baselines (loop input + funnel steps):**
- [Recording Page (mobile-web, new) — monthly](https://app.amplitude.com/analytics/zoog/chart/l1v9atm6?sharingId=dJKRrnVs)
- [User clicks download Zoog — monthly](https://app.amplitude.com/analytics/zoog/chart/ilaem2z1?sharingId=RJSCuSlK)
- [Opened using deep link (view+recId, new users) — monthly](https://app.amplitude.com/analytics/zoog/chart/new/p78j1w9d)
- [Click Start Recording (new users) — monthly](https://app.amplitude.com/analytics/zoog/chart/new/kcywt6aq)
- [User selected share option — monthly active sharers](https://app.amplitude.com/analytics/zoog/chart/new/5fw26l7d)

> **Note on chart URLs:** several of the volume-baseline links above are `chart/new/<editId>` URLs from ad-hoc queries. They persist in Amplitude but are not discoverable to other team members until you "Save As" them into the proper project (suggested: a `Share Loop` dashboard alongside the existing `Growth Loops` dashboard at [227vmg5l](https://app.amplitude.com/analytics/zoog/dashboard/227vmg5l)).
