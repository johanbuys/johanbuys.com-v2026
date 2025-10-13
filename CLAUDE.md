# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Development Commands

This is an Astro blog site deployed to Cloudflare Pages. Use these commands:

- `pnpm dev` - Start development server at localhost:4321
- `pnpm build` - Build production site to ./dist/
- `pnpm preview` - Build and preview with Wrangler locally
- `pnpm deploy` - Build and deploy to Cloudflare Pages
- `pnpm cf-typegen` - Generate Cloudflare Workers types

## Architecture

This is an Astro-based blog site with content collections:

### Content Collections
- **Blog posts**: `src/content/blog/` - Markdown/MDX files with frontmatter schema (title, description, pubDate, updatedDate, heroImage)
- **Notes**: `src/content/notes/` - Markdown/MDX files with simplified schema (title, pubDate)
- Content schemas defined in `src/content.config.ts` using Zod validation

### Key Files
- `src/consts.ts` - Global site constants (SITE_TITLE, SITE_DESCRIPTION)
- `astro.config.mjs` - Astro configuration with Cloudflare adapter, MDX, and sitemap
- `wrangler.jsonc` - Cloudflare Workers configuration for deployment

### Deployment
- Site URL: https://johanbuys.com
- Platform: Cloudflare Pages with Workers adapter
- Static assets served from `public/` directory
- Build output goes to `dist/` directory

### Page Structure
- Blog posts: `/blog/[...slug].astro` (dynamic routing)
- Notes: `/notes/[...slug].astro` (dynamic routing)
- RSS feed: `/rss.xml.js`

Use pnpm as the package manager. The site uses TypeScript with strict configuration.