# WhatsApp Business OS — mini CRM + mini ERP inside WhatsApp (no Odoo, no app)

Plain-language visual version: `whatsapp-business-os.html`. This file is the compact spec for
when you start building.

## Positioning
"Run the whole shop from WhatsApp." Owner-facing, natural-language, Indian languages. One
business number serves both the owner (records, questions, reminders) and their customers
(invoice, UPI pay link, reorder, status). Competes with *habit* (paper udhaar book + personal
WhatsApp), not with Vyapar's feature list.

## Market gap (2026)
| Segment | Players | Why they leave the gap |
|---|---|---|
| Customer-facing inbox/chatbot | Wati (~₹2,500/mo), Interakt (₹999/mo–₹3,499/qtr), DoubleTick (₹3,499/qtr), AiSensy, Gallabox | Dashboard-first, built for D2C brands with support teams |
| Owner-facing billing/ledger apps | Vyapar (1.5 Cr businesses), Khatabook, OkCredit (free, weak monetisation), myBillBook, Swipe | Separate app; WhatsApp only as a share button |
| WhatsApp CRM + billing bundles | Cleomitra, Groweon, Kraya (~₹999/mo) | Still dashboard-first; salon/clinic appointment focus |
| Store builders | Dukaan, Bikayi | Solve "sell online", not daily hisaab; funding faded |
| **Owner talks to WhatsApp, business runs** | — | **Empty.** |

Context: ~1.5 crore Indian businesses on WhatsApp Business; ~78% of SMBs use WhatsApp for
customer chats; top MSME pain = delayed payments; top digital-adoption blockers = software cost,
low tech skill, integration hassle. All three blockers are removed by "no new app".

## V1 scope — exactly seven intents
1. `record_sale` — "Ramesh 5 bag cement 1750 udhaar" → upsert customer, add line items, set
   payment mode (cash/UPI/credit), decrement stock, send invoice to customer.
2. `record_payment` — "Ramesh ne 2000 diya" → reduce balance, send receipt. UPI-link payments
   auto-recorded via gateway webhook.
3. `query_receivables` — "kitna udhaar baaki hai" → total, top debtors, ageing.
4. `remind` — "REMIND ALL" / "remind Ramesh" → utility template with UPI link, from business
   number; weekly auto-repeat until cleared.
5. `query_stock` — "stock cement" → quantity; auto low-stock alert against owner-set threshold.
6. `summary` — "aaj ka hisaab" / "is mahine ka" → sales, cash/UPI/credit split, collections,
   expenses, low stock; auto-sent nightly 21:00.
7. `record_expense` — "kharcha diesel 800".

Customer side (same number, no owner effort): invoice delivery, UPI pay link (WhatsApp Pay /
Razorpay / PhonePe in-chat), reorder by text, order status. Later: Catalogue + Flows.

V2 (only after ≥10 paying): GST invoice PDF, staff recording via team group, monthly CA PDF,
multi-branch, Tally/Excel export.

## Data model (minimal)
`business`, `user` (owner/staff, role), `customer` (name, phone, balance), `item` (name, unit,
price, stock, low_threshold), `sale` (customer, lines[], mode, total, created_by), `payment`
(customer, amount, mode, ref), `expense` (category, amount), `reminder_job`.

## Platform rules that shape the product
- Build only on the **official WhatsApp Business API** (Meta Cloud API direct, or a BSP with no
  per-message markup). Unofficial "phone emulation" libraries = ban risk; unsellable.
- **Groups**: bots in ordinary consumer groups are not supported. The official **Groups API**
  (2026) allows a verified business number to create groups of **≤8 members**, up to 10,000
  groups/number; no interactive buttons/lists, no calls. Use it for the **owner + staff back-office
  group**, not for customers. Customers get 1-to-1 messages and broadcasts.
- **Pricing** (India, 2026): utility/authentication ≈ ₹0.115/msg, marketing ≈ ₹0.863/msg, +18%
  GST; billed per delivered message since Jul 2025; **from 1 Oct 2026 service/utility messages
  inside the 24-h window are also charged** → price internally per message; cap or upsell
  marketing broadcasts.
- **In-chat payments**: WhatsApp Pay (UPI), Razorpay, PhonePe, Paytm all work inside the chat.
- **Flows** for forms (new customer, order) and **Catalogue** for browse-to-order.

## Pricing
| Tier | Price | Includes |
|---|---|---|
| Solo | ₹999/mo | 1 owner, all 7 intents, reminders + UPI links, nightly summary, ≤300 customers |
| Shop | ₹2,499/mo | + owner+4 staff group, GST PDFs, catalogue & reorder, monthly CA PDF, unlimited customers |
| Multi-shop | ₹4,999/mo | + 3 branches, branch summaries, Excel/Tally export, priority support |

Setup fee **₹499** before activation (the "₹9": filters, verifies number, fires Meta Purchase
event). COGS per Shop customer ≈ ₹400/mo (messages ₹100–250, LLM ₹100–200, hosting ₹50) →
~84% gross margin.

## Go-to-market
- **First vertical: small B2B traders/distributors** (building materials, FMCG, agri inputs,
  electrical). High udhaar → reminder ROI obvious → ₹1,500–4,000/mo tolerable.
- **Second: coaching/tuition centres** (fees, batch notices), timed Jan–Jul.
- Channel 1: click-to-WhatsApp ads (Status + Reels + Feed), objective Sales→WhatsApp,
  Advantage+ audience seeded with "wholesale / distributor / Vyapar / building materials", 3
  cities, ₹1,000/day × 14 days. Demo bot prompts "type your first sale".
- Channel 2 (free): local CAs and hardware/market associations; one CA → 40 clients.
- Metrics: cost/conversation < ₹80; conversation→₹499 > 5%; setup→month-2 retention > 60%.

## 90-day plan
Weeks 1–3 build on official API (7 intents, Hinglish + 1 regional) → weeks 3–6 five free
traders, hand-enter their top 30 customers, weekly "kitna recover hua" → week 7 one 15-s video
from a real result → weeks 7–9 ₹14k ads → weeks 9–13 convert, fix onboarding, scale 20%/few
days. Target day 90: 10–20 paying shops (₹25–50k MRR).

## Risks & mitigations
Habit drop-off (must be less effort than paper; nightly summary as reward) · Meta price changes
(per-message internal pricing; broadcasts as add-on) · Vyapar adds a WhatsApp assistant (stay
narrow, regional language, own CA/association relationships) · Trust over money data (export
from day one, clear privacy line).
