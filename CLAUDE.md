# CLAUDE.md — Project Brief for mehdiraoof.github.io

This file is read at the start of every Claude Code session. It holds the decisions,
style, and rules for this website so every change stays consistent. Follow it.

## What this project is

A personal CV and portfolio site for **Mehdi Raoof, Senior SEO Specialist** (8 years,
3 leading teams). Hosted free on **GitHub Pages** at `https://mehdiraoof.github.io`.
The site should quietly demonstrate SEO best practice in its own markup, because the
owner is an SEO professional and the site is itself a work sample.

## Site structure

- **Home (`index.html`)** — the CV: hero, impact stats, focus areas, experience
  timeline, skills, contact. This exists and is live.
- **Blog (`/blog/`)** — planned. SEO articles published regularly. Will move to
  **Jekyll** so posts are simple Markdown files in `_posts/`, not hand-coded pages.
- **Tools (`/tools/`)** — planned. A page for tools the owner has built (e.g. an SEO
  Chrome extension). Each tool is treated as its own mini landing page that can rank
  and attract users on its own, not just a portfolio screenshot.

Keep the homepage focused on the CV. Blog and Tools get their own pages, with a small
teaser and link to each from the homepage.

## Design system

Warm, modern, dark. The boldness lives in only two places: the name and the big result
numbers. Everything else stays quiet so those pop. Never turn this into a generic
"dark background, one bright accent" template.

**Colors (CSS variables already in `index.html`):**
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

## SEO requirements (non-negotiable, this is the owner's craft)

- Semantic HTML5 landmarks, one clear `<h1>` per page, logical heading order.
- Every page: unique `<title>`, meta description, canonical URL, Open Graph + Twitter
  tags. Add a real `og:image` when one exists.
- Structured data (JSON-LD): **Person** on Home, **SoftwareApplication** for each tool,
  **BlogPosting / Article** for each blog post.
- Maintain `sitemap.xml` and `robots.txt` at the site root. Add new pages to the sitemap.
- Fast, lightweight, accessible: alt text on images, visible focus states, good color
  contrast, no layout shift.
- Clean, descriptive URLs (`/tools/seo-extension/`, not query strings).

## Technical setup & constraints

- **Static only.** GitHub Pages serves static files. No server-side code or databases.
- Home is currently a single self-contained `index.html` (inline CSS/JS, fonts via
  Google Fonts `<link>`, inline SVG favicon). Keep it self-contained until the site
  moves to Jekyll.
- When the blog arrives, introduce **Jekyll** with shared layouts/includes so style
  stays in one place across Home, Blog, and Tools.

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
- Deploy is automatic: committing to `main` publishes to the live site via GitHub Pages.

## Decisions log / open items

- Location tag currently shows "Istanbul" in the hero — confirm or change.
- Custom domain deferred for now; owner may buy one later (plan a clean migration then).
- Next planned work: sitemap.xml + robots.txt, social preview image, Download CV button,
  Tools page, then the Jekyll blog.
