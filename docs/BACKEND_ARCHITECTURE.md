# Backend Architecture — AT ToolKit

## Current State: 100% Client-Side

Every tool runs entirely in the user's browser. No server, no database, no API calls.

```
User Browser
└── index.html
    ├── QR Code      → qrcode.js (CDN library)
    ├── Invoice      → jsPDF (CDN library)
    ├── Compressor   → Canvas API (browser built-in)
    ├── Word Counter → Pure JavaScript
    ├── Password     → window.crypto (browser built-in)
    └── Unit Convert → Pure JavaScript
```

---

## Backend Services Needed Per Feature

### 1. Analytics (Add Day 1 — Free)
**What:** Know which tool is most used, which countries visit, bounce rate.
**Service:** Google Analytics 4
**How:** Paste one `<script>` tag. No server needed.
**Cost:** Free

### 2. Ad Revenue (Add After AdSense Approval — Free)
**What:** Display ads, earn per 1000 impressions.
**Service:** Google AdSense
**How:** Paste `<ins>` tag into HTML.
**Cost:** Free. They pay YOU.
**Revenue:** $1–$5 RPM to start, $15–$30 RPM at scale (Mediavine)

### 3. Email Capture for Launch/Premium (Add Week 2)
**What:** Collect emails for premium waitlist, product updates.
**Service:** Brevo (formerly Sendinblue) — free up to 300 emails/day
**How:** Embed their form or call their API via a serverless function.
**Cost:** Free up to 300/day. $25/month for 20k subscribers.

### 4. Premium Payments (Add Month 2)
**What:** Accept subscriptions for premium tier.
**Service:** Paddle (recommended) or LemonSqueezy
**Why Paddle:** They are the Merchant of Record — they handle VAT/GST in 180+ countries. You don't register as a business in each country.
**Integration:**
```
User clicks "Go Premium"
  → Paddle checkout opens (hosted by Paddle)
  → Payment processed by Paddle
  → Paddle sends webhook to your endpoint
  → Your serverless function activates premium in Supabase
  → User gets premium features
```
**Cost:** 5% + 50¢ per transaction. No monthly fee.

### 5. User Accounts — Premium only (Add Month 2)
**What:** Store user data, invoice history, premium status.
**Service:** Supabase (open-source Firebase alternative)
**Free tier:** 500MB database, 50k MAU, 1GB file storage
**What you store:**
```
users table:
  - id, email, created_at
  - is_premium (boolean)
  - premium_expires_at (date)
  - paddle_customer_id

invoices table (premium only):
  - id, user_id, invoice_data (JSON), created_at

qr_history table (premium only):
  - id, user_id, url, created_at
```
**Cost:** Free up to 500MB. $25/month after.

### 6. Serverless Functions (Add with Premium)
**What:** Handle Paddle webhooks, activate premium, send emails.
**Service:** Vercel Edge Functions (same place you host the site)
**Endpoints needed:**
```
POST /api/paddle-webhook   → activate premium on payment
POST /api/contact          → contact form emails
GET  /api/user-status      → check if user is premium
```
**Cost:** Free up to 1M invocations/month on Vercel.

### 7. Geolocation (Optional Enhancement)
**What:** More accurate country detection than browser language.
**Service:** Cloudflare (free) — adds CF-IPCountry header automatically
**How:** Put site behind Cloudflare CDN (also gives you DDoS protection + faster loads).
**Cost:** Free

### 8. Error Monitoring (Add at Launch)
**What:** Know when something breaks in production.
**Service:** Sentry (free up to 5k errors/month)
**How:** One `<script>` tag.
**Cost:** Free tier sufficient for early stage.

---

## Full Architecture at Scale

```
                    ┌──────────────┐
                    │  Cloudflare  │  ← CDN, DDoS, IP geolocation
                    └──────┬───────┘
                           │
                    ┌──────▼───────┐
                    │    Vercel    │  ← Hosting + Edge Functions
                    └──────┬───────┘
                           │
               ┌───────────▼───────────┐
               │      index.html       │  ← All 6 tools (client-side)
               └───────────────────────┘
                           │
        ┌──────────────────┼──────────────────┐
        │                  │                  │
┌───────▼──────┐  ┌────────▼───────┐  ┌──────▼──────┐
│  Google      │  │   Supabase     │  │   Paddle    │
│  Analytics   │  │  (Auth + DB)   │  │  (Payments) │
│  + AdSense   │  │                │  │             │
└──────────────┘  └────────────────┘  └─────────────┘
```

---

## Cost Summary at Scale

| Users/month | Monthly Cost | Monthly Ad Revenue (est.) |
|------------|-------------|--------------------------|
| 1,000 | $0 | $2–$10 |
| 10,000 | $0 | $50–$150 |
| 50,000 | $0 | $250–$750 |
| 100,000 | $25 (Supabase) | $1,000–$3,000 |
| 500,000 | $50 (Supabase + extras) | $5,000–$15,000 |

*All tools are client-side = zero compute cost no matter how many users*

---

## What You Need RIGHT NOW to Launch

1. `index.html` ← already built ✅
2. GitHub repo ← doing this now ✅
3. Vercel account (free) — connect GitHub repo → live in 2 min
4. Domain (~$12/year)
5. Google Analytics account (free) — add tracking ID
6. Apply for Google AdSense (takes 2–4 weeks to approve)

**That's it. Tools work for millions of users with zero backend.**
