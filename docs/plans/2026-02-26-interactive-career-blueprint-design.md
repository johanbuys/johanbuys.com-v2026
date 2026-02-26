# Interactive Career Blueprint — Design

## Summary

A dedicated `/journey` page that visualizes Johan's 20-year career as an interactive technical drawing. The timeline draws itself on scroll, with spec cards revealing details at each career phase. Native to the Blueprint design language.

## Route

`/journey` — linked from main navigation.

## Career Phases

1. **IC Engineer** (~2005–2015) — Full-stack foundations, Computer Science degree, Golden Key honor society, decade of hands-on engineering
2. **Co-Founder & CTO** (~2015–2020) — Startup chapter, built ML-powered computer vision platform for hospitality, every technical decision, COVID shutdown
3. **Engineering Manager** (~2020–present) — Cylinder Health, built team from scratch, doubled size, internship program, promoted engineers
4. **Current & Next** — Leading Member Experience squad, front-end oversight, CI/CD enablement, HIPAA-compliant AI, what's next

## Page Structure

### Header
- Blueprint section label: "SPEC-JOURNEY-001"
- Title: monospace heading
- Subtitle: "A technical drawing of 20 years in engineering."

### Timeline (Desktop)
- Horizontal SVG line that draws itself via `stroke-dashoffset` tied to scroll
- Crosshair markers at each career node (matching existing site crosshairs)
- Dimension annotations between nodes showing year ranges
- Spec cards alternate above/below the timeline (zigzag), connected by leader lines

### Timeline (Mobile)
- Vertical line on the left edge
- Cards stack full-width below each node
- Same scroll-draw animation, vertical orientation

### Spec Cards (per phase)
- Existing `spec-card` styling: `corner-fold`, `pin`, `card-grid-overlay`
- SPEC label (e.g., "SPEC-IC-001")
- Role title + company
- 2-3 sentence description
- Tech stack row using `tech-item` pills
- Key metric in `spec-number` style

### Footer Node
- "What's Next" — forward-looking statement
- Links to About page and LinkedIn

## Animations

- **Line drawing:** CSS `stroke-dashoffset` animated via IntersectionObserver or scroll listener
- **Node reveal:** Crosshairs fade in with pulse when their section enters viewport
- **Card reveal:** Existing `.reveal` pattern — fade-in-up when visible
- **No JS frameworks** — vanilla IntersectionObserver + CSS, consistent with existing patterns

## Technical Approach

- Single Astro page: `src/pages/journey.astro`
- SVG timeline rendered inline
- Career data hardcoded in the template (not a content collection — it's a single curated page)
- Reuses all existing CSS classes from `global.css` (spec-card, crosshair, dimension-line, pin, etc.)
- Small inline `<script>` for scroll-driven line animation and IntersectionObserver
- `prefers-reduced-motion` respected — shows completed timeline without animation

## Navigation

- Add "Journey" link to Header nav between "About" and the end
