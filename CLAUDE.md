# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project overview

Static HTML website for AlexNes (Alexander Nesterenko), a Russian-language addiction therapist based in Germany. Deployed on Vercel. No build system, no npm, no bundler — pure HTML/CSS/JS.

**Live site:** https://alexnes.com  
**Contact:** WhatsApp +49 162 602 7760, Telegram @nesterealex

## No build commands

There is no build step. Edit HTML files directly and push. Vercel deploys automatically on merge to main.

`vercel.json` configures: cleanUrls (no `.html` in URLs), trailingSlash off, legacy redirects from `/blog/article-N` slugs, and security headers.

## File structure

- `/` — root pages: `index.html`, `about.html`, `blog.html`, `reviews.html`, `video.html`, `voprosy.html`, service pages (`terapiya-travmy.html`, `trezvost.html`, etc.)
- `/blog/` — individual article HTML files (~35 articles)
- `/testy/` — psychological test pages
- `/images/` — photos and avatars
- `sitemap.xml` — must be updated manually when adding pages

## Adding a new blog article

Each blog article is a self-contained HTML file in `/blog/`. Copy an existing article (e.g. `blog/prokrastinaciya.html`) and update:

1. **`<head>`**: `<title>`, `<meta name="description">`, `<link rel="canonical">`, OG tags, Twitter Card tags, JSON-LD schema (`headline`, `description`, `url`, `articleSection`, `datePublished`, `dateModified`)
2. **Breadcrumb `<li>`** (last item): article title in `aria-current="page"` span
3. **`article-header`**: `<span class="article-tag">` (category) and `<h1>`
4. **`article-content`**: the article body
5. **Related articles**: 2 `<a class="related-card">` links to thematically related articles

After creating the article file:
- Add a `<article class="blog-card">` entry to **`blog.html`** (prepend to the grid — newest first), with `data-tag` attribute matching the category
- Add a `<url>` entry to **`sitemap.xml`**

## Theming system

Two themes stored in `localStorage` key `theme`: `"neon"` (default, dark purple + violet accent `#8B5CF6`) and `"classic"` (monochrome). CSS uses `[data-theme="neon"]` and `[data-theme="classic"]` attribute selectors on `<html>`. All CSS is inline inside `<style>` tags — there are no external stylesheet files.

Key CSS variables:
```css
--accent-primary  /* white in classic, #8B5CF6 in neon */
--glow-color      /* used for neon box-shadows */
--btn-radius      /* 0 in classic, 50px in neon */
```

## Article content style

All content is in Russian. Writing style: direct, therapeutic, first-person therapist voice. No academic jargon. Paragraphs are long, no punctuation for comma-less lists. Uses `<h2>` for main sections, `<h3>` for subsections, `<strong>` for emphasis, `<div class="highlight-block">` for key quotes/takeaways.

## Article categories

`Самооценка`, `Зависимость`, `Отношения`, `Созависимость`, `Психология`, `Реабилитация`, `Родителям`, `Выздоровление`, `Доверие`, `Осознанность`

## Analytics (present in every page)

- Google Analytics: `G-D9MGJNMBVG` + Google Ads `AW-18060459277`
- Microsoft Clarity: `vyoxcpmq95`
