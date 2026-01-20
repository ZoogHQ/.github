# Storage Only Plan - Product Spec

**Feature Owner:** Yoav
**Status:** Draft
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
| Trigger | 30 days after signup (new policy) |
| Flow | Warning banner + emails before deletion |
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

### Flow 2: Free-Tier Conversion

```
Free user reaches Day 30 after signup
        ↓
In-app banner: "Your videos will be deleted in 30 days"
        ↓
Email campaign begins (same cadence as churners)
        ↓
Options:
  - Upgrade to Zoog+ (full features)
  - Subscribe to Storage Plan ($2.99/mo)
  - Download videos before deletion
        ↓
If no action by Day 60: Videos deleted
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

## Video Deletion Policy

Applies to:
- Zoog+ users who fully cancel (not Storage Plan)
- Free-tier users who don't convert

### Deletion Timeline

| Day | Action | Channels |
|-----|--------|----------|
| **Day 0** | Subscription ends / Free tier hits 30 days | - |
| **Day 1** | "Your subscription ended" notification | Email |
| **Day 7** | "Your memories need a home" | Email + Push |
| **Day 14** | "14 days left to save your videos" | Email + Push + In-app banner |
| **Day 21** | "7 days left - download now" | Email + Push + In-app banner |
| **Day 27** | "3 days left - FINAL WARNING" | Email + Push + In-app full-screen |
| **Day 30** | Videos marked for deletion | Email confirmation |
| **Day 37** | **Permanent deletion** | - |

### Grace Period Features

| Day Range | In-App UI |
|-----------|-----------|
| Day 1-14 | Yellow banner: "Your videos will be deleted on [DATE]" |
| Day 15-27 | Red banner with countdown: "X days left" |
| Day 28-30 | Full-screen warning on app open |

### Recovery Window

- **Days 30-37:** Videos soft-deleted (recoverable)
- If user subscribes during this window: Videos restored automatically
- **Day 37+:** Permanent deletion, no recovery

### Bulk Download Feature

| Feature | Description |
|---------|-------------|
| Location | Settings > Export Data > Download All Videos |
| Progress | Show download progress with percentage |
| Resume | Allow resume if interrupted |
| Notification | Push notification when complete |
| Format | Original quality, organized by album |

---

## Email Templates

### Day 1: Subscription Ended

**Subject:** Your Zoog subscription has ended

```
Hi [Name],

Your Zoog subscription has ended, but your [X] family videos are still safe with us.

You have 30 days to decide:

KEEP YOUR MEMORIES - $2.99/month
Your videos stay safe forever. View, download, and share anytime.
[Keep My Memories]

DOWNLOAD YOUR VIDEOS
Save them to your device before they're removed.
[How to Download]

After [DATE], your videos will be permanently deleted.

The Zoog Team
```

### Day 27: Final Warning

**Subject:** FINAL NOTICE: Your [X] Zoog videos will be deleted in 3 days

```
Hi [Name],

This is your final reminder.

In 3 days, on [DATE], your [X] family videos will be permanently deleted.

These memories cannot be recovered.

[Keep Them Safe - $2.99/mo]

Or download them now:
[Download All Videos]

The Zoog Team
```

---

## Technical Requirements

### iOS (ZoogIOS)

| Task | Priority |
|------|----------|
| App Store subscription - Add Storage Plan SKU | P0 |
| Adapty integration - Configure new plan | P0 |
| Subscription logic - Handle storage-only entitlement | P0 |
| Lock creation features - Disable record, lens picker | P0 |
| Upgrade prompts - Modal when tapping locked features | P0 |
| Cancellation flow UI - Add Storage Plan option | P0 |
| Grace period banners - Yellow/red warnings | P0 |
| Bulk download - "Download All" in Settings | P0 |
| Full-screen warning - Day 28-30 modal | P1 |

### Backend (ZoogCloudFunctions)

| Task | Priority |
|------|----------|
| Subscription validation - Recognize storage-only | P0 |
| Feature flags endpoint - Correct permissions | P0 |
| Deletion scheduler - Cron job at Day 30 | P0 |
| Soft delete logic - Flag videos, retain 7 days | P0 |
| Hard delete logic - Permanent deletion Day 37 | P0 |
| Email triggers - Day 1, 7, 14, 21, 27, 30 | P0 |
| Recovery endpoint - Restore on resubscribe | P1 |
| Storage calculation - For 100GB cap | P1 |

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
- [ ] Backend: subscription validation + feature flags

### Week 2: Flows & UI

- [ ] Build cancellation flow UI with Storage Plan option
- [ ] Build upgrade prompt modals
- [ ] Implement grace period banners (yellow/red)
- [ ] Build bulk download feature

### Week 3: Deletion System

- [ ] Backend: deletion scheduler + soft delete
- [ ] Backend: hard delete logic
- [ ] Create email templates
- [ ] Set up email triggers (Day 1, 7, 14, 21, 27, 30)

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

| Event | Trigger |
|-------|---------|
| `cancellation_started` | User initiates cancel |
| `storage_plan_offered` | Modal shown |
| `storage_plan_selected` | User chooses Storage Plan |
| `storage_plan_purchased` | Purchase completed |
| `bulk_download_started` | User starts download |
| `bulk_download_completed` | Download finished |
| `deletion_warning_shown` | In-app banner shown |
| `videos_soft_deleted` | Day 30 deletion |
| `videos_hard_deleted` | Day 37 permanent deletion |
| `videos_restored` | Resubscribed during grace period |

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

*Video resolution upgrading from 540×960 to 1080×1920 (~4x file size)*

| Metric | Current (540p) | Projected (1080p) |
|--------|----------------|-------------------|
| Avg per user | 183 MB | **732 MB** |
| Median per user | 43 MB | **172 MB** |
| Avg user GCS cost | $0.0036/mo | **$0.015/mo** |
| Margin per user | $2.99 | **$2.97** |

### Projected Storage Distribution (1080p)

| Tier | Current | Projected |
|------|---------|-----------|
| Under 100 MB | 68.3% | ~25% |
| 100-500 MB | 23.3% | ~35% |
| 500 MB - 1 GB | 4.8% | ~20% |
| 1-10 GB | 3.6% | ~18% |
| 10-50 GB | 0.0% | ~2% |
| Over 50 GB | 0.0% | ~0.1% |
| Over 100 GB | 0.0% | ~0.02% |

### 100GB Cap Rationale

The 100GB cap is justified because:
1. **Current:** No users exceed 50GB; top user is 33GB
2. **With 1080p:** Top users may reach 50-100GB over time
3. **Provides headroom:** Accounts for 4x growth from HD upgrade
4. **Marketing value:** "100GB" sounds generous to users
5. **Unit economics:** Even at 100GB, cost is $2.00 vs $2.99 revenue
