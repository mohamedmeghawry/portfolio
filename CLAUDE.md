# mohamedmeghawry.com

## Project goal
Personal portfolio for Mohamed Meghawry, positioning for SOC Tier 1 Analyst roles.
Clean, fast, blog-first. Astro + Tailwind. Static site, deployed to Cloudflare Pages.

## Voice and style rules
- No em dashes. Use commas, semicolons, or periods.
- No years of experience phrasing. Say "background in X" not "5 years of X".
- Direct, confident prose. Short sentences. No hedging.
- Plain language, not corporate speak.

## Content priorities (top to bottom)
1. IT/Operations Coordinator work at Maple Arts (frame as IT, not arts)
2. Lab writeups (TryHackMe, HackTheBox, home SOC experiments)
3. WhatsApp automation system (security-adjacent automation engineering angle)
4. Education: BCS, York University

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
- `src/components/`: `Header.astro` (nav: About, Work, Writing), `Footer.astro` (Email, LinkedIn, GitHub)
- `src/content/writing/`: blog posts (`.md` / `.mdx`)
- `src/content.config.ts`: the `writing` collection schema
- `src/styles/global.css`: Tailwind entry point
- `public/`: static assets (favicon, robots.txt)

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
