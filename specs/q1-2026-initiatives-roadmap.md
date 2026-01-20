# Q1 2026 Strategic Initiatives Roadmap

**Created:** January 2026
**Status:** Active

---

## Context

With a downsized team and no UA spend, we're focusing on three strategic initiatives:

1. **Storage Only Plan (#4)** - Monetize churned users, reduce storage cost burden
2. **AI Lens with MediaPipe (#5)** - Solve content drought (retention)
3. **Social Media Bot (#6)** - Drive organic traffic (acquisition)

**Prioritization logic:** Fix revenue → Fix retention → Then acquisition

---

## 6-Week Sprint Timeline

| Week | Storage Plan (#4) | AI Lens POC (#5) | Social Bot (#6) |
|------|-------------------|------------------|-----------------|
| **1** | Setup: SKU, Adapty, subscription logic | MediaPipe POC | Build trends scraper |
| **2** | UI: Cancellation flow, banners, bulk download | POC Go/No-Go | Scraper live, first data |
| **3** | Backend: Deletion scheduler, emails | Lens dev starts (if POC passed) | Analyze + first manual posts |
| **4** | QA: Full flow testing | Continue lens dev | Measure engagement |
| **5** | **Launch** 🚀 (50/50 A/B) | First AI lens draft | Iterate on posts |
| **6** | Iterate + plan free-tier | Launch 2-3 AI lenses | Phase 2: Auto-generation |

---

## Initiative Details

### #4: Storage Only Plan

**Problem:** Churned users get free storage indefinitely (185k users, $665/month cost)

**Solution:** $2.99/month storage-only tier with 100GB cap

**Spec:** [storage-only-plan.md](./storage-only-plan.md)

**GitHub Issue:** [#7](https://github.com/ZoogHQ/.github/issues/7)

**Key Milestones:**
- Week 1: SKU + Adapty + subscription logic
- Week 2: Cancellation flow UI + bulk download
- Week 3: Deletion system + email triggers
- Week 4: QA
- Week 5: Launch 50/50 A/B test
- Week 6: Iterate based on data

**Success Metrics:**
- Churn Interception Rate > 20%
- Zoog+ cannibalization < 2%

---

### #5: AI Generated Lens with MediaPipe

**Problem:** Content production halted (Lens Studio doesn't scale with reduced team)

**Solution:** Explore MediaPipe as alternative for automated/streamlined lens creation

**GitHub Issue:** [#5](https://github.com/ZoogHQ/.github/issues/5)

**Key Milestones:**
- Week 1-2: Time-boxed POC - Can MediaPipe produce 1 lens at 70% Lens Studio quality?
- Week 2: Go/No-Go decision
- Week 3-5: If Go → Develop first batch of AI lenses
- Week 6: Launch 2-3 AI-generated lenses

**Success Metrics:**
- POC: Quality threshold met
- Production: Retention impact measurable

---

### #6: Social Media Bot (Trends Scraper → Auto-posts)

**Problem:** No UA spend, need organic traffic

**Solution:** Automated trend scraping → manual posts → automated posting

**GitHub Issue:** [#6](https://github.com/ZoogHQ/.github/issues/6)

**Phase 1: Trends Scraper (Weeks 1-3)**
- Build scraper for TikTok/IG trends
- Store trends in DB
- Weekly trend report
- Manual posts based on trends

**Phase 2: Auto-generation (Week 6+)**
- Auto-generate post content
- Scheduled posting
- Engagement tracking

**Success Metrics:**
- Phase 1: Identify actionable trends, manual posts get engagement
- Phase 2: Consistent posting cadence, measurable traffic

---

## Dependencies

```
Storage Plan ──────────────────────────────────────────► Revenue stability
                                                              │
AI Lens POC ─── Go/No-Go ──► Lens Development ──────────────► Retention fix
                   │                                          │
                   └─ No-Go ──► Evaluate alternatives         │
                                                              │
Social Bot (Scraper) ──► Manual Posts ──► Auto-generation ──► Acquisition
                                                              │
                                   Only scale after retention fixed ◄─┘
```

---

## Weekly Check-ins

| Week | Key Decisions |
|------|---------------|
| Week 2 | AI Lens POC Go/No-Go |
| Week 4 | Storage Plan QA sign-off |
| Week 5 | Storage Plan launch readiness |
| Week 6 | Review all metrics, plan Phase 2 |

---

## Risks & Mitigations

| Risk | Mitigation |
|------|------------|
| MediaPipe POC fails | 2-week timebox limits downside; have fallback plan |
| Storage Plan low conversion | A/B test at 50/50; iterate on copy/pricing |
| Social bot feels spammy | Start with manual curation; quality over quantity |
| Team capacity stretched | Strict scope control; defer nice-to-haves |

---

## Resources

- [Storage Plan Spec](./storage-only-plan.md)
- [GCS Storage Report](../../ZoogDBTools/output/gcs-storage-report.json)
