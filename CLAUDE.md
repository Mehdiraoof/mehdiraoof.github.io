# CLAUDE.md — Project Brief for mehdiraoof.github.io

This file is read at the start of every Claude Code session. It holds the decisions,
style, and rules for this website so every change stays consistent. Follow it.

## What this project is

A personal CV and portfolio site for **Mehdi Raoof, Senior SEO/GEO Lead** (10 years,
4 years leading teams at Espard and byFood). Hosted free on **GitHub Pages** at
`https://mehdiraoof.github.io`.
The site should quietly demonstrate SEO best practice in its own markup, because the
owner is an SEO professional and the site is itself a work sample.

## Site structure

The site runs on **Jekyll** (GitHub Pages' native build — no custom plugins beyond
`jekyll-sitemap`, no GitHub Actions).

- **`_config.yml`** — site title/description/url, `permalink: pretty`, the
  `jekyll-sitemap` plugin, `theme: null`, and the build excludes.
- **`_layouts/default.html`** — the shared page shell: includes `head.html`, the GTM
  noscript snippet, `nav.html`, `{{ content }}`, `footer.html`, and the shared JS
  (mobile nav, scroll reveals, count-up numbers).
- **`_includes/head.html`** — meta tags, canonical (built from `page.url`, overridable
  per page), Open Graph/Twitter, fonts, the CSS link, and the GTM head script. Pages
  pass `title` and `description` (and optionally `og_description`, `twitter_description`,
  `canonical`) through front matter.
- **`_includes/gtm-body.html`** — the GTM noscript iframe.
- **`_includes/nav.html`** / **`_includes/footer.html`** — shared site chrome, pulled
  out of the old single-page homepage. Nav has hidden placeholder links for Blog and
  Tools (`hidden` attribute) — unhide them once those sections exist.
- **`assets/css/main.css`** — all site CSS (moved out of the old inline `<style>`
  block, byte-identical). Shared across every page.
- **`index.html`** — front matter (layout, title, description, etc.) plus the CV
  content: hero, impact stats, focus areas, experience timeline, skills, contact.
  Its Person JSON-LD lives directly in this file, not in `head.html`, since schema
  varies per page type (see SEO requirements below).
- **`404.html`** — same design system, links back home, excluded from the sitemap
  via `sitemap: false` in its front matter.
- **Blog (`/blog/`)** — planned. SEO articles as Markdown files in `_posts/`, rendered
  through `layout: default`.
- **Tools (`/tools/`)** — planned. Each tool as its own page/directory (e.g.
  `/tools/seo-extension/`), through `layout: default`.

Every new page's front matter must set `layout: default` — that's what wires up GTM,
nav, footer, and the shared CSS/JS automatically. Keep the homepage focused on the CV.
Blog and Tools get their own pages, with a small teaser and link to each from the
homepage.

## Design system

Warm, modern, dark. The boldness lives in only two places: the name and the big result
numbers. Everything else stays quiet so those pop. Never turn this into a generic
"dark background, one bright accent" template.

**Colors (CSS variables in `assets/css/main.css`):**
- `--bg:#0D0A08` · `--bg-2:#130E0A` · `--surface:#181109` · `--surface-2:#1F160D`
- `--text:#F7EFE4` · `--muted:#ABA096` · `--faint:#6E655C`
- `--line:rgba(255,255,255,0.07)` · `--line-warm:rgba(255,158,69,0.16)`
- Mango gradient: `linear-gradient(118deg,#FFCE45 0%,#FF9A2F 44%,#FF5E3A 100%)`
- Solid mango: `--mango-solid:#FF9A2F`
- Base background is warm near-black, never a cold blue-black. Mango is a warm color
  and a cold base fights it.

**Typography (Google Fonts):**
- Display and headings: **Bricolage Grotesque** (500 / 700 / 800)
- Body: **Inter** (400 / 500 / 600)
- Data labels, eyebrows, dates, small mono bits: **JetBrains Mono**
- The mono face is the "SEO analyst" signature. Use it for eyebrow labels, dates,
  stat captions, and source tags.

**Layout & components:**
- Max content width `1080px`, generous spacing, mobile-first responsive.
- Reusable pieces already defined: eyebrow labels, gradient text, stat cards, chips,
  the experience timeline, ghost/primary buttons, section headers. Reuse these styles
  on new pages so Home, Blog, and Tools feel like one site.
- Motion: subtle scroll reveals, count-up on numbers, soft hover lifts. Always respect
  `prefers-reduced-motion`.

## Content principles

- **No walls of text.** The owner's Word CV is dense bullets. The site does the
  opposite: curate, don't dump.
- Turn strong metrics into large scannable numbers, not buried bullet points.
- Each job = one short context line plus its 2–3 best wins as small tags.
- Skills are grouped chips, not long lists.
- Write in a warm, human, expert voice. First person is fine and welcome.
- **Approved stat:** the homepage line "over $100K a month from organic search alone"
  is approved and must stay. Other results should use relative numbers (percentages,
  before/after), not additional absolute dollar figures.

## SEO requirements (non-negotiable, this is the owner's craft)

- Semantic HTML5 landmarks, one clear `<h1>` per page, logical heading order.
- Every page: unique `<title>`, meta description, canonical URL, Open Graph + Twitter
  tags. Add a real `og:image` when one exists.
- Structured data (JSON-LD): **Person** on Home, **SoftwareApplication** for each tool,
  **BlogPosting / Article** for each blog post.
- `sitemap.xml` is generated by `jekyll-sitemap` — never hand-write or edit it directly.
  Exclude a page from it with `sitemap: false` in that page's front matter (used for
  `404.html`).
- `robots.txt` stays hand-written at the site root; keep it pointing at `/sitemap.xml`.
- Keep `llms.txt` at the site root in sync with the live site. Whenever a page is added
  or meaningfully changed, update `llms.txt` in the same commit — add, remove, or refresh
  that page's link and one-line description so it always matches what's actually published.
- Fast, lightweight, accessible: alt text on images, visible focus states, good color
  contrast, no layout shift.
- Clean, descriptive URLs (`/tools/seo-extension/`, not query strings).

## Technical setup & constraints

- **Static only, Jekyll native.** GitHub Pages builds this site with its own Jekyll +
  `github-pages` gem — no custom plugins beyond `jekyll-sitemap`, no GitHub Actions.
  `Gemfile`/`Gemfile.lock` exist only to run and test Jekyll locally
  (`bundle exec jekyll build` / `bundle exec jekyll serve`); GitHub Pages ignores them
  and builds with its own pinned gem versions.
- `theme: null` in `_config.yml` is intentional — the `github-pages` gem defaults to
  `jekyll-theme-primer` otherwise, which silently adds an unused `assets/css/style.css`
  to every build.
- **Analytics:** every page must include the Google Tag Manager snippets (container
  `GTM-MJTHWQ88`). `_layouts/default.html` already wires this up automatically (via
  `_includes/head.html` and `_includes/gtm-body.html`) for any page with
  `layout: default` — don't hand-add GTM snippets to a page that uses the layout.

## Rules and gotchas

- **Never delete or rename `google0cfa74813d6a62aa.html`.** It keeps Google Search
  Console verified. Leave it at the repo root untouched.
- Never save pages via a browser's "Save As" — it rewrites links to local file paths
  and breaks fonts. Edit source files directly.
- **Privacy:** phone number is intentionally kept **off** all public pages to avoid
  spam. Contact is email, LinkedIn, GitHub.

## Git conventions

- Small, focused commits. Clear messages in the imperative mood
  (e.g. `Add tools page with SEO extension entry`).
- Prefer surgical edits to the relevant file over regenerating whole files.
- Do not add `Co-Authored-By` (or other AI attribution) trailers to commit messages.
- Deploy is automatic: committing to `main` publishes to the live site via GitHub Pages.

## Git workflow

- Never push directly to `main`. For every change: create a branch, commit, push it,
  open a PR, merge the PR yourself, delete the branch, then pull `main` locally.
- Never wait for the owner to merge — merge it yourself as part of finishing the change.
- Exception: if a change touches `google0cfa74813d6a62aa.html`, ask the owner first
  before doing anything. Once approved, ship it through the same branch/PR/merge flow.

## Decisions log / open items

- Location tag currently shows "Istanbul" in the hero — confirm or change.
- Custom domain deferred for now; owner may buy one later (plan a clean migration then).
- Jekyll migration, sitemap.xml, and robots.txt are done. Next planned work: social
  preview image, Download CV button, the Tools page, then the Jekyll blog.
