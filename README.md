# Multiplatform Kickstarter — Website

Static website for [Multiplatform Kickstarter](https://multiplatformkickstarter.com), the local AI app builder for Kotlin Multiplatform developers. Built with [Hugo](https://gohugo.io) and the `hugo-serif-theme` as a base, with full project-level layout and style overrides.

---

## Running locally

```bash
# Install Hugo extended (required for SCSS compilation)
brew install hugo          # macOS
# or: snap install hugo --channel=extended  (Linux)
# or: download from https://github.com/gohugoio/hugo/releases

# Clone and run
git clone https://github.com/your-org/website.git
cd website
hugo server -D
```

The site runs at `http://localhost:1313`.

### Requirements

- Hugo **extended** v0.55+  (extended is required for SCSS processing)
- No Node.js required

---

## Configuring Lemon Squeezy

All three checkout URLs are stored in `config.toml` under `[params]`:

```toml
# config.toml
[params]
  # Replace these with your real Lemon Squeezy checkout links
  lemon_squeezy_pro_monthly_url = "https://multiplatformkickstarter.lemonsqueezy.com/checkout/buy/REPLACE_PRO_MONTHLY"
  lemon_squeezy_pro_yearly_url  = "https://multiplatformkickstarter.lemonsqueezy.com/checkout/buy/REPLACE_PRO_YEARLY"
  lemon_squeezy_lifetime_url    = "https://multiplatformkickstarter.lemonsqueezy.com/checkout/buy/REPLACE_LIFETIME"
```

To find your checkout URL in Lemon Squeezy:
1. Go to **Lemon Squeezy → Products → [your product] → Variants**
2. Click **Share** on a variant
3. Copy the checkout URL
4. Paste it into the matching `config.toml` parameter

These URLs are injected into the homepage pricing section, the pricing page, and any CTA buttons at build time. No backend validation is performed on the website — license activation happens inside the desktop app.

### Optional: Lemon Squeezy overlay

To enable the Lemon Squeezy pop-up checkout overlay instead of navigating to a new page, add this script to `layouts/_default/baseof.html` just before `</body>`:

```html
<script src="https://app.lemonsqueezy.com/js/lemon.js" defer></script>
```

Then add `class="lemonsqueezy-button"` to any checkout link. This is already commented in the layout — uncomment when ready.

---

## Deploying

### Netlify (recommended)

1. Connect your Git repository in Netlify
2. Set build command: `hugo --minify`
3. Set publish directory: `public`
4. Set environment variable: `HUGO_VERSION=0.121.0` (or your target version)

The `content/_redirects` file is automatically copied to `public/` by Hugo.

### Cloudflare Pages

Build command: `hugo --minify`  
Output directory: `public`  
Environment variable: `HUGO_VERSION=0.121.0`

### GitHub Pages

Use the included GitHub Actions workflow (`.github/workflows/deploy.yml` — update if needed). Hugo extended must be installed:

```yaml
- name: Setup Hugo
  uses: peaceiris/actions-hugo@v2
  with:
    hugo-version: '0.121.0'
    extended: true
```

---

## Project structure

```
website/
├── config.toml                  # Site config, Lemon Squeezy URLs, menu
├── content/en/
│   ├── _index.md                # Homepage front matter
│   ├── blog/                    # Blog posts (Markdown)
│   ├── pricing/_index.md        # Pricing page front matter
│   ├── download.md              # Download / early access page
│   ├── faq/_index.md            # FAQ content
│   ├── privacy.md               # Privacy policy
│   └── terms.md                 # Terms of service
├── layouts/
│   ├── _default/
│   │   ├── baseof.html          # Base HTML template (overrides theme)
│   │   └── single.html          # Default single page
│   ├── index.html               # Homepage layout (all sections)
│   ├── blog/
│   │   ├── list.html            # Blog index
│   │   └── single.html          # Blog post
│   ├── pricing/list.html        # Pricing page
│   ├── download/single.html     # Download page
│   ├── faq/list.html            # FAQ page
│   └── partials/
│       ├── header.html          # Site header
│       └── footer.html          # Site footer
├── assets/scss/
│   └── custom.scss              # All custom CSS (dark theme, components)
└── static/
    └── images/                  # Static images and OG image
```

---

## SEO notes

- **Title**: `Multiplatform Kickstarter — Local AI App Builder for Kotlin Multiplatform`
- **Meta description**: Set globally in `config.toml` and overridden per page in front matter
- **Canonical URLs**: Added to every page via `<link rel="canonical">`
- **Open Graph**: Full OG tags on all pages
- **Twitter Cards**: `summary_large_image` card on all pages
- **JSON-LD**: `SoftwareApplication` schema on homepage; `FAQPage` schema for FAQ section; `BlogPosting` on each blog post
- **Sitemap**: Generated automatically by Hugo at `/sitemap.xml`
- **robots.txt**: Generated automatically by Hugo (`enableRobotsTXT = true` in config)
- **Blog posts**: Target keywords naturally — "AI app builder for Kotlin Multiplatform", "local AI app builder", "Compose Multiplatform app generator", "KMP project generator"

### OG image

Replace `static/images/og-image.png` with a real 1200×630 PNG. The current placeholder is an SVG. For production, generate a proper PNG that shows the product UI mockup.

---

## Future TODOs

- [ ] Replace Lemon Squeezy placeholder URLs with real checkout links
- [ ] Add real OG image PNG (1200×630)
- [ ] Add real product logo SVG to `static/images/logo/MKLogo.svg`
- [ ] Add Google Analytics ID to `config.toml` when ready
- [ ] Uncomment Lemon Squeezy overlay script in `baseof.html` when ready
- [ ] Add download links once the desktop app binary is available
- [ ] Implement sitemap prioritization for blog posts
- [ ] Add dark/light mode toggle (CSS custom properties are already in place)
- [ ] Add i18n support for additional languages (config stubs exist)
- [ ] Add structured data for blog authors
- [ ] Set up email capture or integrate with Beehiiv/Substack for newsletter
