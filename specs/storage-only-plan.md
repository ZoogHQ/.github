# Storage Only Plan - Product Spec

**Feature Owner:** Yoav
**Status:** In Progress — Backend complete, iOS in progress
**Target Launch:** 6 weeks

---

## Executive Summary

A low-cost subscription tier ($2.99/month) for users who want to preserve their videos without actively creating new content. Targets two segments:
1. **Zoog+ churners** - offered during cancellation flow
2. **Free-tier users** - offered before video deletion begins

**Primary Goal:** Validate whether a low-cost storage option reduces hard churn and converts free users.

---

## Business Objectives

| Metric | Target |
|--------|--------|
| Storage-Only Conversion Rate (churners) | 20-30% |
| Free-tier Conversion Rate | TBD |
| Zoog+ Cannibalization | <2% decline |
| Gross Margin | Revenue > Storage Cost |

---

## Pricing

| Plan | Price | Notes |
|------|-------|-------|
| Monthly | $2.99/month | Single tier MVP |
| Annual | $29.99/year | 16.7% savings |

**Storage Limit:** 100GB

---

## Target Audiences

### Audience 1: Zoog+ Churners (Primary)

| Attribute | Detail |
|-----------|--------|
| Trigger | User clicks "Cancel Renewal" |
| Flow | Post-cancellation interruption modal |
| Excluded | New users (first 7 days), active subscribers |
| Goal | Convert to Storage Plan instead of full churn |

### Audience 2: Free-Tier Users (Secondary)

| Attribute | Detail |
|-----------|--------|
| Trigger | User exceeds 100MB free storage limit |
| Flow | Warning banner + emails + push + in-app before deletion |
| Goal | Convert to Storage Plan or Zoog+ |

---

## Feature Scope

### Included in Storage Plan

| Feature | Included | Notes |
|---------|----------|-------|
| View all videos | Yes | Full playback access |
| Download videos | Yes | Including bulk download |
| Share videos | Yes | Sharing encouraged (existing incentives) |
| Access memory albums | Yes | View existing albums |
| Cloud storage | Yes | Up to 100GB |
| App access | Yes | Full app access |

### NOT Included (Creation Features)

| Feature | Included | Notes |
|---------|----------|-------|
| Record new videos | No | Locked, prompts upgrade |
| Access to lenses | No | Locked |
| Create new albums | No | Locked |
| New title releases | No | Locked |

### Grandfather Clause (>100GB Users)

Users with existing storage exceeding 100GB:
- Can view/download all videos
- Cannot create new content
- Must delete or upgrade to Zoog+ if they want to add more

---

## User Flows

### Flow 1: Zoog+ Cancellation

```
User clicks "Cancel Renewal"
        ↓
Standard retention offer
        ↓
If declined: Storage Plan offer modal
        ↓
"Keep Your Memories Safe for Just $2.99/Month"
"You have X videos (X.X GB). Don't lose them!"
        ↓
[Keep My Memories - $2.99/mo]  [Download & Cancel]  [Cancel Anyway]
        ↓
If Storage Plan: Downgrade, keep access
If Download: Bulk download flow, then 30-day deletion countdown
If Cancel: 30-day deletion countdown begins
```

### Flow 2: Free-Tier Storage Limit Exceeded

```
Free user exceeds 100MB storage limit
        ↓
storageLimitCron marks oldest videos as "scheduledForDeletion"
        ↓
In-app: Videos show warning badge via getScheduledDeletions API
        ↓
30-day warning sequence begins (email + push + in-app):
  Day 1:  "You have exceeded your storage limit. X videos scheduled for deletion..."
  Day 7:  "Your oldest videos are scheduled for removal..."
  Day 14: "14 days left to save your videos"
  Day 21: "7 days left!"
  Day 27: "3 days left — FINAL NOTICE"
  Day 30: "Your oldest videos have been removed"
        ↓
Options at any time:
  - Upgrade to Zoog+ (full features, unlimited storage)
  - Subscribe to Storage Plan (100GB, $2.99/mo)
  - Download videos before deletion
  - Delete videos to go under 100MB limit (auto-reverts scheduled deletions)
        ↓
If no action by Day 30: Videos soft-deleted (hidden from app, files remain on GCS)
```

### Flow 3: In-App Experience (Storage Plan User)

```
Storage Plan user opens app
        ↓
Full access to Library, Albums, Videos
        ↓
Taps "Record" or any creation feature
        ↓
Upgrade modal: "Unlock Recording with Zoog+"
        ↓
[Upgrade to Zoog+]  [Maybe Later]
```

---

## Storage Limit Enforcement System (✅ Implemented — PR #363)

### Per-Plan Storage Limits

| Plan | Limit | Config Key |
|------|-------|------------|
| Free | 100 MB | `settings/plans.storageLimits.free` |
| Storage-Only | 100 GB | `settings/plans.storageLimits.storage-only` |
| Premium (Zoog+) | Unlimited | `settings/plans.storageLimits.premium = -1` |

Limits stored in Firestore `settings/plans` document — can be updated without redeploying.

### Recording Status Flow

System-initiated statuses (separate from user-initiated `markedForDeletion` → `deleted`):
```
active → scheduledForDeletion → softDeleted
  ↑            │
  └── revert ──┘  (user upgrades or deletes enough to be under limit)
```

| Status | Visibility | Files on GCS | Recoverable |
|--------|-----------|--------------|-------------|
| `active` | Visible in app | Yes | N/A |
| `scheduledForDeletion` | Visible in app with warning | Yes | Yes — automatic |
| `softDeleted` | Hidden from app | Yes | Yes — automatic on resubscribe |

### Enforcement Cron (`storageLimitCron`)

Daily cron (Cloud Scheduler, 3am UTC) that:
1. Queries users who may be over limit (expired subscribers, storage-only users, users already in grace period)
2. Calculates **active-only** storage per user (cross-references GCS files with Firestore recording statuses)
3. Marks oldest recordings as `scheduledForDeletion` until active storage ≤ plan limit
4. Re-evaluates on every run — if user is now under limit, reverts all scheduled deletions
5. Transitions `scheduledForDeletion` → `softDeleted` when `scheduledDeletionDate` has passed

### Grace Period Model

| Field | Type | Description |
|-------|------|-------------|
| `gracePeriodStartDate` | ISO string | When the 30-day countdown began |
| `gracePeriodReason` | string | `"subscription_expired"` or `"storage_limit_exceeded"` |
| `scheduledDeletionDate` | ISO string | On recording docs: `gracePeriodStartDate + 30 days` |

### Client API (`getScheduledDeletions`)

Callable function that returns what the app needs to display deletion warnings:
```json
{
  "hasScheduledDeletions": true,
  "deletionDate": "2026-03-18T00:00:00Z",
  "daysLeft": 23,
  "recordings": [
    { "id": "rec123", "thumbnailImage": "...", "updateTime": "...", "duration": 42, "scheduledDeletionDate": "..." }
  ],
  "totalScheduledCount": 12,
  "currentActiveUsage": "48.2 MB",
  "planLimit": "100 MB",
  "planLimitBytes": 104857600,
  "overageBytes": 37600000,
  "tier": "free"
}
```

### Storage Usage API (`getStorageUsage`)

Updated to support all tiers with dynamic limits:
```json
{
  "storageUsedBytes": 121634816,
  "storageUsedGB": 0.11,
  "storageLimitBytes": 104857600,
  "storageLimitGB": 0.10,
  "isOverCap": true,
  "canUpload": false,
  "tier": "free"
}
```

### Recovery

Automatic recovery when subscription becomes active (via Adapty or Apple webhook):
1. All `scheduledForDeletion` and `softDeleted` recordings revert to `active`
2. Grace period fields cleared from user doc
3. Amplitude "Videos Restored" event fired

Also triggers during cron re-evaluation if user manually deletes enough videos to go under limit.

### Subscription Tier Verification (✅ Implemented — PR #369, PR #370)

**Problem:** Adapty webhook events (especially from sandbox) can write stale `accessLevel: "premium"` and `subscriptionActive: true` to Firestore for expired subscriptions. Additionally, Adapty may never send `subscription_expired` webhooks for sandbox auto-renewals — it just stops renewing, so Firestore never learns the sub expired.

**Solution:** Three-layer tier resolution, from most authoritative to fallback:

| Layer | Function | Source | Used By |
|-------|----------|--------|---------|
| 1. Adapty API | `getAdaptyVerifiedTier(userId, userData)` | Real-time Adapty API call | `getStorageUsage`, `getScheduledDeletions` |
| 2. Firestore expiry check | `getValidatedSubscriptionTier(userData)` | Firestore `subscriptionExpiryDate` | `storageLimitCron` (batch, avoids API rate limits) |
| 3. Access level only | `getSubscriptionTier(accessLevel)` | Firestore `accessLevel` field | Legacy (kept for backward compat) |

**`getAdaptyVerifiedTier`** (PR #370):
- Calls `GET /api/v1/sdk/profiles/{userId}/` on Adapty API
- Checks `paid_access_levels.premium.is_active` and `paid_access_levels["storage-only"].is_active`
- Falls back to `getValidatedSubscriptionTier` if Adapty API is unreachable (5s timeout)
- Used for user-facing functions where accuracy matters more than latency

**`getValidatedSubscriptionTier`** (PR #369):
- Checks `subscriptionExpiryDate` — if in the past, returns `"free"`
- If no expiry date and `subscriptionActive === false`, returns `"free"`
- Otherwise falls through to `accessLevel` (same as original behavior)
- Used for batch processing where Adapty API rate limits are a concern

---

## Notification System (✅ Implemented — PR #363)

### Warning Sequence

| Day | Action | Channels |
|-----|--------|----------|
| **Day 1** | Videos scheduled, warning begins | Email + Push + In-App |
| **Day 7** | "Your memories need a home" | Email + Push + In-App |
| **Day 14** | "14 days left to save your videos" | Email + Push + In-App |
| **Day 21** | "7 days left" | Email + Push + In-App |
| **Day 27** | "3 days left — FINAL NOTICE" | Email + Push + In-App |
| **Day 30** | Videos soft-deleted | Email + Push + In-App |

### Two Template Sets

| Channel | Cancelled Subscribers | Free Users |
|---------|----------------------|------------|
| Email | `deletion-warning-day-{N}` | `storage-limit-warning-day-{N}` |
| Push CTA | Storage-only popup | Upgrade to Zoog+ |
| In-App CTA | Storage-only popup | Manage subscription |

Selection is automatic based on `gracePeriodReason`:
- `"subscription_expired"` → subscriber templates
- `"storage_limit_exceeded"` → free-user templates

### Email Templates (Mandrill)

12 templates total (6 per flow). Each day has a distinct header color that progressively conveys urgency:

| Day | Header Color | Subhead Color |
|-----|-------------|---------------|
| 1 | `#F1F1F1` (light gray) | `#002349` (dark blue) |
| 7 | `#002349` (dark blue) | `#FFFFFF` (white) |
| 14 | `#ff7051` (orange-red) | `#FFFFFF` (white) |
| 21 | `#ff8500` (orange) | `#FFFFFF` (white) |
| 27 | `#b71c1c` (dark red) | `#FFFFFF` (white) |
| 30 | `#424242` (dark gray) | `#FFFFFF` (white) |

Merge variables: `*|FNAME|*`, `*|VIDEO_COUNT|*`, `*|STORAGE|*`, `*|DAYS_LEFT|*`, `*|DELETION_DATE|*`

---

## Technical Requirements

### iOS (ZoogIOS)

| Task | Priority | Status |
|------|----------|--------|
| App Store subscription - Add Storage Plan SKU | P0 | ✅ Done |
| Adapty integration - Configure new plan | P0 | |
| Subscription logic - Handle storage-only entitlement | P0 | |
| Lock creation features - Disable record, lens picker | P0 | |
| Upgrade prompts - Modal when tapping locked features | P0 | |
| Cancellation flow UI - Add Storage Plan option | P0 | |
| Grace period banners - Yellow/red warnings | P0 | |
| Bulk download - "Download All" in Settings | P0 | |
| Full-screen warning - Day 28-30 modal | P1 | |
| Show scheduled deletions UI (via `getScheduledDeletions` API) | P0 | |

### Backend (ZoogCloudFunctions)

| Task | Priority | Status |
|------|----------|--------|
| Storage limits per plan (`settings/plans`) | P0 | ✅ PR #363 |
| Storage limit enforcement cron (`storageLimitCron`) | P0 | ✅ PR #363 |
| Soft delete logic (`scheduledForDeletion` → `softDeleted`) | P0 | ✅ PR #363 |
| Client API for scheduled deletions (`getScheduledDeletions`) | P0 | ✅ PR #363 |
| Email triggers (Day 1, 7, 14, 21, 27, 30) | P0 | ✅ PR #363 |
| Free-user email templates (6 Mandrill templates) | P0 | ✅ PR #363 |
| Push + in-app notifications for free users | P0 | ✅ PR #363 |
| Recovery on resubscribe (webhooks) | P1 | ✅ PR #363 |
| Active-only storage calculation | P1 | ✅ PR #363 |
| Dynamic storage limits (`getStorageUsage`) | P1 | ✅ PR #363 |
| Subscription tier verification — Firestore expiry check | P0 | ✅ PR #369 |
| Subscription tier verification — Adapty API real-time check | P0 | ✅ PR #370 |
| Validation script (`validate-subscription-tiers.js`) | P2 | ✅ PR #369 |
| Hard delete logic | P2 | Deferred (#338) |

### Files Modified/Created (PR #363, #369, #370)

| File | Action |
|------|--------|
| `functions/controllers/shared.js` | Added `getStorageLimits`, `calculateActiveStorageBytes`, `formatStorageSize`, `revertScheduledDeletions` (PR #363); Added `getValidatedSubscriptionTier` (PR #369); Added `getAdaptyVerifiedTier` (PR #370) |
| `functions/controllers/storageLimitCron.js` | **NEW** — core enforcement cron |
| `functions/controllers/getScheduledDeletions.js` | **NEW** — client API |
| `functions/controllers/deletionWarningCron.js` | Refactored to unified grace period model with two milestone sets |
| `functions/controllers/getStorageUsage.js` | Dynamic limits, active-only calculation |
| `functions/controllers/getSubscriptionInfo.js` | Recovery logic on resubscribe |
| `functions/controllers/appleWebHook.js` | Recovery logic on resubscribe |
| `scripts/validate-subscription-tiers.js` | **NEW** — read-only tier validation script (PR #369) |
| `functions/controllers/testDeletionWarning.js` | Added `reason` param for free-user testing |
| `functions/index.js` | Registered `storageLimitCron` and `getScheduledDeletions` |

---

## A/B Test Plan

### 50/50 Split from Launch

| Group | % | Experience |
|-------|---|------------|
| Control | 50% | Existing cancellation flow (hard churn) |
| Test | 50% | New flow with Storage Plan offer |

**Success Criteria:**
- Churn Interception Rate (CIR) > 20%
- Zoog+ cannibalization < 2%

---

## 6-Week Rollout Plan

### Week 1: Setup & Core

- [ ] Add Storage Plan SKU to App Store Connect
- [ ] Configure Adapty
- [ ] Implement subscription logic (iOS)
- [ ] Lock creation features for storage users
- [x] Backend: subscription validation + feature flags
- [x] Backend: subscription tier verification — Adapty API + Firestore expiry checks (PR #369, #370)

### Week 2: Flows & UI

- [ ] Build cancellation flow UI with Storage Plan option
- [ ] Build upgrade prompt modals
- [ ] Implement grace period banners (yellow/red)
- [ ] Build bulk download feature
- [ ] Show scheduled deletions UI (via `getScheduledDeletions` API)

### Week 3: Deletion System — ✅ Complete

- [x] Backend: storage limit enforcement cron + soft delete
- [x] Backend: recovery logic in webhooks
- [x] Create email templates (subscriber + free-user sets)
- [x] Set up notification triggers (Day 1, 7, 14, 21, 27, 30)
- [x] Client API for scheduled deletions

### Week 4: QA & Launch Prep

- [ ] Test full 30-day flow (accelerated in staging)
- [ ] Test billing: purchase, downgrade, restore
- [ ] Test bulk download: progress, resume, completion
- [ ] Full QA pass
- [ ] Prepare analytics dashboards

### Week 5: Launch (50/50)

- [ ] Launch to 50% of cancelling users
- [ ] Monitor: conversion rate, errors, support tickets
- [ ] Daily standups to review metrics

### Week 6: Iterate & Expand

- [ ] Analyze conversion data
- [ ] Optimize copy/UX based on learnings
- [ ] Plan free-tier rollout (Phase 2)
- [ ] Apply to existing churned users (with 60-day notice)

---

## Analytics Events

| Event | Trigger | Status |
|-------|---------|--------|
| `cancellation_started` | User initiates cancel | |
| `storage_plan_offered` | Modal shown | |
| `storage_plan_selected` | User chooses Storage Plan | |
| `storage_plan_purchased` | Purchase completed | |
| `bulk_download_started` | User starts download | |
| `bulk_download_completed` | Download finished | |
| `deletion_warning_shown` | In-app banner shown | |
| `Deletion Warning Sent` | Email/push/in-app sent (with `milestone_day`, `grace_period_reason`) | ✅ |
| `Subscription Event` | Subscription status change | ✅ |
| `Videos Soft Deleted` | Day 30 soft deletion | ✅ |
| `Videos Restored` | Resubscribed/went under limit (with `restored_count`, `source`) | ✅ |
| `videos_hard_deleted` | Permanent deletion | Deferred |

---

## Open Questions

| Question | Status |
|----------|--------|
| What's the average storage per user? | **Answered: 183 MB** |
| How many users are >100GB? | **Answered: 0 users** |
| How many churned users have free storage? | **Answered: 185,492 users** |
| Notice period for existing churned users? | Recommend 60 days |
| Family sharing support? | Defer to Phase 2 |
| Web platform support? | iOS only for MVP |
| When to implement hard delete? | After soft-delete system is proven stable |

---

## Appendix A: Storage Analysis (Actual Data)

*Data collected: January 2026 via GCS bucket scan of `recordings_storage_prod`*

### Current Storage Statistics

| Metric | Value |
|--------|-------|
| Total users with recordings | 185,492 |
| Total files | 4,006,827 |
| Total storage | 32.46 TB |
| **Average per user** | **183 MB** |
| **Median per user** | **43 MB** |
| 90th percentile | 418 MB |
| 95th percentile | 795 MB |
| 99th percentile | 2.23 GB |

### Storage Distribution

| Tier | Users | % |
|------|-------|---|
| Under 100 MB | 126,746 | 68.3% |
| 100-500 MB | 43,246 | 23.3% |
| 500 MB - 1 GB | 8,812 | 4.8% |
| 1-10 GB | 6,653 | 3.6% |
| 10-50 GB | 35 | 0.0% |
| 50-100 GB | 0 | 0.0% |
| **Over 100 GB** | **0** | **0.0%** |

### Top Users by Storage

| Rank | User ID | Storage |
|------|---------|---------|
| 1 | UUyPhm7FUBYBKk7bujK2... | 33.3 GB |
| 2 | v3Y9zd2XNDX92oGLwuRR... | 24.5 GB |
| 3 | hb9NSsJTJKYu1tDuXZAe... | 22.8 GB |

**Note:** No users currently exceed 50GB. The 100GB cap provides significant headroom.

---

## Appendix B: Cost Analysis

### Current Cost Structure (540p videos)

| Metric | Value |
|--------|-------|
| GCS Standard Storage | $0.02/GB/month |
| Total monthly GCS cost | $664.73 |
| **Avg user cost** | **$0.0036/month** |
| Storage Plan price | $2.99/month |
| **Margin per user** | **$2.99 (99.9%)** |
| Break-even storage | 150 GB |

### Projected Cost Structure (1080p videos)

*Video resolution upgrading from 540x960 to 1080x1920 (~4x file size)*

| Metric | Current (540p) | Projected (1080p) |
|--------|----------------|-------------------|
| Avg per user | 183 MB | **732 MB** |
| Median per user | 43 MB | **172 MB** |
| Avg user GCS cost | $0.0036/mo | **$0.015/mo** |
| Margin per user | $2.99 | **$2.97** |

### 100GB Cap Rationale

The 100GB cap is justified because:
1. **Current:** No users exceed 50GB; top user is 33GB
2. **With 1080p:** Top users may reach 50-100GB over time
3. **Provides headroom:** Accounts for 4x growth from HD upgrade
4. **Marketing value:** "100GB" sounds generous to users
5. **Unit economics:** Even at 100GB, cost is $2.00 vs $2.99 revenue
