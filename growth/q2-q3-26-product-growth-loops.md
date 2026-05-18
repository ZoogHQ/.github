# Q2–Q3 2026 Product Growth Loops Plan

**Created:** May 18, 2026
**Status:** Active
**Owner:** Product + Engineering
**Companion plans:**
- [`q2-q3-26-ASO.md`](https://github.com/ZoogHQ/.github/issues/18) — App Store / ASA / In-App Events / CPPs / Featuring
- [`q2-q3-26-SEO+landing-page-optimization.md`](https://github.com/ZoogHQ/.github/issues/19) — Marketing site, SEO, email, attribution
- [`q2-q3-26-organic-social.md`](https://github.com/ZoogHQ/.github/issues/22) — Organic social channels

---

## Context

A diagnostic dive into the share-loop funnel (May 2025 – May 2026) surfaced two distinct collapses that are **product / engineering issues, not ASO issues**, and both are independently fixable.

### Area 1 — Web request-rate collapse (Nov 2025)

On Nov 6, 2025 (ZoogFrontEnd commit `b6c3195` "incentive sharing task"), the web Recording Page request flow was rebuilt to insert an "incentive sharing" modal after the user selects a book to request. The modal occupies the screen, interrupts the natural engagement loop, and either suppresses the `User Requested Content` event from firing reliably or trains recipients to avoid the request action.

**Data signature:**
- Web request rate (Click Play Recording → User Requested Content): **20.6% (Sep '25) → 13.5% (Apr '26)** — a 35% relative drop, stepwise from Nov 2025
- Web like rate (Click Play Recording → User clicks the heart): essentially flat (5.2% → 4.0%) — confirms it's not a global reaction issue
- Mobile request rate (Reactions View → User Requested Content): stable or improving across personas — confirms it's not content quality
- Downstream effect: new-user Watch → Click Start Recording funnel fell **50% (May '25) → 31% (Mar '26)** — same timing, same shape

**Supporting charts:**
- [Web Reaction Rate — total (Click Play → any reaction)](https://app.amplitude.com/analytics/zoog/chart/vjj0fmf/edit/fkgvu72t)
- [Web Likes rate (Click Play → User clicks the heart)](https://app.amplitude.com/analytics/zoog/chart/vjj0fmf/edit/l1d33b8q) — control: barely moved
- [Web Requests rate (Click Play → User Requested Content)](https://app.amplitude.com/analytics/zoog/chart/vjj0fmf/edit/ljfebiws) — the 35% drop
- [Mobile Requests by persona (Reactions View → User Requested Content)](https://app.amplitude.com/analytics/zoog/chart/zn63vkhp/edit/zpaa1k0a) — control: stable across personas, rules out content quality

### Area 2 — New user web view → share collapse (Aug 25 / Dec 25 / Feb 26)

Three separate inflection points in the new-user web `Recording Page → User selected share option` funnel:

- **Aug 2025:** Firebase Dynamic Links shutdown (Aug 25, 2025). Frontend was mid-migration to AppsFlyer (deeplink.service.ts commits Aug 22 + Sep 4). iOS-side reverts on the same day. Web share-button URL generation may have shifted.
- **Dec 2025:** Likely the cohort-lagged effect of the Nov 6 incentive modal compounding into share behavior. Also potentially the Dec 7 `reverted runmediflowv2` iOS commit.
- **Feb 2026:** Cumulative — Meta pause completed + Nov 6 modal damage + degraded loop dynamics. Probably no single product change; the steady-state of a broken loop.

### Plus: iOS deferred-deep-link condition bug (Sep 4, 2025)

A separate bug in `AppDelegate+AppsFlyer.swift` (commit `15f7f203d`). The deferred deep-link handler has an inverted condition that suppresses the `Opened using deep link {type: "view", isDeferred: true}` event for most cold installs — and as a side effect, fails to route the user to the recording they were trying to view. Capture rate currently ~65/month vs an estimated 200–400 expected.

**Supporting charts:**
- [Share-loop conversion split by isDeferred (Nov 25 – today)](https://app.amplitude.com/analytics/zoog/chart/fxcpr11c/edit/aasxxnm3) — isDeferred=true cohort converts much worse and on smaller base than isDeferred=false
- [Total Download clicks vs first-time deep-link opens (the ratio flip)](https://app.amplitude.com/analytics/zoog/chart/new/igaas1vt) — pre-Sep 2025: 1st-time opens > download clicks; post-Sep: the ratio flips
- [Opened using deep link by `type` over time](https://app.amplitude.com/analytics/zoog/chart/new/hhf2jvne) — Jul 2025 view→recId rename (measurement artifact, distinct from this bug)
- [isDeferred=true monthly uniques (Sep '25 onward)](https://app.amplitude.com/analytics/zoog/chart/new/4o8szj36) — ~65/month in Apr 2026; the floor the fix should lift

### Plus: cross-device identity gap (structural)

There's no web → iOS device_id handoff in the OneLink URL. Every web visitor and every post-install user lives under separate `amplitude_id` entries with no merge logic outside of post-install email-match sign-in. Cohort analysis across surfaces is materially distorted; the loop's true install contribution is not measurable without a fix.

---

## North-star metrics (90-day target)

| Metric | Today (Apr/May 2026) | 90-day target |
|---|---:|---:|
| Web request rate (mobile-web) | 13.5% | **18–20%** (recover to pre-Nov baseline) |
| Watch → Click Start Recording (new users via deep-link) | 31% | **45–50%** (recover to pre-Nov baseline) |
| isDeferred=true monthly events (cold-install attribution) | ~65 | **200–400** (post iOS fix) |
| New users firing Opened using deep link (view+recId, monthly) | ~200 | 400–600 (depends on share volume recovery + measurement) |
| New web view → share rate (Aug 2025 baseline restoration) | (current low) | within 20% of Aug '25 baseline |
| Click handlers with analytics coverage | 2 of 4 | 4 of 4 |
| Cross-device merge rate (web visitor → iOS install) | unknown | measurable + tracked |

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

---

## Open questions

- [ ] What does the SECOND treatment look like for the incentive modal A/B test? (Less intrusive design — toast? Post-share confirmation? Card on the home page?)
- [ ] After the iOS deferred-deep-link fix, what's the true cold-install share-loop install volume? (Floor estimate: 200/month. Ceiling: unknown.)
- [ ] Should we add a `Bot/Synthetic` filter to the Recording Page event? Some of the (none)-bucket events may be bot traffic; worth verifying.
- [ ] Cross-device cohort analysis (post-handoff fix) — what does the web visitor → installer → creator funnel actually look like end-to-end? Currently can't see it without merge.
- [ ] iPad gap: auto-popup gates are `(iOS && mobile) || (Mac && tablet)`. Modern iPads identify variously. How big is the iPad cohort and are they falling through?
- [ ] Whether to remove or rebuild the `parent_after_div` and `halloween_div` popups (currently dead code — desktop-gated with iOS-only buttons inside).

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

**Area 1 — Web request-rate (Nov 2025 regression):**
- [Web Reaction Rate — total](https://app.amplitude.com/analytics/zoog/chart/vjj0fmf/edit/fkgvu72t)
- [Web Likes rate](https://app.amplitude.com/analytics/zoog/chart/vjj0fmf/edit/l1d33b8q)
- [Web Requests rate](https://app.amplitude.com/analytics/zoog/chart/vjj0fmf/edit/ljfebiws)
- [Mobile Requests by persona (control)](https://app.amplitude.com/analytics/zoog/chart/zn63vkhp/edit/zpaa1k0a)

**iOS deferred-deep-link bug evidence:**
- [Share-loop conversion split by isDeferred](https://app.amplitude.com/analytics/zoog/chart/fxcpr11c/edit/aasxxnm3)
- [Download clicks vs first-time deep-link opens (ratio flip)](https://app.amplitude.com/analytics/zoog/chart/new/igaas1vt)
- [Opened using deep link by type over time (Jul rename)](https://app.amplitude.com/analytics/zoog/chart/new/hhf2jvne)
- [isDeferred=true monthly uniques](https://app.amplitude.com/analytics/zoog/chart/new/4o8szj36)

**Volume baselines (loop input + funnel steps):**
- [Recording Page (mobile-web, new) — monthly](https://app.amplitude.com/analytics/zoog/chart/new/phetw7a3)
- [User clicks download Zoog — monthly](https://app.amplitude.com/analytics/zoog/chart/new/6ataybd7)
- [Opened using deep link (view+recId, new users) — monthly](https://app.amplitude.com/analytics/zoog/chart/new/p78j1w9d)
- [Click Start Recording (new users) — monthly](https://app.amplitude.com/analytics/zoog/chart/new/kcywt6aq)
- [User selected share option — monthly active sharers](https://app.amplitude.com/analytics/zoog/chart/new/5fw26l7d)

> **Note on chart URLs:** several of the volume-baseline links above are `chart/new/<editId>` URLs from ad-hoc queries. They persist in Amplitude but are not discoverable to other team members until you "Save As" them into the proper project (suggested: a `Share Loop` dashboard alongside the existing `Growth Loops` dashboard at [227vmg5l](https://app.amplitude.com/analytics/zoog/dashboard/227vmg5l)).
