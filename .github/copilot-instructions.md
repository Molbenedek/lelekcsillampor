<!--
Guidance for AI coding agents working on this repo.
Generate concise, actionable edits and preserve site build behavior.
-->

# Copilot instructions — Lélekcsillámpor

This is a small Jekyll-based static site (GitHub Pages). The goal of these instructions is to give an AI coding agent immediate, repository-specific context so edits are safe and useful.

## Big picture
- **Static site (Jekyll):** pages contain YAML front matter (see `index.html`) and there is a `_layouts` folder with `default.html`. Treat this as a Jekyll site: pages use layouts and the SASS pipeline.
- **Assets:** styles live at `assets/css/main.scss`. It contains the YAML front matter (the `---` lines at top) so Jekyll will compile it to CSS. Do NOT remove those lines or change the path referenced in `_layouts/default.html` (`/assets/css/main.scss`).
- **Custom domain:** `CNAME` contains `lelekcsillampor.hu`. Deployment is via GitHub Pages; preserve `CNAME` when editing repository-level settings.

## Important files to reference
- `index.html` — home page content and example of page front matter (`layout: default`).
- `_layouts/default.html` — site wrapper, loads fonts and the stylesheet, contains the `{% seo %}` tag.
- `assets/css/main.scss` — primary stylesheet. Variables at the top (`$font-sans`, `$font-serif`, color hexes) control branding.
- `CNAME` — custom domain for Pages.

## Build & developer workflow (what to run locally)
- If using Bundler (recommended):
  - `bundle install; bundle exec jekyll serve --incremental --livereload`
- If Jekyll is installed globally: `jekyll serve` (or `jekyll build` to produce `_site`).
- On Windows PowerShell: separate chained commands with `;` (shown above).
- There is no `package.json` or explicit JS build step detected; edits to SCSS/HTML are handled by Jekyll's pipeline.

## Project-specific conventions & gotchas
- SCSS file is referenced directly as `/assets/css/main.scss` in the layout; keep that path and file extension so Jekyll compiles it.
- `main.scss` includes front matter (`---`) at the top — this triggers SASS processing. Do not remove it.
- The layout includes `{% seo %}` tag. This implies the site may expect the `jekyll-seo-tag` plugin or similar. If you modify SEO or head content, search for `_config.yml` to confirm plugin availability before making breaking changes.
- Fonts are loaded from Google Fonts in the layout. Change font variables in `assets/css/main.scss` rather than rewriting link tags unless you understand the typography impact.

## Typical, safe edits (examples)
- To change the headline: update `index.html` `h1` or `.tagline`.
- To adjust theme colors or typography: update variables near the top of `assets/css/main.scss` (`$font-sans`, `$font-serif`, color hex values) and re-run the local build to verify.
- To add a new page: create `about.md` or `about.html` with front matter `---
layout: default
title: About
---` and place content below.

## When to ask for human confirmation
- Adding/removing plugins in `_config.yml`, changing `CNAME`, or altering the build pipeline (adding npm, webpack, etc.).
- Removing the `---` front matter from SCSS or page files.
- Making large structural changes to `_layouts/default.html` (head, fonts, SEO) without testing locally.

## Search tips for the repo
- Look for front matter (`---`) to find Jekyll-processed files.
- Inspect `_layouts/default.html` when changing global markup/headers/footers.

## Final notes
- Keep edits minimal and localized when possible. Verify visual changes locally with `bundle exec jekyll serve` or via GitHub Pages preview after pushing.
- If anything referenced here is missing (for example `_config.yml` or a plugin), ask the repo owner before adding plugins or changing deploy behavior.

---
If you want, I can run a quick commit with this file and then run a local build check (if you confirm you have Ruby/Bundler available), or update wording based on any extra conventions you'd like included.
