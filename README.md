# Swim Montréal — Modernised Website
### Institut de Natation de Montréal (MIS)

A complete modern rebuild of [swim-montreal.com](https://swim-montreal.com) — 11 fully self-contained HTML pages, consistent design system, animated water backgrounds, live search, interactive features, SEO-optimised, and a chatbot UI throughout.

---

## Pages

| File | Page | Description |
|------|------|-------------|
| `index.html` | Homepage | Hero with animated water canvas, programs overview, reviews, locations, jobs divider |
| `jobs.html` | Jobs & Careers | Full instructor recruitment — perks, MISway method, testimonials, apply steps |
| `programs.html` | Programs | All 6 programs with sticky nav pills, terms table, MISway method, FAQ |
| `about.html` | About MIS | Story, what makes us different, evolution timeline, values, reviews |
| `meet-the-team.html` | Meet the Team | 16 real instructor cards with live search + filter by specialty |
| `contact.html` | Contact & Locations | Contact form, 18 clickable Google Maps location cards with cursor glow effect |
| `faq.html` | FAQ | 12 real FAQs with live search, category tabs, accordion |
| `policies.html` | Policies | House rules, cancellation, payment, pool-specific rules — sticky sidebar TOC |
| `news.html` | Latest News | 9 real blog posts with category filter chips and newsletter signup |
| `lifeguard.html` | Private Lifeguard | Full-height hero, what we do, timeline, MIS advantage stats, booking steps |
| `privacy-policy.html` | Privacy Policy | Full legal policy — sticky TOC, 9 sections, last updated Sept 2023 |

## SEO & Technical Files

| File | Purpose |
|------|---------|
| `sitemap.xml` | All 11 pages with priority weights for Google indexing |
| `robots.txt` | Allows all crawlers, points to sitemap |

---

## Design System

| Token | Value | Use |
|-------|-------|-----|
| `--navy` | `#0a1628` | Primary background, nav |
| `--ocean` | `#0066cc` | Links, accents |
| `--aqua` | `#00b4d8` | Hero highlights, CTAs |
| `--gold` | `#e8a020` | Jobs, lifeguard, alerts |
| `--sand` | `#f8f4ef` | Section alternates |
| `--foam` | `#caf0f8` | Light accents |

**Fonts:** Playfair Display (headings) · DM Sans (body)  
**Animations:** Canvas water simulation on every hero · Fade-up entrance animations

---

## SEO — What's Included

Every page has:
- Unique keyword-rich `<title>` tag
- `<meta name="description">` (120–160 chars)
- `<link rel="canonical">` pointing to the live domain
- Full Open Graph tags (`og:title`, `og:description`, `og:image`, `og:url`)
- Twitter/X card (`summary_large_image`)
- JSON-LD structured data per page type (LocalBusiness, FAQPage, Course, Service etc.)
- Single H1 per page
- `lang="en"` on `<html>`
- `sitemap.xml` + `robots.txt`

---

## Features

- **Animated water canvas** — bubbles, light rays, layered waves on every hero
- **Live search** — meet-the-team and FAQ filter in real time as you type
- **Category filters** — instructors by specialty, news by topic, FAQs by category
- **Cursor-following glow** — location cards on contact.html track your mouse
- **Clickable location cards** — all 18 pool locations link to Google Maps
- **AI Chatbot UI** — present on every page, routes to `/api/chat` proxy endpoint
- **Contact form** — name, email, phone, topic, message with success state
- **Newsletter signup** — on news.html with success confirmation
- **Sticky navs** — policy sidebar TOC, programs journey pills, FAQ category tabs
- **Mobile hamburger menu** — all pages responsive with collapsible nav
- **Consistent footer** — all 10 other pages linked from every footer

---

## Deployment

### Netlify via GitHub (auto-deploy)
1. Connect this GitHub repo to Netlify
2. Auto-deploys on every push to `main`
3. No build settings needed — pure static HTML

### Netlify (drag & drop)
1. Go to [netlify.com](https://netlify.com)
2. **Add new site → Deploy manually**
3. Drag and drop the folder containing all files

---

## Chatbot Setup

The chatbot UI is on every page and routes to `/api/chat`. Enable it with a serverless proxy.

**Netlify Function** (`netlify/functions/chat.js`):
```js
const Anthropic = require('@anthropic-ai/sdk');
exports.handler = async (event) => {
  const { messages, system } = JSON.parse(event.body);
  const client = new Anthropic({ apiKey: process.env.ANTHROPIC_API_KEY });
  const response = await client.messages.create({
    model: 'claude-sonnet-4-20250514',
    max_tokens: 500,
    system,
    messages,
  });
  return {
    statusCode: 200,
    body: JSON.stringify({ reply: response.content[0].text }),
  };
};
```

Add to `netlify.toml`:
```toml
[[redirects]]
  from = "/api/chat"
  to = "/.netlify/functions/chat"
  status = 200
```

Set `ANTHROPIC_API_KEY` in your Netlify dashboard environment variables.

---

## About MIS

**Institut de Natation de Montréal Inc.**  
Québec's #1 swim school — 25+ pool locations across Montréal.

- **Email:** info@swim-montreal.com
- **Phone:** (514) 294-8259
- **Facebook:** [@SwimMontreal](https://www.facebook.com/SwimMontreal)
- **Instagram:** [@swimmontreal](https://www.instagram.com/swimmontreal/)
- **Register:** [appus.sportimea.com/portal/swim-montreal](https://appus.sportimea.com/portal/swim-montreal)

---

© 2026 Institut de Natation de Montréal Inc. All rights reserved.
