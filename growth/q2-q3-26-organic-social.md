# Q2–Q3 2026 Organic Social Plan

**Created:** May 14, 2026
**Status:** Active
**Owner:** Marketing
**Companion plans:**
- [`q2-q3-26-ASO.md`](./q2-q3-26-ASO.md) — App Store / ASA / In-App Events / CPPs
- [`q2-q3-26-SEO+landing-page-optimization.md`](./q2-q3-26-SEO+landing-page-optimization.md) — Marketing site, SEO, email, attribution
- [`specs/creator-incentivization-tier1.md`](./specs/creator-incentivization-tier1.md) — Tag-on-share product spec (UGC supply)

---

## Context

Organic social is currently a **near-zero install channel** (431 GA sessions and a handful of attributed installs over the last 12 months) but has structural assets that make it the highest-leverage long-term lever:

1. **138K active creators producing 1.04M shares/year** — the largest UGC pool any kids/family app has
2. **Custom share sheet** in iOS — full control over the share-to-Instagram and share-to-TikTok flows (Tier 1 spec lives here)
3. **Existing IG presence (5K–20K followers, moderate engagement)** — real audience, just not scaling
4. **Smaller FB / YT / TikTok / LinkedIn footprints** — opportunity rather than legacy

### The honest framing

Goal selected: **direct app install acquisition.**
Capacity: **1–2 posts/week per platform, internal team.**

Realistic ceiling under those constraints: **50–200 installs/month at month 1, growing to 200–500 by month 6** — meaningful but not the channel that solves the App Store install collapse on its own. The much bigger long-term value is a **library of organic-validated creative** ready for paid amplification when Meta reactivates, plus a **defensible community moat** competitors can't replicate.

Strategy: optimize every post for **both** direct response **and** paid creative reuse. Cross-post aggressively to multiply 1–2 posts into 5–10 platform appearances. Treat UGC sourcing and community as multipliers on top of original production.

---

## North-star metrics (90-day target)

| Metric | Today | Day 30 | Day 60 | Day 90 |
|---|---:|---:|---:|---:|
| IG followers (@zooghq) | 5–20K | +5–10% | +10–15% | +15–25% |
| TikTok followers | ~0 (build) | 200–500 | 1–2K | 3–5K |
| Cross-platform Reel views/mo | low | 10–20K | 30–50K | 50–100K |
| Social-attributed installs/mo (UTM) | <50 | 50–150 | 100–250 | 200–500 |
| Bio-link clicks/mo | unmeasured | baseline | +50% | +100% |
| UGC reposts/mo | 0 | 1–2 | 4–6 | 8–10 |
| Viable paid creatives in library | 0 | 2–4 | 8–12 | 15–20 |

**Asymmetric upside not in this table:** at 1–2 posts/week with reaction-video content, expect 1–2 organic posts per quarter that significantly outperform the median. That's the upside worth optimizing for, even though it can't be planned.

---

## Workstreams

Five layers. The whole plan only works if all five run — UGC supply alone produces content nobody can convert, conversion fixes alone leave you with more efficient distribution of one post per week, etc.

- **A. Conversion mechanics** — every post earns a click
- **B. Distribution multiplier** — cross-posting, platform launches, algorithmic plays
- **C. UGC supply engine** — sourcing content from the 200K-household base
- **D. Community moat** — founder content, FB groups, real engagement
- **E. Measurement & attribution** — UTM convention, dashboards, weekly review

### Platform priority

| Tier | Platform | Audience fit | Effort/return |
|---|---|---|---|
| 1 | **Instagram** | Parents 30–45 + grandparents 50–65 | Primary surface |
| 1 | **TikTok** | Parents 25–40, grandparent-creator content rising | Same content as IG, different audience |
| 2 | **Facebook (Reels + Groups)** | Grandparents 50–65 (highest-converting persona) | Reels cross-post; Groups is separate community play |
| 3 | **YouTube Shorts** | Compounding SEO + cross-platform reach | Cross-post only |
| Niche | **LinkedIn** (founder personal) | PR / investor / partnership signal | 1 post/week from founder |
| Defer to Q4 | **YouTube long-form** | High production cost; SEO compounding | Not on Q2–Q3 roadmap |

---

## Week 1 (May 12–18) — Conversion mechanics fix

The "you should have done this last year" category. All four are 1–2 hours each, all measurable, all ship this week.

### A. Conversion mechanics

- [ ] **Link in bio rebuild** — single primary CTA across all platforms
  - [ ] Build `getzoog.com/start` page: one Get Zoog Free button, App Store + Play Store badges, ~300 words social proof (4.9★ / 20K+ ratings, Scary Mommy press), no other links
  - [ ] OR set up Stan / Beacons / Komi if analytics-on-bio is preferred (~$15/mo, includes click tracking)
  - [ ] Update bio link on IG, TikTok, FB, YouTube, LinkedIn to point to `/start` with platform UTM (`?utm_source=ig_bio`, `?utm_source=tt_bio`, etc.)
- [ ] **Reels CTA template** — every Reel earns a click
  - [ ] Create reusable end-card asset: "Make one for your grandkid — link in bio" (1-second card, also voice-over option)
  - [ ] Caption template ending with the same CTA + branded hashtag
  - [ ] Post-publish habit: pin a comment with the bio link
- [ ] **IG Stories link sticker** — daily install CTA
  - [ ] Decide cadence (target: at least 1 Story/day, even just resharing feed posts)
  - [ ] Add link sticker to every Story
  - [ ] Save default link sticker location/text as a habit
- [ ] **Hashtag strategy reset**
  - [ ] Replace generic high-competition tags (#kids, #family, #app, #parenting) with niche grandparent-intent tags:
    - `#grandparenting` `#grandparentlife` `#grandparenthood`
    - `#longdistancegrandma` `#longdistancefamily`
    - `#newgrandma` `#newgrandpa`
    - `#granddaughter` `#grandson`
    - `#grandmasoftiktok` `#grandparentsoftiktok`
  - [ ] Plus branded: `#zoogmoment` `#zoogapp`
  - [ ] Save as default tag set in scheduling tool

### E. Measurement baseline

- [ ] Pull current IG insights — followers, reach, engagement rate, top posts (anchor for measuring lift)
- [ ] Document UTM convention: every social link uses `utm_source={platform}_{surface}&utm_medium=organic&utm_campaign={pillar}`
- [ ] Set up Amplitude dashboard for `Bio Link Click` events from `/start` page (separate from web LP traffic)

---

## Week 2 (May 19–25) — Distribution infrastructure

### B. Distribution

- [ ] **Cross-posting tool setup** — Buffer (~$15/mo), Later (~$25/mo), or Metricool
  - [ ] Connect IG, TikTok, FB, YouTube accounts
  - [ ] Build template that handles aspect-ratio differences (TikTok 9:16, IG Reels 9:16, YT Shorts 9:16, FB Reels 9:16 — mostly aligned)
  - [ ] Save default tag set + caption structure
- [ ] **TikTok account launch / refresh**
  - [ ] Profile setup: handle (@zooghq if available), bio with `/start` link, profile photo
  - [ ] Plan first 10 cross-posted Reels for the launch month
- [ ] **Founder LinkedIn account setup**
  - [ ] Founder updates personal LinkedIn bio to "Building Zoog — personalized stories for grandparents and grandkids"
  - [ ] First post: launch announcement / share Zoog journey

### A. Apply CTA template
- [ ] Audit last 10 Reels → add the Reels CTA template + bio-link pin to backfill where possible

---

## Weeks 3–4 (May 26 – Jun 8) — UGC supply + content rhythm

### C. UGC supply (Tier 1 — passive harvest, 0 product changes)

- [ ] **Branded hashtag confirmation** — finalize `#ZoogMoment` (or alternative); update bio + post mentions to surface it
- [ ] **Mention monitoring setup** — daily check of @zooghq tags on IG, TikTok, FB
  - [ ] Tool: Brand24 free trial OR manual via platform notifications
- [ ] **DM template** — ready-to-paste repost-permission ask
  - [ ] *"Hi [name]! Loved seeing your Zoog moment 💕 Mind if we feature it on our official account? Always with full credit to you."*
- [ ] **First UGC reposts shipped** (target: 2 in this window)
  - [ ] Find → DM → wait for permission → polish (light touch — captions only) → cross-post → credit creator → DM creator letting them know

### B. Content rhythm — first month of cross-posting

- [ ] **Weekly content rhythm:**
  - [ ] Mon: Reaction Reel (UGC if available, otherwise produced)
  - [ ] Wed: Behind-the-scenes / creator-demo
  - [ ] Fri: Occasion content (tied to next In-App Event from ASO plan)
  - [ ] Plus: 1–2 IG Stories/day with link sticker
- [ ] **Trending audio integration** — every Reel/TikTok uses trending audio when remotely fitting
  - [ ] Open TikTok / Reels creator tools, browse trending, pick before recording
  - [ ] Tools: Hypeauditor or Predis.ai for niche trend surfacing if scrolling becomes the bottleneck

---

## Weeks 5–6 (Jun 9–22) — Community + measurement

### D. Community moat

- [ ] **Engagement discipline** — 30 min/day on top 5 posts of the week
  - [ ] Reply to every comment in the first hour after posting (algorithm signal)
  - [ ] Like + reply to comments 24h after posting
  - [ ] DM engaged commenters with personalized follow-up
- [ ] **Facebook Groups sourcing**
  - [ ] Identify top 5–10 most active grandparenting groups (AARP forums, "Grandmas Connecting," "Grandparenting Together")
  - [ ] Team member joins, observes for 1–2 weeks before posting
- [ ] **Founder LinkedIn cadence established** — 1 post/week
  - [ ] Pillars: building-in-public updates, real grandparent reaction story, lessons learned, milestones

### E. Measurement
- [ ] First post-launch report (Day 30 vs baseline)
  - [ ] Bio link clicks per platform
  - [ ] Reach / engagement per Reel
  - [ ] UGC reposts shipped
  - [ ] Social-attributed installs (AppsFlyer + GA UTM)

---

## Weeks 7–9 (Jun 23 – Jul 13) — UGC engine product layer

### C. UGC supply (Tier 1 product spec — see `specs/creator-incentivization-tier1.md`)

- [ ] **Tier 1 spec engineering kickoff** — issue filed against ZoogIOS#2191 with the spec; engineering schedules ~5-day work
- [ ] **Tier 1 ships** — tag-on-share with story unlock reward
  - [ ] Pre-launch baseline: % of Zoogs shared to Instagram or TikTok
  - [ ] First 30 days of data: tag rate, reward grants, cap behavior
- [ ] **Tier 1.5 design conversation** — ad-pool consent (paid creative reuse). Spec only if Tier 1 produces real share volume

### B. Pinterest launch (slow-build channel)

- [ ] Pinterest profile setup, brand kit, board structure
- [ ] First 20 pins published (repurposed Reels still images, plus new pins from SEO blog content)
- [ ] Weekly cadence: 5–10 pins/week

---

## Weeks 10–12 (Jul 14 – Aug 3) — Compounding

### B. Distribution
- [ ] First creator collab — partner with one mid-tier grandparent creator on TikTok / IG (5K–50K followers) for a single collab post (relationship-based, not paid)

### C. UGC supply (Tier 2 if Tier 1 validated)
- [ ] Spec Tier 2: verified-public-post detection, manual submission, Zoog+ month reward
- [ ] If Tier 1 underperformed: pause Tier 2, investigate Tier 1 friction

### D. Community
- [ ] First "real contribution" posts in 2–3 Facebook groups (genuinely helpful, not Zoog-promotional)
- [ ] First press / partner outreach using a UGC moment as the hook

### E. Measurement
- [ ] 90-day report — measure all north-star metrics vs baseline
- [ ] Identify which content pillars / platforms / pillar combos are working; double down
- [ ] Identify which CTAs / bio links convert best; finalize
- [ ] Document creative library inventory for paid reuse readiness

---

## Steady-state cadence (after Week 12 / Aug 4 onwards)

- [ ] **Original Reels** (1–2/week) cross-posted to IG + TikTok + FB Reels + YT Shorts
- [ ] **IG Stories with link sticker** (daily-ish)
- [ ] **UGC reposts** (2–4/week as engine matures)
- [ ] **Pinterest** (5–10 pins/week)
- [ ] **Founder LinkedIn** (1 post/week)
- [ ] **Engagement** (30 min/day on top posts)
- [ ] **FB Groups** (3–5 contributions/week, no Zoog spam)
- [ ] **Trending audio review** (5 min/post)
- [ ] **Monthly review** — performance per platform per pillar; update content mix

---

## Content pillars

Four pillars cycle through the weekly rhythm:

| Pillar | Frequency | Format | Source |
|---|---|---|---|
| **Reaction Reels** | 1/week | UGC reposts of grandkids reacting to Zoogs | UGC engine (Tier 1 hashtag harvest, eventually Tier 2/3) |
| **Creator-led demos** | 1/2 weeks | Real grandparent recording a Zoog, voice + face | Internal production OR paid creator partner |
| **Occasions** | 1/2 weeks | Tied to upcoming In-App Event (Father's Day, Summer Reading, Halloween, etc.) | Internal production, themed hero asset reused for multiple posts |
| **Use-case stories** | 1/month | Long-distance / military / new-grandparent family stories | Internal production with featured family + their permission |

Plus Stories daily, Carousels when there's a substantive guide ("5 things to send your new grandchild").

---

## Tool stack (target ~$30–50/mo additional)

- **Buffer / Later / Metricool** ($15–25/mo) — cross-posting, scheduling, basic analytics
- **Stan / Beacons / Komi** ($0–15/mo) — link in bio with click tracking, OR custom `/start` page (no tool cost)
- **Brand24** (free trial → $50/mo if needed) — mention monitoring; manual works for now
- **Hypeauditor / Predis.ai** (free tiers OK) — trending audio + creator discovery
- **CapCut** (free) — auto-captions, light editing
- **Native platform analytics** — IG Insights, TikTok Analytics, FB Page Insights — free
- **AppsFlyer SmartLinks** — already paid — for per-platform / per-pillar attribution
- **Claude / ChatGPT** — already paid — for caption drafting, hashtag suggestions

Avoid: Hootsuite (overpriced for one-app), influencer-marketplace tools at this stage (manual outreach is fine for first 1–3 partnerships).

---

## Decision log

| Date | Decision | Rationale |
|---|---|---|
| 2026-05-14 | Goal: direct app install acquisition (with realistic expectations) | User selected; honest framing acknowledges 50–500 installs/mo realistic ceiling at 1–2 posts/week |
| 2026-05-14 | LinkedIn = founder personal account, not company page | Personal accounts get vastly more LinkedIn reach; B2C app doesn't need company LinkedIn presence |
| 2026-05-14 | Defer YouTube long-form to Q4 | High production cost vs. capacity; cross-post Shorts only for now |
| 2026-05-14 | Treat conversion mechanics (link in bio, CTAs, hashtags) as Week 1 priority | Highest impact-per-effort; everything else compounds on top |
| 2026-05-14 | UGC supply has both passive (Tier 1 harvest) and product-driven (Tier 1 spec) components | Hashtag harvest needs no engineering, ships in Week 3; in-product reward ships when engineering schedules |

---

## Open questions

- [ ] **Should LinkedIn company page be deprecated entirely?** Founder personal is the lever; company page may not be worth the production slot
- [ ] **Brevo (email) cross-promotion** — should every email push followers to social channels? Probably yes, but coordinate with the SEO/email plan
- [ ] **Should we run a "month one" giveaway** to seed the @ZoogMoment hashtag with content? Could accelerate the UGC engine but adds operational complexity
- [ ] **Tier 1.5 ad-pool consent** — only spec if Tier 1 share volume justifies; revisit Day 60
- [ ] **Pinterest commitment** — is it worth the 5–10 pins/week if growth is slow? Re-evaluate at Day 90
- [ ] **Apple Search Ads brand defense (`zoog`)** — already re-enabled; coordinate so social mentions of "@zooghq" or "search Zoog in the App Store" route through the brand-defended ASA flow
- [ ] **First few paid creator partnerships** — budget approval for $1.5–2.5K/mo for 3–5 mid-tier grandparent creators? Defer to Day 30 decision once organic baseline is real

---

## Cross-references

- App Store / ASA / In-App Events / CPPs / Featuring → [`q2-q3-26-ASO.md`](./q2-q3-26-ASO.md)
- Marketing site / SEO / email / attribution → [`q2-q3-26-SEO+landing-page-optimization.md`](./q2-q3-26-SEO+landing-page-optimization.md)
- UGC supply product spec → [`specs/creator-incentivization-tier1.md`](./specs/creator-incentivization-tier1.md)
- Featured-tab segmentation → filed as backlog issue, `needs-specs`
- Children doc strategic narrative → `https://zooghq.github.io/DataRoom/Children/`
