# Q2–Q3 2026 SEO & Landing Page Optimization Plan

**Created:** May 14, 2026
**Status:** Active
**Owner:** Marketing
**Companion plan:** [`q2-q3-26-ASO.md`](./q2-q3-26-ASO.md)

---

## Context

Marketing site (getzoog.com) is the **highest-quality install channel** by every measure — but at much smaller scale than its conversion rate justifies.

### What the GA4 data shows (May 2025 – May 2026)

| Stage | Number | Notes |
|---|---:|---|
| Total sessions | 38,724 | All channels |
| Real sessions (excl. Unassigned + not-set) | ~16,400 | Bot/broken-attribution traffic strips out 57% |
| Unique visitors | 26,251 | |
| Download CTA clicks (unique) | 1,324 | **5.04% click rate — half the share-recording bridge's 9.4%** |
| Download CTA clicks (total) | 1,880 | |
| AppsFlyer-attributed installs | ~993 | 53% of clicks complete install |
| **Subscription conversion (per AppsFlyer)** | **~15%** | **Highest in the portfolio** (vs ASA 11.4%, Meta 9.4%, Organic 4.4%) |
| **Revenue per install** | **$9.34** | **Highest in the portfolio** |

### Channel mix

| Channel | Sessions | Engagement |
|---|---:|---:|
| **Unassigned** ⚠ | 14,482 | 0.2% (broken attribution / bots) |
| Organic Search | 12,499 | 91.7% |
| Direct | 10,102 | 95.3% |
| Referral | 1,060 | 93.1% |
| Organic Social | 431 | 93.3% |
| Paid Social | 126 | 99.2% |
| Email | **5** | (essentially dead channel) |

### Top SEO winners (proven patterns to replicate)

The site already has 251 landing pages. The categories that pull traffic and engage:
- **Cultural moments**: `/why-is-baby-shark-so-popular` (1,987 sessions)
- **Competitor alternatives**: `/family-video-chat-app` (627), `/amazon-glow-alternatives` (460)
- **Direct intent**: `/apps-for-grandma` (490), `/storytelling-for-toddlers` (188)
- **Press features**: `/zoog-named-1-app-for-grandparents-by-scary-mommy` (666 sessions, **67s avg engagement** — highest of any page)
- **Long-tail content**: `/itsy-bitsy-spider-lyrics` (101), `/jokes/gabbys-jokes-knock-knock` (136)

### Diagnosis

The marketing site is fundamentally healthy — strong SEO foundation, real organic traffic, working competitor-alternative content, press placements. **The bottleneck is conversion, not traffic**: 5% download CTR on the marketing site vs. 9% on the much-lower-intent share-recording pages. Plus three secondary issues: data plumbing is broken (37% unattributed), email channel is at zero, and SEO content cadence has slowed.

**Strategic shift:** double the conversion rate on existing traffic first (highest leverage), then scale traffic via more SEO pages in proven categories, then activate email as the second free recurring channel.

---

## North-star metrics (90-day target)

| Metric | Today (May 2026) | 90-day target |
|---|---:|---:|
| Total monthly sessions | ~3,200/mo | 4,500–5,500/mo |
| Real sessions (excl. Unassigned) | ~1,400/mo | 4,000–5,000/mo |
| Download CTR (visitor → click) | 5.04% | 8–10% |
| Installs from marketing site (AppsFlyer) | ~80/mo | 250–400/mo |
| New SEO pages live | 0 added | 15–20 added |
| Email subscribers captured | 0 | 1,500–2,500 |
| Unassigned/(not set) traffic share | 57% | <15% |

---

## Workstreams

Six tracks. Most are independent so can run in parallel.

### A. Data Quality (fix the plumbing)
### B. Landing Page CTA Optimization
### C. SEO Content Engine
### D. Email Channel Activation
### E. Landing Page → App Store Deep Linking (CPP integration)
### F. Press / PR / Backlink Earning

---

## Week 1 (May 12–18)

**Get measurement clean before optimizing — otherwise A/B tests are noise.**

### A. Data Quality
- [ ] Audit GA4 / Google Tag Manager setup
  - [ ] Identify why 37% of sessions are "Unassigned" (broken referrer pass-through, missing UTM defaults, or bot traffic — likely a mix)
  - [ ] Identify why 7,871 sessions land on `(not set)` (tracking firing before page loads, single-page-app routing not registering, or an ad pixel firing without page context)
  - [ ] If bot traffic: enable bot filtering in GA4 admin
  - [ ] If broken referrer: fix in GTM
- [ ] Set up server-side event verification — confirm `Download Zoog for Free` event is firing on the right element with the right metadata
- [ ] Add UTM parameter conventions doc — every paid / partnership / press link should be UTM'd consistently going forward

### B. CTA Audit (no changes yet, just measure)
- [ ] Pull `/pricing`-specific download CTR (currently top-2 traffic but unknown conversion)
- [ ] Pull `/zoog-named-1-app-for-grandparents-by-scary-mommy` download CTR (67s engagement = high-intent visitors)
- [ ] Pull homepage `/` download CTR (15,992 sessions = baseline)
- [ ] Identify which pages have NO clear download CTA above the fold

### C. SEO Quick Inventory
- [ ] Pull list of all 251 indexed pages from GA4
- [ ] Identify pages with traffic but no app download CTA
- [ ] Identify pages where the CTA could lead to a more-relevant CPP (linkable once CPPs ship in the ASO plan)

### D. Email
- [ ] Confirm Brevo (or equivalent) is set up and SMTP/API keys are valid
- [ ] Confirm we have a working email-capture form component on the site (or identify what's needed to build one)

---

## Weeks 2–3 (May 19 – Jun 1)

### B. CTA Optimization — Phase 1 (highest-impact pages)

- [ ] **Homepage CTA refresh**
  - [ ] Add sticky bottom-of-screen "Download Free" button on mobile
  - [ ] Move 4.9★ / 20K+ ratings social proof above the fold
  - [ ] Add multiple CTAs (after each value-prop section, not just hero)
  - [ ] Test new CTA copy variants (queue 3 for A/B):
    - "Download Zoog for Free"
    - "Get Your First Story Free"
    - "Try Zoog — Loved by 20,000+ Families"
- [ ] **Pricing page CTA refresh**
  - [ ] Audit current CTA placement — pricing-page CTRs should be 2–3× the site average; if not, that's the biggest single fix
  - [ ] Add free trial / first-story-free promise above the price table
  - [ ] Add testimonials inline with pricing tiers
- [ ] **Press page CTA add**
  - [ ] `/zoog-named-1-app-for-grandparents-by-scary-mommy` has 67s engagement and currently lacks a clear next step
  - [ ] Add sticky right-rail or top "Download Zoog Free" card with the Scary Mommy quote

### A. Data Quality
- [ ] Verify Unassigned + (not set) shares dropped after Week 1 fixes
- [ ] If still elevated, escalate to a deeper GTM / GA4 audit

---

## Weeks 4–6 (Jun 2 – Jun 22) — SEO Content Sprint

### C. SEO Content Engine — Wave 1

Build 10 new pages in the proven categories. Each ~800–1,200 words, original photography or quality stock, internal links to homepage + pricing + library, and a clear download CTA module.

**Competitor alternatives** (proven category — `/amazon-glow-alternatives` and `/family-video-chat-app` already work):
- [ ] `/caribu-alternative` — direct competitor, recently acquired by Mattel and possibly stagnating
- [ ] `/bookful-vs-zoog`
- [ ] `/marco-polo-alternative-for-families`
- [ ] `/storyline-online-alternative-personalized`

**Direct grandparent intent** (proven — `/apps-for-grandma` works):
- [ ] `/best-apps-for-grandparents-2026`
- [ ] `/long-distance-grandparent-app`
- [ ] `/grandparent-bonding-activities`

**Cultural moments** (proven — Baby Shark works):
- [ ] `/gabbys-dollhouse-songs` (you already have related content — extend it)
- [ ] `/why-is-bluey-so-popular`
- [ ] `/ms-rachel-alternative-for-bedtime`

### B. CTA Optimization — Phase 2
- [ ] Apply CTA template (sticky button, social proof, multiple placements) to top-20 landing pages by traffic
- [ ] Document the CTA template as a reusable component so all new SEO pages use it by default

---

## Weeks 7–9 (Jun 23 – Jul 13) — Email Activation + SEO Wave 2

### D. Email Channel Activation

- [ ] **Email capture form deployment**
  - [ ] On `/library` page: gate one premium-feel preview behind email signup ("See the full library for free — enter your email")
  - [ ] On `/pricing` page: "Email me a discount code" capture
  - [ ] On long-form blog posts: "Get our 10 best stories to share with grandkids" PDF gate
  - [ ] On exit intent (homepage): "Don't leave — get a free Zoog story for your grandchild"
- [ ] **Welcome email sequence (Brevo automation)**
  - [ ] Email 1 (immediate): "Welcome — your free story is here" + App Store link
  - [ ] Email 2 (day 2): grandparent-creator story / case study
  - [ ] Email 3 (day 5): library preview, sharing-loop story
  - [ ] Email 4 (day 10): pricing / Zoog+ subscription pitch
- [ ] **Reactivation campaign for existing 200K-household base**
  - [ ] Pull list of users with valid emails who haven't opened the app in 60+ days
  - [ ] "What's new this month" email — feature recent AI-pipeline releases + In-App Events
  - [ ] One-time send, then weekly cadence to engaged segment

### C. SEO Content Engine — Wave 2

Build the next 10 pages, prioritizing:
- [ ] **Holiday / occasion pages** (each becomes evergreen but seasonally surges)
  - [ ] `/halloween-stories-for-kids`
  - [ ] `/christmas-stories-personalized-app`
  - [ ] `/birthday-story-for-grandchild`
  - [ ] `/mothers-day-story-from-grandma`
  - [ ] `/fathers-day-grandfather-stories`
- [ ] **Long-tail kids song lyrics** (`/itsy-bitsy-spider-lyrics` works — extend pattern)
  - [ ] `/wheels-on-the-bus-lyrics-and-video`
  - [ ] `/twinkle-twinkle-little-star-lyrics-printable`
  - [ ] `/old-macdonald-lyrics-and-printables`
- [ ] **Educational / parent-intent**
  - [ ] `/screen-time-alternatives-for-toddlers`
  - [ ] `/early-literacy-tips-for-grandparents`

---

## Weeks 10–12 (Jul 14 – Aug 3) — Compounding

### E. Landing Page → App Store Deep Linking
- [ ] As CPPs ship in the ASO plan, swap App Store links from generic to use-case-specific:
  - [ ] `/apps-for-grandma` → CPP 1 (Grandparent Creator)
  - [ ] `/family-video-chat-app` → CPP 2 (Family Sharing)
  - [ ] `/birthday-story-for-grandchild` → CPP 5 (Birthday Stories)
  - [ ] `/halloween-stories-for-kids` → CPP 6 (Holiday Cards) once Halloween hero swapped in
- [ ] Add CPP-aware deep-link logic to the homepage CTA based on UTM params (e.g., `utm_campaign=grandparent` lands on CPP 1)

### F. Press / Backlinks
- [ ] Outreach to parenting / grandparenting publications for new press features (use the AI-pipeline content angle, the 4.9★ rating, the Children-doc 4-arc story as hook)
- [ ] Submit to indie app directories (Indie App Gallery, Product Hunt, kids-app review sites)
- [ ] Reach out to grandparenting Facebook groups and newsletters with a partnership offer
- [ ] Track new backlinks weekly via AppTweak / Ahrefs free tier / GA Referral channel

### Measurement
- [ ] First post-refresh report — measure CTR lift, session lift, install lift vs Apr 2026 baseline
- [ ] Identify which Wave 1 / Wave 2 SEO pages are ranking; double down on the winners
- [ ] Email open / CTR baseline

---

## Steady-state cadence (after Week 12 / Aug 4 onwards)

- [ ] **2 new SEO pages per week** (8/month, sustainable single-person pace)
- [ ] **CTA refresh test** every 30 days (rotating: copy, placement, design)
- [ ] **Email send** weekly to engaged segment, monthly broader
- [ ] **Press pitch** monthly to one publication
- [ ] **GA4 quality audit** monthly (verify Unassigned stays <15%)
- [ ] **Quarterly SEO opportunity review** — what new search trends, competitor gaps, cultural moments warrant pages

---

## Tool stack (target ~$50/mo additional, beyond the ASO plan's stack)

- **Google Tag Manager** (free) — for CTA tracking, A/B test deployment
- **GA4** (free) — already installed, needs cleanup
- **Brevo** (~$20–50/mo) — email automation, already migrating
- **Vercel / Cloudflare A/B testing** (free for simple tests) — variant routing for homepage CTA tests
- **Or:** **VWO** ($199/mo) / **Convert.com** ($199/mo) if more polished A/B testing UI is needed
- **Ahrefs / SEMrush free tier** — backlink + keyword discovery; or just AppTweak if it covers web SEO too
- **Claude / ChatGPT** ($20/mo) — already have — for SEO content drafting

Avoid: Optimizely (enterprise), Adobe Target (enterprise), big SEO platforms unless we get to >50 indexed pages and need the workflow tooling.

---

## Decision log

| Date | Decision | Rationale |
|---|---|---|
| 2026-05-14 | Build email channel separately, not as part of broader social | Email at 5 sessions/year is a giant unused asset; deserves its own focused launch with welcome sequence + reactivation send |
| 2026-05-14 | Prioritize CTA fix over SEO content scaling | 5% → 10% CTR doubles installs from existing traffic; new SEO pages take 60–90 days to rank meaningfully |
| 2026-05-14 | Defer paid SEO tooling (Ahrefs paid tier, etc.) | Free tiers + AppTweak (already paid) cover monitoring needs at this stage |
| 2026-05-14 | Use existing Brevo migration rather than new email tool | Already in workspace; not worth re-tooling |

---

## Open questions

- [ ] What does the **"Unassigned" 14,482 sessions** actually represent? Bot, broken UTM, or something else? Resolution affects whether the real conversion rate is 5% or higher
- [ ] Why does **`(not set)`** show up as the second-most-popular landing page (7,871 sessions)? Tag misfire or real?
- [ ] What's the **`/pricing` download CTR** specifically? If it's anything close to the site average, that's the biggest single CTA fix opportunity
- [ ] What's currently driving the **666 sessions to the Scary Mommy press page**? Direct from the article still, or from internal navigation? Tells us whether press placement is still alive
- [ ] Are the **job postings** distorting visitor metrics enough to warrant filtering them out of marketing-site analytics?
- [ ] Should we consider **App Clip** integration for `getzoog.com` pages (vs only on share-recording pages)? Lets users sample Zoog inline before committing to install

---

## Cross-references

- App Store / ASA / In-App Events / CPPs / Featuring → [`q2-q3-26-ASO.md`](./q2-q3-26-ASO.md)
- Featured-tab segmentation → filed as backlog issue, `needs-specs`
- Children doc strategic narrative → `https://zooghq.github.io/DataRoom/Children/`
