# 11ty Starter Template

Minimal [Eleventy (11ty)](https://www.11ty.dev/) starter for marketing sites, optimized for AWS Amplify deployment.

## Features

- ⚡ **Fast** — 11ty generates static HTML, served via CDN
- 🎨 **Simple CSS** — CSS custom properties for easy theming, no build step
- 📱 **Responsive** — Mobile-first, works on all devices
- 🚀 **Amplify-ready** — Pre-configured `amplify.yml` for instant deployment
- 🔄 **PR Previews** — Automatic preview URLs for every pull request

## Quick Start

### Local Development

```bash
# Install dependencies
npm install

# Start dev server (http://localhost:8080)
npm run dev

# Build for production
npm run build
```

### Deploy to AWS Amplify

1. Push this repo to GitHub
2. Go to [AWS Amplify Console](https://console.aws.amazon.com/amplify/)
3. Click "New app" → "Host web app"
4. Connect your GitHub repo
5. Amplify auto-detects the `amplify.yml` — accept defaults
6. Deploy!

## Project Structure

```
├── src/
│   ├── _data/
│   │   └── site.json      # Site-wide data (name, description, etc.)
│   ├── _includes/
│   │   └── layouts/
│   │       └── base.njk   # Base HTML template
│   ├── assets/
│   │   └── css/
│   │       └── style.css  # Styles (customize colors in :root)
│   ├── pages/
│   │   ├── about.njk
│   │   └── contact.njk
│   └── index.njk          # Homepage
├── .eleventy.js           # 11ty configuration
├── amplify.yml            # AWS Amplify build settings
└── package.json
```

## Customization

### Site Info

Edit `src/_data/site.json`:

```json
{
  "name": "Your Site Name",
  "description": "Your site description",
  "url": "https://yourdomain.com"
}
```

### Colors

Edit the CSS variables in `src/assets/css/style.css`:

```css
:root {
  --color-primary: #2563eb;    /* Main brand color */
  --color-text: #1f2937;       /* Body text */
  /* ... */
}
```

### Adding Pages

Create a new `.njk` file in `src/pages/`:

```njk
---
layout: base.njk
title: New Page
permalink: /new-page/
---

<section class="page-content">
  <h1>New Page</h1>
  <p>Your content here.</p>
</section>
```

## SEO Guidelines

This template includes comprehensive SEO guidelines at [`docs/SEO-GUIDELINES.md`](docs/SEO-GUIDELINES.md).

**Key requirements for every page:**
- 1000+ words of unique content
- Primary keyword in title, H1, URL, and first 100 words
- Minimum 3 external links to high-authority sites
- FAQ section with 5+ Q&As (with schema markup)
- Embedded Google Map in footer

See the full guidelines for checklists, schema templates, and URL structure patterns.

## Custom Domain Setup

1. In Amplify Console, go to "Domain management"
2. Add your domain
3. Amplify gives you DNS records to add in Namecheap:
   - CNAME for `www` → Amplify URL
   - ANAME/ALIAS for root → Amplify URL (or use redirect)
4. SSL certificate is auto-provisioned

## License

MIT
