---
name: project-website-rebuild-2025
description: Full rebuild of multiplatformkickstarter.com Hugo website to new AI app builder positioning
metadata:
  type: project
---

Completed full website rebuild for Multiplatform Kickstarter pivot from KMP templates to local AI app builder.

**Why:** Product pivot — from selling KMP templates to a desktop AI app builder that generates full KMP projects using local LLMs (Ollama). New positioning: "Build Kotlin Multiplatform apps from prompts — locally."

**How to apply:** When working on this website, the source of truth is all in project-level layout overrides (layouts/) and content/en/. The theme (hugo-serif-theme) is left largely untouched — all new design lives in assets/scss/custom.scss and project layouts/.

## What was built

- `config.toml` — fully rewritten with new title, menu, Lemon Squeezy URL params, Inter font, purple brand color
- `assets/scss/custom.scss` — ~500 lines of new dark-theme design system (CSS custom properties, all page components)
- `layouts/index.html` — full homepage (hero + product mockup, problem section, comparison, how it works, local-first, feature grid, use cases, pricing preview, FAQ accordion)
- `layouts/pricing/list.html` — pricing page with comparison table and monthly/yearly toggle
- `layouts/download/single.html` + `list.html` — download / early access page
- `layouts/blog/list.html` + `single.html` — blog index and post templates
- `layouts/faq/list.html` — FAQ page
- `layouts/_default/single.html` + `baseof.html` — default page and base HTML (with custom.scss injection)
- `layouts/partials/header.html` + `footer.html` — new semantic nav/footer
- `content/en/blog/` — 3 SEO blog posts written
- `content/en/download.md`, `terms.md`, `faq/_index.md` — new content pages
- `static/images/og-image.svg` — OG image placeholder SVG
- `README.md` — complete developer docs

## Lemon Squeezy URLs
Configured as Hugo params in config.toml — NOT hardcoded in templates:
- `lemon_squeezy_pro_monthly_url`
- `lemon_squeezy_pro_yearly_url`  
- `lemon_squeezy_lifetime_url`

## Build status
Hugo builds cleanly (49 pages, 0 errors) with `hugo --minify`.
