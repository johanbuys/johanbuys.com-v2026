# Interactive Career Blueprint — Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Build an interactive `/journey` page that visualizes Johan's 20-year career as a scroll-animated blueprint schematic with spec cards at each career milestone.

**Architecture:** Single Astro page (`src/pages/journey.astro`) with inline SVG timeline, hardcoded career data, CSS animations driven by a scroll listener, and IntersectionObserver for card reveals. Reuses all existing Blueprint design system classes from `global.css`. Desktop shows horizontal zigzag layout; mobile collapses to vertical.

**Tech Stack:** Astro page, inline SVG, CSS `stroke-dashoffset` animation, vanilla JS scroll listener + IntersectionObserver.

---

### Task 1: Add "Journey" to navigation

**Files:**
- Modify: `src/components/Header.astro` — add Journey link in both desktop and mobile nav

**Step 1: Add the nav link**

In `src/components/Header.astro`, find the desktop `nav-links` div and add a Journey link after Projects and before About:

```html
<HeaderLink href="/projects">Projects</HeaderLink>
<HeaderLink href="/journey">Journey</HeaderLink>
<HeaderLink href="/about">About</HeaderLink>
```

Do the same in the mobile `mobile-menu-inner` div — add Journey between Projects and About.

**Step 2: Verify the build**

Run: `pnpm build`
Expected: Build succeeds (the /journey route doesn't exist yet, that's fine — HeaderLink just renders an `<a>` tag)

**Step 3: Commit**

```bash
git add src/components/Header.astro
git commit -m "feat: add Journey link to navigation"
```

---

### Task 2: Create the journey page with header and static structure

**Files:**
- Create: `src/pages/journey.astro`

**Step 1: Create the page scaffold**

Create `src/pages/journey.astro` with:
- Astro frontmatter importing BaseHead, Header, Footer, and consts
- Full HTML document structure
- Page header with section-label ("SPEC-JOURNEY-001"), h1, subtitle
- Four empty `<section>` elements with IDs for each career phase: `phase-ic`, `phase-cto`, `phase-em`, `phase-current`
- The overall `<main>` should use `max-width: 1152px` matching the homepage

Use the same page-header pattern from the blog/projects listing pages:

```html
<div class="page-header">
  <div class="section-label">
    <span class="section-label-text">SPEC-JOURNEY-001</span>
  </div>
  <h1>The Blueprint</h1>
  <p>A technical drawing of 20 years in engineering.</p>
</div>
```

**Step 2: Verify**

Run: `pnpm build`
Expected: Build succeeds, `/journey/index.html` appears in output

**Step 3: Commit**

```bash
git add src/pages/journey.astro
git commit -m "feat: scaffold journey page with header"
```

---

### Task 3: Build the desktop timeline SVG and phase layout

**Files:**
- Modify: `src/pages/journey.astro`

**Step 1: Add the timeline container and SVG**

Below the page-header, add a `timeline-container` div that holds:

1. An SVG element (class `timeline-svg`) positioned absolutely, spanning the full width. It contains a single `<path>` element (class `timeline-path`) that will be the horizontal line. The path should be a straight horizontal line at `y=50%` of the container.

2. Four **phase sections** arranged in a CSS grid. Each phase section contains:
   - A **crosshair node** (reuse `.crosshair` and `.crosshair-circle` from global.css)
   - A **dimension annotation** between nodes showing the year range (reuse `.dimension-line` pattern)
   - A **spec card** (reuse `.spec-card`, `.corner-fold`, `.pin`, `.card-grid-overlay` from global.css)

Desktop layout: Use CSS grid with the timeline line running horizontally through the middle. Cards alternate above/below (odd phases above, even phases below) using grid row placement.

The spec card for each phase should contain:
- `card-seq` label (e.g., "SPEC-IC-001")
- Role title as `<h3>` in mono font
- Company/context line
- Description paragraph in serif
- Tech stack pills using `tech-item` class
- A key stat using `spec-number` class

**Career data to hardcode:**

Phase 1 — IC Engineer:
- Years: 2005–2015
- Title: "Full-Stack Engineer"
- Context: "Building foundations across the entire stack"
- Description: "Nearly a decade honing craft from databases to frontend. Computer Science degree, Golden Key International Honor Society. Driven by curiosity and a love for building things that work."
- Tech: ["JavaScript", "Python", "SQL", "Linux", "Full-Stack"]
- Stat: "10" / "Years as IC"

Phase 2 — Co-Founder & CTO:
- Years: 2015–2020
- Title: "Technical Co-Founder & CTO"
- Context: "ML-powered computer vision startup"
- Description: "Just me and the CEO, building an ML-powered computer vision platform for the hospitality industry. Architected the entire system, made every technical decision. COVID ended the company, but the experience was invaluable."
- Tech: ["Python", "ML/CV", "AWS", "React", "Architecture"]
- Stat: "CTO" / "From Zero to Product"

Phase 3 — Engineering Manager:
- Years: 2020–Present
- Title: "Engineering Manager"
- Context: "Cylinder Health — Series B HealthTech"
- Description: "Built an engineering team from scratch. Hired every person, doubled the team, launched an internship program, promoted engineers into senior roles. Created a culture where people want to do their best work."
- Tech: ["TypeScript", "React", "Node.js", "Go", "Firebase"]
- Stat: "0→5" / "Team Built from Scratch"

Phase 4 — Current & Next:
- Years: "Now"
- Title: "What's Next"
- Context: "The next chapter"
- Description: "Leading Member Experience, overseeing all front-end engineering, driving CI/CD enablement, architecting HIPAA-compliant AI features. Ready for Director/VP of Engineering or CTO at an early-stage startup."
- Tech: ["AI/LLM", "Go", "React", "DevOps", "Leadership"]
- Stat: "20+" / "Years & Counting"

**Step 2: Add the scoped CSS**

In the `<style>` block, add styles for:

```css
/* Timeline container */
.timeline-container {
  position: relative;
  padding: 4em 0;
}

/* The SVG line */
.timeline-svg {
  position: absolute;
  top: 50%;
  left: 0;
  width: 100%;
  height: 4px;
  transform: translateY(-50%);
  z-index: 1;
  pointer-events: none;
}

.timeline-path {
  stroke: var(--accent);
  stroke-width: 2;
  fill: none;
  stroke-dasharray: var(--path-length);
  stroke-dashoffset: var(--path-length);
  transition: stroke-dashoffset 0.05s linear;
}

/* Phase grid - desktop zigzag */
.phases {
  position: relative;
  z-index: 2;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 2em;
  align-items: start;
}

/* Odd phases: card above center line */
.phase:nth-child(odd) {
  padding-bottom: 6em;
}

/* Even phases: card below center line */
.phase:nth-child(even) {
  padding-top: 6em;
}

/* Phase node - the crosshair at the timeline intersection */
.phase-node {
  position: absolute;
  left: 50%;
  transform: translateX(-50%);
  z-index: 3;
}

.phase:nth-child(odd) .phase-node {
  bottom: 0;
}

.phase:nth-child(even) .phase-node {
  top: 0;
}

/* Year label next to node */
.phase-year {
  font-family: var(--font-mono);
  font-size: 0.6rem;
  letter-spacing: 0.15em;
  text-transform: uppercase;
  color: var(--text-muted);
  text-align: center;
}

/* Leader line connecting node to card */
.leader {
  position: absolute;
  left: 50%;
  width: 1px;
  background: var(--accent);
  opacity: 0.4;
  z-index: 2;
}

.phase:nth-child(odd) .leader {
  bottom: 24px;
  height: calc(6em - 24px);
}

.phase:nth-child(even) .leader {
  top: 24px;
  height: calc(6em - 24px);
}

/* Phase spec card content */
.phase-card h3 {
  font-family: var(--font-mono);
  font-size: 0.85em;
  font-weight: 700;
  letter-spacing: 0.06em;
  text-transform: uppercase;
  margin: 0 0 0.25em;
}

.phase-context {
  font-family: var(--font-mono);
  font-size: 0.65em;
  color: var(--text-muted);
  letter-spacing: 0.04em;
  margin-bottom: 0.75em;
}

.phase-desc {
  font-family: var(--font-serif);
  font-size: 0.9em;
  line-height: 1.6;
  color: var(--text-secondary);
  margin-bottom: 1em;
}

.phase-stat {
  margin-bottom: 0.75em;
  text-align: center;
}

.phase-stat .spec-number {
  font-size: 2em;
}

.phase-stat-label {
  font-family: var(--font-mono);
  font-size: 0.6rem;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  color: var(--text-muted);
}

.phase-tech {
  display: flex;
  flex-wrap: wrap;
  gap: 0.3em;
  margin-top: 0.5em;
}
```

**Step 3: Verify**

Run: `pnpm build`
Expected: Builds successfully.

Run: `pnpm dev` and visit `localhost:4321/journey`
Expected: Page loads with header and four spec cards in a grid. No animation yet.

**Step 4: Commit**

```bash
git add src/pages/journey.astro
git commit -m "feat: add timeline structure with career phase cards"
```

---

### Task 4: Add scroll-driven line drawing animation

**Files:**
- Modify: `src/pages/journey.astro` — add inline `<script>` at end of file

**Step 1: Add the scroll animation script**

Add a `<script is:inline>` block that:

1. Gets the `.timeline-path` SVG element
2. Measures its total length with `getTotalLength()`
3. Sets `--path-length` CSS variable on the element to that length
4. Sets initial `stroke-dasharray` and `stroke-dashoffset` to that length (fully hidden)
5. On scroll, calculates how far the timeline container has been scrolled through the viewport
6. Maps that 0–1 progress to `stroke-dashoffset` from full-length to 0 (fully drawn)
7. Wraps everything in `requestAnimationFrame` for smoothness

```javascript
function initTimeline() {
  var path = document.querySelector('.timeline-path');
  var container = document.querySelector('.timeline-container');
  if (!path || !container) return;

  var length = path.getTotalLength();
  path.style.strokeDasharray = length;
  path.style.strokeDashoffset = length;

  function onScroll() {
    var rect = container.getBoundingClientRect();
    var windowH = window.innerHeight;
    var start = rect.top + windowH * 0.2;
    var end = rect.bottom - windowH * 0.2;
    var progress = Math.max(0, Math.min(1, (windowH - rect.top - windowH * 0.2) / (rect.height - windowH * 0.4)));
    path.style.strokeDashoffset = length * (1 - progress);
  }

  window.addEventListener('scroll', onScroll, { passive: true });
  onScroll();
}
document.addEventListener('astro:page-load', initTimeline);
initTimeline();
```

8. Also add `prefers-reduced-motion` check: if reduced motion, set `stroke-dashoffset: 0` immediately (fully drawn, no animation).

**Step 2: Add reveal classes to phase cards**

Add class `reveal` to each phase card section so they fade in via the existing IntersectionObserver from BaseHead.astro. Add staggered `transition-delay` via inline style.

**Step 3: Verify**

Run: `pnpm dev` and visit `/journey`
Expected: The red SVG line draws itself as you scroll. Cards fade in as they enter the viewport.

**Step 4: Commit**

```bash
git add src/pages/journey.astro
git commit -m "feat: add scroll-driven timeline drawing animation"
```

---

### Task 5: Mobile responsive layout

**Files:**
- Modify: `src/pages/journey.astro` — add responsive CSS in `<style>` block

**Step 1: Add mobile styles**

Add media queries that at `max-width: 768px`:

1. Switch `.phases` grid to `grid-template-columns: 1fr` (single column)
2. Remove the odd/even padding offsets — all cards stack vertically
3. Move the SVG timeline to be a vertical line on the left edge instead of horizontal center:
   - The SVG path becomes a vertical line
   - OR: hide the SVG on mobile and use a CSS `::before` pseudo-element on the phases container as a vertical line
4. Position crosshair nodes on the left edge instead of center
5. Leader lines extend horizontally from node to card instead of vertically
6. Cards get full width with left padding to clear the vertical line

Recommended approach for mobile: Hide the horizontal SVG (`display: none` on mobile). Use a CSS `border-left` on `.phases` as the vertical timeline line. Crosshairs sit on the left edge. Cards extend to the right.

```css
@media (max-width: 768px) {
  .timeline-svg {
    display: none;
  }

  .phases {
    grid-template-columns: 1fr;
    gap: 0;
    border-left: 2px solid var(--accent);
    margin-left: 12px;
    padding-left: 2em;
  }

  .phase:nth-child(odd),
  .phase:nth-child(even) {
    padding: 0 0 2em 0;
  }

  .phase-node {
    left: -2em;
    top: 0;
    transform: translateX(-50%);
  }

  .leader {
    display: none;
  }

  .phase {
    position: relative;
  }
}
```

**Step 2: Test at multiple breakpoints**

Check at 375px (iPhone SE), 390px (iPhone 14), 768px (iPad), and full desktop.

**Step 3: Verify build**

Run: `pnpm build`
Expected: Builds successfully.

**Step 4: Commit**

```bash
git add src/pages/journey.astro
git commit -m "feat: add mobile responsive timeline layout"
```

---

### Task 6: Add "What's Next" footer section and final polish

**Files:**
- Modify: `src/pages/journey.astro`

**Step 1: Add the footer CTA section**

After the timeline container, add a closing section:

```html
<section class="journey-footer reveal">
  <div class="dimension-line">
    <div class="end-mark-left"></div>
    <span class="dim-label">What's Next</span>
    <div class="end-mark-right"></div>
  </div>
  <div class="spec-card footer-card">
    <div class="card-grid-overlay"></div>
    <div class="footer-card-inner">
      <p>I'm at an inflection point. After 20 years of building — systems, teams, and companies — I'm ready for the next challenge. Director/VP of Engineering at a scale-up, or CTO at an early-stage startup building AI products.</p>
      <div class="footer-links">
        <a href="/about" class="footer-link">Read the full story →</a>
        <a href="https://www.linkedin.com/in/johan-buys/" target="_blank" rel="noopener noreferrer" class="footer-link">Connect on LinkedIn ↗</a>
      </div>
    </div>
  </div>
</section>
```

Style the footer-card with centered text, generous padding, and the footer-links as mono-font accent-colored links.

**Step 2: Add crosshair parallax script**

Copy the same parallax script from `index.astro` — on desktop, crosshairs shift slightly on mouse move.

**Step 3: Final visual polish**

- Ensure all spec cards have `.corner-fold`, `.pin`, `.card-grid-overlay` where appropriate
- Verify all text content matches the about page biographical details
- Check that `prefers-reduced-motion` shows the complete page without animations

**Step 4: Verify**

Run: `pnpm build`
Expected: Clean build.

Run: `pnpm dev` → test full page scroll on desktop and mobile.

**Step 5: Commit**

```bash
git add src/pages/journey.astro
git commit -m "feat: add journey footer CTA and final polish"
```
