# The "₹999 → ₹9" Funnel: How It Actually Makes Money

> Case study: Be10x "AI Tools Workshop" ad seen in WhatsApp Status, Sept 2026.
> The same playbook is run by Skill Nation, Growth School / Outskill, and dozens of smaller
> coaches. Be10x just runs it at the largest scale (claims 5M+ learners via 800+ live workshops,
> founded 2023 by two IIT-KGP grads, bootstrapped — no external funding).

---

## 1. Decode the ad you clicked

The URL is a gift — the UTM parameters are Be10x's own internal labelling of the campaign:

```
utm_source   = Whatsapp_Status
utm_medium   = AID | 30-65+ | M+F | Healthcare Operations
utm_campaign = XL(A) | OTO | Conversion
utm_content  = Laid off Employees_02/07/2026 (Video)
fbclid       = PAdHNhZg...   (Meta click ID; contains app_id 994766073959253)
```

What each piece tells you:

| Param | Meaning | Insight |
|---|---|---|
| `Whatsapp_Status` | Placement: ads between Status updates (Meta Ads Manager → placements → WhatsApp Status) | Status is still under-priced vs Facebook/Instagram feed; CPCs of ₹5–₹25 in India. They're arbitraging cheap attention while it lasts. |
| `AID` | Almost certainly *Advantage+ Audience* (Meta's AI targeting) | They're letting Meta's algorithm find buyers rather than hand-picking interests. This only works well if you feed it a *Purchase* event — see §3. |
| `30-65+ / M+F` | Age 30 to 65+, both genders | Not students. Mid-career, salaried, has a UPI app, anxious about AI. |
| `Healthcare Operations` | Interest / job-title segment | They run **one ad set per profession** (you'd also find "Banking Ops", "HR", "Teachers", "Sales"...). Same workshop, different ad copy so it feels made for *you*. |
| `XL(A)` | Campaign tier label (their budget-size / test-cell naming) | They run many parallel cells and scale the winners. |
| `OTO` | **One-Time Offer** | There is an upsell *immediately after* the ₹9 payment (order bump / "add recordings + bonus for ₹499 — only on this page"). See §2 step 3. |
| `Conversion` | Campaign objective = Conversions (Purchase), not Traffic or Leads | Critical. They pay Meta to find people who *complete a payment*, and the ₹9 makes that event cheap and abundant. |
| `Laid off Employees_02/07/2026 (Video)` | Creative angle + date + format | The hook is *fear* ("laid off? AI took your job? Learn AI in 3 hours"). Dated so they can track creative fatigue. Video because Status is a full-screen vertical video placement. |

So the "unbelievable price" is the least interesting part of the ad. The interesting part is
that they are running **profession-segmented fear-based video creatives, optimised for a
Purchase event, with an immediate one-time upsell**.

---

## 2. The funnel, step by step

```
WhatsApp Status video ad
        │  CPC ₹5–25 (Status) / ₹2–25 (FB)
        ▼
Landing page  ─────────────────────────────────────────
  "3-Hour LIVE AI Tools Workshop"                      │
  ₹̶9̶9̶9̶  ₹9   ⏱ timer   "Only 137 seats left"          │
  "Trusted by 5,00,000+ learners"  ★ 4.9              │
  Certificate + ₹5,000 worth of bonuses               │
        │  Landing conv. 20–40% → cost per ₹9 buyer ≈ ₹150–₹400
        ▼
₹9 payment (UPI)  → phone number verified, WhatsApp opt-in, Meta Purchase pixel fires
        │
        ▼
OTO page (One-Time Offer)
  "Add lifetime recordings + prompt library for ₹499 — this page only"
  Takes 10–25% of buyers. Recovers a chunk of ad spend on the spot.
        │
        ▼
3–5 days of WhatsApp nurture
  reminders, "pre-work", founder story, testimonials, calendar invite
  → show-up rate 40–55% (vs ~20–30% for a free webinar)
        │
        ▼
"Live" workshop (Zoom/own platform, often pre-recorded + live chat)
  0:00–1:30  genuine teaching: ChatGPT, Excel/PPT with AI, image tools
  1:30–3:00  THE PITCH: "Our flagship program, normally ₹X, today only ₹Y,
             first 50 people get bonus, EMI available, offer closes when
             the session ends"
        │  2–5% of attendees buy
        ▼
High-ticket program: ~₹35,000–₹40,000 typical; packages up to ~₹1,00,000
  Sales team calls non-buyers for 3–7 days ("special extension for you")
        │
        ▼
Inside the program: further upsells (mentorship, placement, "mastermind")
```

Reviewer reports back this up: Trustpilot reviewers say "90+ minutes talking about their paid
course"; a LinkedIn commenter paid ~₹40,000 after the ₹9 workshop; another reviewer saw packages
up to ~₹1 lakh; several say the "live" workshop appeared pre-recorded.

---

## 3. Why ₹9 specifically (and not free, and not ₹499)

**It's a qualifier, not a price.**

1. **Payment-verified lead.** Anyone who completes a ₹9 UPI payment has a working payment method
   and the *habit* of paying online. Free-webinar registrants include a huge share of people who
   will never spend ₹40,000.
2. **Feeds Meta's algorithm a Purchase event.** With a Conversions campaign, Meta needs ~50
   conversion events per ad set per week to exit "learning". At ₹9, they get thousands of Purchase
   events cheaply, so Meta's model learns *who buys*, then finds more buyers. A free lead-form
   campaign optimises for *who fills forms* — a very different, lower-quality population.
3. **Commitment & consistency.** Behavioural econ: once someone has paid you *anything*, they
   rationalise the decision and are far more likely to buy again. Tripwire-funnel data commonly
   shows 60–70% of tripwire buyers making a second purchase vs 5–20% for cold leads.
4. **Anchoring.** ₹̶9̶9̶9̶ → ₹9 makes ₹9 feel like theft-level value, and later ₹̶7̶9̶,̶9̶9̶9̶ → ₹39,999
   feels like the same kind of "deal" they already trusted once.
5. **Show-up rate roughly doubles.** People show up to what they paid for.
6. **₹9 is below the "think about it" threshold** — it's less than a chai. Nobody consults their
   spouse about ₹9. ₹499 would cut conversions 5–10×.
7. **WhatsApp number capture.** UPI checkout = verified mobile number. The whole nurture and
   follow-up sales process runs on WhatsApp, where open rates are 80%+ vs 20% for email.

The ₹9 itself is a rounding error. If they run 10,000 registrations a week, ₹9 × 10,000 = ₹90,000
against an ad spend of ₹15–40 lakh. It exists for the seven reasons above, not for revenue.

---

## 4. Unit economics (illustrative, using 2026 Indian benchmarks)

Assumptions (all from cited sources in `sources.md`; ranges are wide, so treat as a model not a fact):

| Metric | Benchmark range | Model value |
|---|---|---|
| Cost per ₹9 registration (paid) | ₹150–₹400 (edtech CPL India); some say ₹500–₹1000 now | **₹250** |
| OTO take rate × price | 10–25% × ₹299–₹999 | 15% × ₹499 |
| Show-up rate (paid webinar) | 40–55% | **45%** |
| Attendee → high-ticket buyer | 2–5% (high-ticket coaching "action" benchmark 5–12%) | **3%** |
| High-ticket price | ₹35k–₹1L | **₹40,000** |
| Refund/chargeback | 5–15% | 10% |

For **₹25,00,000 ad spend** in a month:

```
Registrations        = 25,00,000 / 250            = 10,000
₹9 revenue           = 10,000 × 9                 =    ₹90,000
OTO revenue          = 10,000 × 15% × 499         =  ₹7,48,500
Attendees            = 10,000 × 45%               =     4,500
High-ticket buyers   = 4,500 × 3%                 =       135
High-ticket revenue  = 135 × 40,000               = ₹54,00,000
Less refunds 10%                                  = ₹48,60,000
─────────────────────────────────────────────────────────────
Gross revenue        ≈ ₹57,00,000  →  ROAS ≈ 2.3× on ₹25L
```

Then subtract: sales team commissions (~10–15% of high-ticket), payment gateway (2%), EMI
financing cost (they subsidise 0% EMI — 3–8%), delivery (mentors, platform), GST handling.
Net margin lands somewhere around 20–35% *if* the 3% close holds. Every 1 percentage point of
close rate is worth ~₹18 lakh here — which is exactly why the last 90 minutes of the workshop is
a hard pitch and why there's a phone sales team calling non-buyers.

**Sensitivity:** at ₹500 CPL and 2% close, the same ₹25L produces ~₹20L in high-ticket revenue —
a loss. The model lives or dies on (a) cheap registrations, (b) the close rate. That's why they
segment by profession (better relevance → cheaper CPL) and use fear hooks (higher urgency → better
close).

Use `funnel-calculator.html` in this folder to play with these numbers.

---

## 5. The psychological toolkit they use (so you recognise it — and so you decide what you're willing to use)

| Tactic | Where | Mechanism |
|---|---|---|
| Price anchoring | ₹̶9̶9̶9̶ → ₹9; ₹̶7̶9̶,̶9̶9̶9̶ → ₹39,999 | Reference price makes the real price feel like a gain |
| Fake/soft scarcity | "137 seats left", countdown timer resets on refresh | Loss aversion |
| Deadline | "Offer ends when this session ends" | Prevents deliberation, kills "let me think" |
| Social proof | "5,00,000+ learners", "★4.9", logos of Amazon/Google where alumni "work" | Herd effect; the logos are usually *employers of attendees*, not partners |
| Authority | "IIT graduates", "TEDx speaker", press coverage (mostly paid ANI/PR-wire releases republished by Tribune/Business Standard/ThePrint) | Credibility transfer |
| Fear framing | "Laid off employees", "AI will replace you" | Pain > aspiration for cold traffic |
| Identity targeting | "for Healthcare Operations professionals" | Feels personalised; increases relevance score → cheaper ads |
| Reciprocity | 90 min of real free teaching before the pitch | You feel you owe them |
| Commitment ladder | ₹9 → ₹499 → ₹39,999 → ₹1L | Each yes makes the next yes easier |
| Certificate | "Get a certificate" for a 3-hour session | Trophy motivation; LinkedIn-shareable → free distribution |
| Fake live | Pre-recorded video with live chat moderators | Scale: one recording, 10,000 "live" attendees, zero marginal delivery cost |

---

## 6. Why it's weakening (2025–26) — and the risks if you copy it

1. **Lead costs up 5–10×.** Indian marketers (e.g. Digital Deepak's "Death of the ₹99 webinar
   funnel") report workshop leads that cost ₹100 in 2020 now cost ₹500–₹1,000. Everyone copied
   the playbook; the auction got expensive.
2. **Audience literacy.** People now recognise "₹9 workshop = 90-minute sales pitch". Quora,
   Trustpilot, LinkedIn "awareness posts" and YouTube reviews rank for the brand name.
3. **Regulatory heat.** Education is the #1 most-complained-about ad category at ASCI (again in
   2025). CCPA fined 19 coaching institutes ₹61.6L in 2024 under the Consumer Protection Act 2019
   for misleading ads; guidelines specifically call out false urgency, fake scarcity, and unproven
   outcome claims ("3× salary hike") — i.e. the exact toolkit in §5. The 2023 Dark Patterns
   guidelines explicitly name "false urgency" and "drip pricing".
4. **Refund and reputation drag.** Once you have a phone sales team paid on commission, refund
   complaints become structural. That caps how long a brand can run before it needs a new brand
   (note Growth School → Outskill).
5. **Platform risk.** Meta periodically bans ad accounts for "misleading claims" and "get rich
   quick" framing. Running this as a solo operator with one ad account is fragile.

**Verdict:** it is a real, working, profitable model — at scale, with a sales team, a content
team, a compliance-tolerant brand, and a willingness to be disliked by ~30% of your customers. It
is *not* a good fit for a solo technical founder, and that's the subject of file 02.

---

## 7. What's genuinely worth stealing from it (ethically)

- **Charge a token amount instead of "free"** — for a pilot, a demo slot, a setup. It filters
  tyre-kickers and doubles show-up.
- **Optimise Meta for a real conversion event**, not clicks or leads.
- **Segment creatives by profession/vertical**; same product, different first sentence.
- **Order bump / OTO** right after any payment — highest-converting moment you'll ever have.
- **Run the nurture and follow-up on WhatsApp**, not email.
- **Teach something real before you sell** — the reciprocity is legitimate if the teaching is.
- **Have a deadline that is true** (cohort starts on X, price rises on Y because Z).
