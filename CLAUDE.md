# mohamedmeghawry.com

## Project goal
Personal portfolio for Mohamed Meghawry. Positioning: Desktop Analyst, healthcare IT
(decided 2026-10-05, see Career/PROFILE.md POS-1). Security operations is the longer-term track.
Clean, fast, blog-first. Astro + Tailwind. Static site, deployed to Cloudflare Pages.

## Voice and style rules
- No em dashes. Use commas, semicolons, or periods.
- No years of experience phrasing. Say "background in X" not "5 years of X".
- Direct, confident prose. Short sentences. No hedging.
- Plain language, not corporate speak.

## Content priorities (top to bottom)
1. Desktop and endpoint work at LifeLabs. Generic wording only: no ticket counts, no client config detail.
2. Technical Support Engineer at The Canadian Arabic Orchestra (frame as IT; the employer is never labelled "Maple Arts"; the app's store name is Maple Arts), including the app and the WhatsApp automation
3. Writing: only real writeups. Never claim labs or experiments that do not exist yet.
4. Education: BCS, York University

Facts come from `Career/resume/src/lib/resume-data.ts`; public-safe rules from `Career/CAREER-MAP.md`.

## Stack
- Astro 6.x (static output, no SSR adapter)
- Tailwind CSS v4 via `@tailwindcss/vite` (configured in `astro.config.mjs`, imported in `src/styles/global.css` with `@import "tailwindcss";`)
- `@tailwindcss/typography` for the `prose` classes on blog posts
- MDX for blog posts (`@astrojs/mdx`)
- `@astrojs/sitemap` (emits `/sitemap-index.xml`) and `@astrojs/rss` (emits `/rss.xml`)
- Node >= 22.12.0
- Cloudflare Pages for hosting, deployed automatically on `git push`
- GitHub for source

## Project structure
- `src/pages/`: routes. `index.astro` (home), `about.astro`, `work.astro`, `writing.astro` (post list), `writing/[...slug].astro` (post detail), `404.astro`, `rss.xml.js` (feed)
- `src/layouts/Layout.astro`: shared shell with head/SEO/OG/Twitter meta, skip link, Header, Footer. Props: `title`, `description?`, `image?`, `type?`
- `src/components/`: `Header.astro` (nav: About, Work, Writing), `Footer.astro` (Email, LinkedIn; GitHub removed 2026-10-05 until it holds desktop-relevant work)
- `src/content/writing/`: blog posts (`.md` / `.mdx`)
- `src/content.config.ts`: the `writing` collection schema
- `src/styles/global.css`: Tailwind entry point
- `public/`: static assets (favicon, robots.txt, `og.png` default social preview, set in Layout.astro)

## Commands
- `npm run dev`: local dev server (localhost:4321)
- `npm run build`: static build to `./dist/`
- `npm run preview`: preview the build locally
- `npm run astro -- --help`: Astro CLI

## Adding a blog post
Create `src/content/writing/{nnn}-{slug}.mdx` with this frontmatter (schema in `src/content.config.ts`):
```yaml
---
title: "..."           # required
description: "..."      # required
pubDate: 2026-05-21     # required (YYYY-MM-DD)
updatedDate: 2026-05-22 # optional
tags: ["soc", "thm"]    # optional, defaults to []
draft: false            # optional, defaults to false; drafts are excluded from list, feed, and routes
---
```
The slug (route at `/writing/{id}`) comes from the filename. Lists, the RSS feed, and static routes all filter out `draft: true`.

## What NOT to do
- No fancy animations, parallax, or hero video
- No iOS/Android dev showcase on homepage (lives in work history only)
- No "full stack developer" framing anywhere
- No design system libraries (shadcn, MUI). Tailwind only.
