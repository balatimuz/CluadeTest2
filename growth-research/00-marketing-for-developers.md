# Marketing for Developers — read this first

You build WhatsApp bots, Odoo bots, AI workflows and voice agents. You have never run a paid ad.
This file explains everything in the other two docs using things you already know.

---

## 1. The whole thing is a pipeline with a leaky bucket at every stage

Think of it as a request flowing through middleware. At each stage, most requests get dropped.

```
   1,000 people see your ad
     │  ~2% tap it                       ← "CTR" (click-through rate)
     ▼
      20 people land on your page / WhatsApp
     │  ~30% do the first thing you ask  ← "conversion rate"
     ▼
       6 people pay ₹9  (or start a chat, or book a demo)
     │  ~50% actually show up later      ← "show-up rate"
     ▼
       3 people sit through your workshop / demo
     │  ~3–5% buy the real thing         ← "close rate"
     ▼
     0.1 customer   (i.e. 1 customer per ~10,000 impressions)
```

**Marketing is just measuring the drop-off at each stage and reducing it.** That's it. Every
buzzword is a name for one stage or one lever.

---

## 2. Glossary — every term I used, in one line each

| Term | Plain meaning | Developer analogy |
|---|---|---|
| **Meta Ads / Ads Manager** | Facebook's dashboard where you create ads that show on Facebook, Instagram, WhatsApp Status | AWS console for buying attention |
| **Placement** | *Where* the ad shows: FB feed, Instagram Reels, WhatsApp Status, etc. | Which server region you deploy to |
| **Impression** | One person saw your ad once | One request hit your server |
| **CPM** | Cost per 1,000 impressions (₹50–₹400 in India) | Price per 1,000 requests |
| **CTR** | % of viewers who tapped the ad (1–3% is normal) | Cache hit rate — tiny but crucial |
| **CPC** | Cost per click (₹5–₹25 on WhatsApp Status) | Price per successful request |
| **Landing page** | The single page a person lands on after tapping the ad. One goal, one button. | A single-endpoint microservice |
| **Conversion** | The person did the thing you wanted (paid, registered, started a chat) | A `200 OK` on the endpoint you actually care about |
| **Conversion rate** | % of visitors who converted | Success rate |
| **Lead** | A person who gave you their phone number / email | A row in your `prospects` table |
| **CPL** (cost per lead) | Ad spend ÷ number of leads (₹150–₹400 for edtech in India) | Cost per row inserted |
| **CAC** (customer acquisition cost) | Ad spend ÷ number of *paying* customers | Cost per row that reaches `status = paid` |
| **LTV** (lifetime value) | Total profit one customer gives you before they leave | Total revenue per row over its lifetime |
| **LTV : CAC** | LTV divided by CAC. ≥ 3:1 is healthy. | Return on infra spend. Below 1:1 you're burning money. |
| **ROAS** (return on ad spend) | Revenue ÷ ad spend. 2× means ₹100 of ads made ₹200 of revenue. | Throughput per rupee |
| **Churn** | % of paying customers who cancel each month (3–7% for SMB SaaS) | Rows deleted per month |
| **Payback period** | Months until a customer's payments cover what you spent to acquire them | Break-even |
| **Funnel** | The whole pipeline in §1 | Your middleware chain |
| **Tripwire / low-ticket offer** | A tiny first purchase (₹9, ₹99, ₹499) whose job is to get a *first* yes, not to make money | A handshake before the real payload |
| **OTO** (one-time offer) / **order bump** | An upsell shown *right after* someone pays, "only on this page" | Post-commit hook — fires once, while the connection is hot |
| **High-ticket** | The expensive thing (₹35,000+) that actually makes the money | The paid tier |
| **Upsell** | Selling a more expensive thing to an existing buyer | Tier upgrade |
| **Nurture** | The sequence of messages between "signed up" and "bought" — reminders, stories, proof | A cron job that pings the row until it changes state |
| **Show-up rate** | % of registrants who attend | Job completion rate |
| **Close rate** | % of attendees who buy | Final-stage conversion |
| **Webinar / workshop** | A live (or "live") video session used to teach and then sell | A demo call at scale |
| **Creative** | The actual ad — the video/image + text | The payload |
| **Hook** | The first 2 seconds / first sentence of the creative | The subject line |
| **Angle** | The emotional frame — fear ("laid off?"), aspiration ("earn ₹1L/mo"), curiosity | The framing of the user story |
| **Targeting** | Who Meta shows the ad to — age, location, interests, job | `WHERE` clause on 2 billion users |
| **Advantage+ Audience** | Let Meta's ML pick the audience instead of you | Auto-scaling instead of manual provisioning |
| **Campaign objective** | What you tell Meta to optimise for: Traffic (clicks), Leads (forms), **Sales/Conversions (purchases)** | The loss function. Pick the wrong one and the model optimises for the wrong thing. |
| **Meta Pixel / Conversions API (CAPI)** | A JS snippet / server webhook that tells Meta "this person just paid" so it can learn who buys | Your analytics event → sent back to the ad platform as training data |
| **Purchase event** | The specific signal "money changed hands" | The label in your training data |
| **Learning phase** | Meta needs ~50 conversion events per week to figure out who to target | Model needs a minimum batch size to converge |
| **Ad set** | A group of ads sharing one audience + budget | A deployment group |
| **Scaling** | Increasing budget on what works, ≤20% every few days | Rolling out gradually |
| **Creative fatigue** | An ad stops working because the same people have seen it too often | Cache gone stale |
| **Anchoring** | Show a big price first so the real price feels small (₹̶9̶9̶9̶ → ₹9) | Setting the baseline |
| **Scarcity / urgency** | "137 seats left", countdown timer | Rate-limit warnings that make you act now |
| **Social proof** | "5,00,000 learners", ★4.9, logos | GitHub stars |
| **Click-to-WhatsApp ad** | An ad whose button opens a WhatsApp chat with your business number | A deep link straight into your bot |
| **BSP** | Business Solution Provider — resellers of WhatsApp API (AiSensy, Wati, Gupshup) | Managed hosting vs going direct to Meta Cloud API |
| **Vertical** | One specific industry (clinics, salons, coaching) | A domain-specific module |
| **Horizontal** | "For any business" | A generic framework |
| **Micro-SaaS** | Small software product, monthly subscription, 1–3 people run it | Your bot, with a Razorpay subscription attached |
| **Productized service** | A fixed-scope service sold at a fixed price ("WhatsApp bot setup: ₹25,000") | A fixed-price implementation package |
| **MRR** | Monthly recurring revenue | Sum of active subscriptions |
| **ASCI / CCPA** | India's ad-standards body / consumer-protection regulator. They fine fake urgency and false claims. | Compliance |

---

## 3. The ₹9 funnel, explained as code

Here is Be10x's business as pseudo-code. This is literally all it is.

```python
# Stage 1: buy attention
for profession in ["Healthcare Ops", "Banking", "HR", "Teachers", ...]:
    meta.run_ad(
        placement   = ["whatsapp_status", "ig_reels", "fb_feed"],
        audience    = Advantage_Plus(age=(30, 65), seed_interest=profession),
        creative    = video(hook=f"Laid off? {profession} jobs are going to AI. Learn AI in 3 hrs."),
        objective   = "PURCHASE",          # <-- optimise for people who PAY, not click
        landing     = "/ai-tools-fb4b",
    )

# Stage 2: the ₹9 handshake
def on_landing_page_view(user):
    show(anchor_price=999, real_price=9, timer=True, seats_left=random(100, 200))

def on_payment(user, amount=9):          # UPI success webhook
    meta.pixel.fire("Purchase", user)      # <-- training data for Stage 1's model
    db.leads.insert(phone=user.phone, opted_in=True)
    show_oto(user, "Recordings + prompt pack, ₹499, this page only")   # ~15% take it
    whatsapp.schedule_nurture(user, days=3)  # reminders, founder story, testimonials

# Stage 3: the workshop
def workshop(attendees):                  # ~45% of payers show up
    teach(minutes=90)                      # genuinely useful → reciprocity
    pitch(minutes=90, price=39999, anchor=79999, deadline="when this call ends", emi=True)
    buyers = [a for a in attendees if a.buys()]   # ~3%
    sales_team.call(attendees - buyers, days=7)    # "special extension for you"
    return buyers

# The math
ad_spend      = 25_00_000
registrations = ad_spend / 250            # ₹250 per ₹9 buyer  → 10,000
attendees     = registrations * 0.45      # → 4,500
buyers        = attendees * 0.03          # → 135
revenue       = buyers * 40_000           # → ₹54,00,000   (ROAS ≈ 2.2×)
```

Three non-obvious things:

1. **The ₹9 exists to fire `meta.pixel.fire("Purchase")`.** A free signup can't do that. Meta's
   targeting model is only as good as its labels, and "paid ₹9" is a far better label than "filled
   a form". This is the single most important idea in the whole doc.
2. **The workshop is one recording played to thousands.** Marginal delivery cost ≈ 0. It's a
   stateless service.
3. **The margin is thin.** Drop the close rate from 3% to 2% and they lose money. That's why the
   pitch is aggressive — the business is one config value away from unprofitable.

---

## 4. Why I told you *not* to copy it

Because it's not a software business. Its moat is:
- a creative team producing dozens of video ads a week,
- a phone sales team on commission,
- a tolerance for 1-star reviews and regulator notices.

None of those are things you're good at or want to be. You'd be an inexperienced player in a
game where the incumbents have a 10-crore ad budget and 3 years of Purchase-event training data.

---

## 5. What your existing skills are actually worth

Map what you've built to what people pay for:

| You built | Who has this problem, badly | What they'd pay for | Roughly |
|---|---|---|---|
| **WhatsApp group bots** | Coaching institutes, apartment RWAs, clinics, D2C sellers drowning in group messages | Auto-answer FAQs, collect fees/orders, push reminders, moderate | ₹1,500–₹4,000/mo |
| **Odoo bots** | Every SME already on Odoo (India has thousands of Odoo partners and lakhs of installs) | "Ask your ERP on WhatsApp": stock check, invoice status, approve PO, daily sales summary as a voice note | ₹3,000–₹10,000/mo or ₹50k–₹2L one-time |
| **AI workflows** | Agencies, CA firms, real-estate brokers | Lead qualification, document intake, follow-up sequences | ₹15k–₹50k setup + retainer |
| **AI voice agents** | Clinics, coaching institutes, car dealers, real-estate — anyone whose phone rings more than they can answer | AI receptionist that picks up, books, reminds, in Hindi/Tamil/Telugu | ₹3,000–₹8,000/mo (voice minutes are a real COGS — price carefully) |

**The Odoo one is the sleeper.** Almost nobody is combining "Odoo bot" + "WhatsApp" + "AI" for
Indian SMEs, and Odoo customers have *already proven* they pay for software. Odoo partners
(implementation agencies) would resell it for you — that's a distribution channel you don't have
to pay Meta for. Consider making this the productized service (option C in file 02) while the
clinic/coaching WhatsApp agent is the SaaS (option B).

---

## 6. The one plan, with zero jargon

**Step 1 — Don't touch ads yet.** Take one of your existing bots (WhatsApp + AI voice for a
clinic, or WhatsApp + Odoo for an SME). Find 5 businesses through people you know. Install it
free. Ask them every week: "what did it save you?" Write those numbers down. This is your
*proof*. Nothing else in marketing works without proof.

**Step 2 — Put a price on it.** ₹499 for a 14-day setup on their own number, then ₹2,499/month.
Not free. People who pay ₹499 show up, take it seriously, and tell you the truth.

**Step 3 — Make one 15-second vertical video.** Screen-record your bot handling a real message.
Text on top: "Dr. X's clinic missed 23 appointments last month. Now WhatsApp handles it. Tap to
try it." The button opens *your bot*. The prospect plays with the bot. The bot is the sales pitch.

**Step 4 — Spend ₹1,000/day for 2 weeks** (₹14,000 total). In Meta Ads Manager: objective =
"Sales", conversion location = "WhatsApp", placement = WhatsApp Status + Instagram Reels, audience
= let Meta choose ("Advantage+") with a hint like "dentist" or "clinic owner", cities = yours + 2
nearby. Connect Razorpay's payment-success webhook to Meta's Conversions API so every ₹499
payment tells Meta "this kind of person buys".

**Step 5 — Look at three numbers only.**
- Cost per WhatsApp conversation (want: < ₹80)
- % of conversations that pay ₹499 (want: > 5%)
- % of ₹499 payers who convert to ₹2,499/mo (want: > 40%)

If all three hit, spend more. If one doesn't, that stage is broken — fix *that* stage (better
video → cheaper conversations; better bot demo → more ₹499s; better onboarding → more monthly).

**Step 6 — Everything else in files 01 and 02 is detail you can read once this is running.**

---

## 7. Things a developer gets wrong the first time (so you don't)

- **Building more features before anyone pays.** The 5 free pilots are your spec. Ship nothing
  they didn't ask for.
- **Making the ad about the tech.** "AI-powered NLP WhatsApp automation" → nobody cares.
  "Never miss a patient call again" → clinic owner cares.
- **Optimising the ad for Clicks/Traffic.** Meta will happily find you 10,000 people who click
  and never buy. Always pick Sales/Conversions.
- **Free trial.** Free = no commitment, no show-up, no Purchase event. Charge ₹499.
- **Going horizontal.** "WhatsApp bot for any business" competes with AiSensy at ₹999/mo. "WhatsApp
  receptionist for dental clinics" competes with nobody and a dentist buys it in one conversation.
- **Judging after ₹2,000 of spend.** Meta needs ~50 conversions to learn. Budget ₹15k minimum
  before deciding anything.
- **Faking urgency.** You want these SMBs as customers for years. Also, the CCPA fines it.
