# Splynk — Landing Site

Static landing page for Splynk. Single HTML file, no build step, no dependencies. Drop it anywhere that serves static files.

## Structure

```
splynk-site/
├── index.html              ← the site
├── robots.txt              ← crawler directives
├── sitemap.xml             ← search engine index map
├── site.webmanifest        ← PWA manifest
├── README.md
└── assets/
    ├── favicon.ico         ← multi-resolution (16/32/48)
    ├── favicon-16.png
    ├── favicon-32.png
    ├── favicon-48.png
    ├── apple-touch-icon.png  ← 180×180 for iOS home screen
    ├── icon-192.png        ← PWA
    ├── icon-512.png        ← PWA / Google logo schema
    ├── og-image.png        ← 1200×630 social share preview
    ├── og-image.jpg        ← JPEG fallback
    └── screens/            ← in-app screenshots used in showcase
```

## Deploy

**GitHub Pages**
1. Push the folder to a repo.
2. Settings → Pages → Source: `main`, folder: `/ (root)`.
3. Live at `https://<username>.github.io/<repo>/`.

**Vercel / Netlify / Cloudflare Pages**
Connect the repo, accept defaults. No build command, no output directory needed.

## ⚠️ Before going live — update the canonical URL

Every meta tag, OG tag, schema entry, sitemap entry, and robots.txt sitemap line references `https://splynk.app/` as a placeholder. **Replace all instances with your actual domain** once you've registered it.

A fast find-and-replace across the three files (`index.html`, `robots.txt`, `sitemap.xml`):

```bash
# macOS
find . -type f \( -name "*.html" -o -name "*.xml" -o -name "*.txt" \) -exec sed -i '' 's|https://splynk.app|https://yourdomain.com|g' {} +

# Linux
find . -type f \( -name "*.html" -o -name "*.xml" -o -name "*.txt" \) -exec sed -i 's|https://splynk.app|https://yourdomain.com|g' {} +
```

## SEO checklist — what's included

- Keyword-rich `<title>` and meta description optimized for "pickup games near me", "fitness classes", "sports leagues" search intent
- Comprehensive `<meta keywords>` covering 200+ relevant terms (sport types, formats, intents, demographics, locations)
- Canonical URL declared
- Open Graph tags for iMessage / Slack / Discord / Facebook / LinkedIn previews
- Twitter / X large image card
- 1200×630 OG share image featuring the Splynk logo and tagline
- Multi-resolution favicon set (16, 32, 48, 180, 192, 512)
- PWA manifest for "Add to Home Screen" on mobile
- Robots.txt with crawler directives
- XML sitemap with image metadata
- JSON-LD structured data: `Organization`, `MobileApplication`, `WebSite`
- Strong descriptive alt text on every image
- Semantic HTML5 (single `<h1>`, proper section structure)
- Mobile responsive, fast load, no JS framework
- Respects `prefers-reduced-motion`

## What's intentional in the design

- **Ambient breathing background** — four blurred color blobs (blue / orange / violet / amber) drift and pulse on independent timing loops (~9–14s per breath, ~22–34s per drift).
- **Hero cursor glow** — soft radial gradient follows your cursor with eased lerp.
- **Haptic feedback** — every button and link triggers `navigator.vibrate()`. Primary CTAs use a stronger double-pulse pattern. Silent no-op on devices without support.
- **Visibility-aware** — marquee and ambient blobs pause when the tab is backgrounded.
- **Paper grain overlay** — subtle SVG noise filter for the editorial feel.

## About the screenshots

The app screenshots are not the main visual driver. Phones appear in exactly one section ("A single place. Three formats.") arranged as a cascading editorial composition. Every other section is design-only — typography, color, rhythm.

## Edit copy

All text lives in `index.html`. Search the file for the section you want to change — sections are marked with comment blocks (`<!-- HERO -->`, `<!-- SHOWCASE -->`, etc).

## Customize colors

All colors are CSS variables at the top of the `<style>` block in `index.html`:

```css
--paper:  #F4F1EA;   /* background */
--ink:    #161516;   /* primary text */
--blue:   #1B4FFF;   /* primary accent */
--orange: #FF5B2E;   /* secondary accent */
--violet: #9B5BFF;   /* third ambient color */
--amber:  #FFB45B;   /* fourth ambient color */
```

Change those six and the whole site re-themes — including the ambient breathing background.

## Regenerating the OG image / favicons

If you update branding or want different copy on the share preview, the generation script lives at `assets/build_assets.py` (not included in this drop — happy to add it back if needed). Right now the OG image is pre-rendered at `assets/og-image.png` (and `.jpg`).

## What's intentionally left for later

- App Store / Play Store badges — add them when the app is live in the App Store
- Email capture endpoint — the "Get on the list" button is a `#` placeholder. Wire it to Mailchimp, ConvertKit, or Formspree.
- Analytics — drop Plausible, Fathom, or GA snippet into the `<head>`.
- Production OG image with proper Fraunces typography — current version uses DejaVu Serif. Once you have access to render Fraunces, swap in a typographically-tighter version.
