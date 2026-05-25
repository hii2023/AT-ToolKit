# 🛠 AT ToolKit

**6 free online tools in one place — works in 15 languages, on any device.**

> No signup · No limits · No server required

🌐 **Live:** [attoolkit.com](https://attoolkit.com) *(deploy to get your URL)*

---

## Tools Included

| # | Tool | What it does |
|---|------|-------------|
| 1 | 🔲 **QR Code Generator** | Turn any URL or text into a downloadable QR code |
| 2 | 🧾 **Invoice Generator** | Fill a form → download a professional PDF invoice |
| 3 | 🖼️ **Image Compressor** | Upload image → compress with quality slider → download |
| 4 | 📝 **Word Counter** | Real-time word, character, sentence & reading time stats |
| 5 | 🔐 **Password Generator** | Cryptographically secure passwords with strength meter |
| 6 | ⚖️ **Unit Converter** | Length, weight, temperature, area, speed — all categories |

---

## Languages Supported (Auto-Detected)

English · Español · Português · Français · Deutsch · हिंदी · 日本語 · 한국어 · 中文 · Русский · Indonesia · العربية · Türkçe · Tiếng Việt · Italiano

Language is auto-detected from the browser. User can override via the dropdown.

---

## Tech Stack

| Layer | Technology | Cost |
|-------|-----------|------|
| Frontend | Pure HTML/CSS/JS (zero framework) | Free |
| QR Code | qrcode.js (CDN) | Free |
| PDF | jsPDF (CDN) | Free |
| Image compression | Canvas API (browser built-in) | Free |
| Hosting | Vercel | Free |
| Analytics | Google Analytics 4 | Free |
| Ads | Google AdSense | Free (revenue share) |

**Total infrastructure cost: ~$12/year (domain only)**

---

## Deploy in 2 Minutes

### Option 1 — Vercel (Recommended)
```bash
npm i -g vercel
vercel --prod
```

### Option 2 — Netlify
Drag the project folder to [netlify.com/drop](https://netlify.com/drop)

### Option 3 — GitHub Pages
1. Push this repo to GitHub
2. Settings → Pages → Deploy from `main` branch

---

## Project Structure

```
ATToolKit/
├── index.html          # Everything — all 6 tools, all 15 languages
├── vercel.json         # Hosting config + security headers
├── assets/             # Favicon, og-image, future assets
├── docs/               # Architecture diagrams, notes
└── README.md
```

---

## Monetization Plan

### Free Tier (Default)
- All 6 tools fully functional
- Google AdSense ads displayed

### Premium Tier (Roadmap)
- No ads
- Unlimited invoice history (saved to account)
- Bulk QR generation
- Custom invoice templates
- Priority support

**Payment:** Paddle (handles global VAT/GST automatically)

---

## Adding AdSense

Replace the two ad slot placeholders in `index.html`:
```html
<!-- Replace this: -->
<div class="ad-slot">[ Ad Space 728×90 — Google AdSense ]</div>

<!-- With your real AdSense code: -->
<ins class="adsbygoogle" ...></ins>
```

---

## Roadmap

- [ ] More tools (PDF merger, color picker, loan calculator)
- [ ] Premium accounts (Supabase Auth + Paddle)
- [ ] SEO landing pages per language (`/es/`, `/pt/`, etc.)
- [ ] PWA support (offline mode)
- [ ] API access for developers (premium)

---

## License

MIT — free to use, fork, and modify.

---

*Built with ❤️ · AT ToolKit*
