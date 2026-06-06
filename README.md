# klusai-pages-brand

**Single source of truth for the `klusai-pages-*` family's brand.** A Jekyll *remote theme*
holding the shared layouts, includes, CSS tokens, fonts, and logos used by the KlusAI Pages
sites (research.klusai.com, academy.klusai.com, …). Change a colour, font, logo, or the
header/footer **here once** and every consumer site picks it up on its next build.

Mirrors the klusai.com / klusai-webos brand system v1.1.

## How a consumer site uses it

In the consumer repo's `_config.yml`:

```yaml
remote_theme: klusai/klusai-pages-brand
plugins:
  - jekyll-remote-theme
  - jekyll-feed
  - jekyll-seo-tag

# --- brand parameters (all optional; sensible defaults) ---
accent: academy            # accent ramp: research (default) | academy | klusai | coral
brand_sub: Academy         # subtitle next to the logo (omit for none)
nav:                       # header nav links (internal paths or full URLs)
  - { title: Offerings, url: /offerings/ }
  - { title: About,     url: /about/ }
nav_cta_text: klusai.com   # right-hand pill (defaults to "klusai.com" → https://klusai.com)
nav_cta_url: https://klusai.com
footer_legal: >-           # optional fine print (e.g. non-affiliation disclaimer)
  Independent training. Not affiliated with, endorsed by, or sponsored by Anthropic.
feed_in_footer: true       # show the RSS link in the footer (sites with a blog)
```

The consumer **overrides any layout** by placing a same-named file in its own `_layouts/`
(e.g. a site-specific `paper.html` or `roadmap.html` that isn't part of the shared set).

> **Visibility:** GitHub Pages' build can only fetch a **public** remote theme (no auth on the
> legacy build). This repo holds only presentation assets that are already served publicly by
> every consumer site, so it is intended to be **public**.

## What's shared here

```
_layouts/   default · home · page · post   (parameterized header/nav/footer + accent)
_includes/  cite.html · references.html     (bibliography helpers, opt-in)
assets/css/ brand.css                       (palette tokens + components; the accent ramp lives here)
assets/fonts/  Familjen Grotesk SemiBold · Inter Regular/Medium (woff2)
assets/brand/  logo-horizontal[-white].svg · icon-only.svg
```

## Accent ramps

`brand.css` defines named colour ramps (`--research-*`, `--academy-*`, `--klusai-*`, `--coral-*`)
each with `-100/-400/-500/-600/-700` stops. A consumer picks one via `accent:` and `default.html`
remaps the semantic `--accent` tokens (light + dark). Default is Research Teal.

| Property | `accent:` | Hue |
|---|---|---|
| research.klusai.com | `research` (default) | Teal `#14B8A6` |
| academy.klusai.com  | `academy` | Indigo `#6366F1` |

To add a property's accent: add a `--<name>-*` ramp to `brand.css` and set `accent: <name>`.
