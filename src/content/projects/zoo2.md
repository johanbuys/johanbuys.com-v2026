---
title: "The Zoo 2: No more bars!"
description: "A showcase project demonstrating the new projects collection feature with all available schema fields."
pubDate: 2025-10-13
tags: ["Web Development", "Astro", "TypeScript"]
techStack: ["Astro", "TypeScript", "Cloudflare Pages", "pnpm"]
url: "https://github.com/example/project"
heroImage: "../../assets/blog-placeholder-3.jpg"
---

## Overview

This is an example project that demonstrates all the features of the new projects content collection. You can use this as a template for your own project entries.

## Key Features

- Full schema support including tags, tech stack, and external links
- Optional hero images for visual appeal
- Featured flag to highlight important projects
- Rich markdown content support

## Implementation Details

The project includes:

1. **Content Schema** - Defined in `src/content.config.ts`
2. **Listing Page** - Shows all projects with featured ones at the top
3. **Detail Pages** - Full project information with tech stack and tags
4. **Responsive Design** - Works great on all screen sizes

## Tech Stack

This project uses modern web technologies:

- Astro for static site generation
- TypeScript for type safety
- Cloudflare Pages for hosting
- Zod for schema validation

## Next Steps

Replace this example with your own projects! Simply create new markdown files in `src/content/projects/` with the following frontmatter:

```yaml
---
title: "Your Project Title"
description: "A brief description of your project"
pubDate: 2025-10-13
featured: false
tags: ["tag1", "tag2"]
techStack: ["tech1", "tech2"]
url: "https://example.com" # optional
heroImage: ./path-to-image.jpg # optional
---
```
