# High-Tech Redesign Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Rebuild the Secure QR Scanner marketing website with an authoritative, modern high-tech visual identity ("Security Telemetry & Scanner HUD"), zero taste-skill lint/inspect FAILs, and 100% verified link functionality.

**Architecture:** Pure vanilla HTML5 and modern responsive CSS with dynamic viewport units, fluid type scaling (`clamp`), container-based layouts, and an optical scanner reticle motif `[ ]`. All interactive simulation and telemetry demonstrations are crafted statically with semantic HTML and CSS without heavy JS dependencies or bundle overhead.

**Tech Stack:** HTML5, CSS3 (CSS Custom Properties, Flexbox, Grid, Dynamic Viewport Units, Container Queries), SVG vector graphics, tasteskill lint & inspect tooling (Node.js 22+, Headless Chrome).

**Spec:** [docs/superpowers/specs/2026-11-02-high-tech-redesign-design.md](file:///C:/Users/falte/Repos/secure-qr-scanner-website/docs/superpowers/specs/2026-11-02-high-tech-redesign-design.md)

## Global Constraints

- Ground color: `#071110`; Surface elevation 1: `#0c1a18`; Surface elevation 2: `#122724`; Ink primary: `#F4F7F6`; Ink muted: `#8FAEA9`; Accent safe/action: `#00D696`.
- Anti-slop rules: 0 emoji as UI icons, 0 gradients, 0 hairline borders (`border: 1px solid` without surface fill), 0 resting shadows, 0 pill badges or floating glass panels.
- Typography: Display headlines 2 lines or fewer at 1440px, 768px, and 390px. Body copy >= 16px. Fluid type clamp for display headers (`clamp(2.2rem, 1.6rem + 3vw, 3.8rem)`).
- Outbound and navigation links must preserve target URLs, `rel="noopener"`, and exact URL query parsing logic on `feedback.html` (`v`, `lang`).
- No git commits until user explicitly reviews the local result.

## Review Focus

- Broken mobile navigation layout on small screens (< 390px): Navigation links must wrap gracefully or stack cleanly without horizontal scroll.
- Link degradation on secondary action buttons (e.g. Ko-fi or Google Play): Verify exact URLs and keyboard focus visibility (`:focus-visible`).
- Cumulative Layout Shift (CLS) on the hero preview graphic: Explicit `width`, `height`, and `aspect-ratio` on all `<img>` tags.
- Disrupted issue URL generation in `feedback.html`: Query string parameters for `version` and `locale` must be parsed and appended properly to GitHub issue templates.
- Contrast failure between muted text and dark surfaces: Body and caption text must exceed WCAG AA (4.5:1 for normal text, 3:1 for large display text).

---

### Task 1: Design Tokens, Typography, & Base Resets in `styles.css`

**Files:**
- Modify: `styles.css`

**Interfaces:**
- Consumes: Design doc color and typography specifications.
- Produces: CSS custom properties (`--bg-ground`, `--surface-1`, `--surface-2`, `--ink-primary`, `--ink-muted`, `--accent-cyber`, `--status-danger`, `--status-warn`), reset rules, fluid typography scale, and reticle corner utility classes (`.reticle-box`, `.reticle-corner`).

- [ ] **Step 1: Define design tokens and base styles in `styles.css`**
  Set `:root` CSS variables for the palette, fluid font sizes using `clamp()`, and remove gradient/shadow definitions.

- [ ] **Step 2: Implement reticle corner bracket geometry and surface styling in `styles.css`**
  Add `.reticle-frame` with clean pseudo-elements or border corners representing scanner viewfinder brackets `[ ]`.

- [ ] **Step 3: Run taste-skill linter on `styles.css` to verify removal of banned patterns**
  Run: `node "C:\Users\falte\.gemini\config\plugins\taste-skill\skills\design-taste-frontend\scripts\lint.mjs" styles.css`
  Expected: 0 FAILs on `styles.css`.

---

### Task 2: Sticky Header & Navigation Unification

**Files:**
- Modify: `styles.css`
- Modify: `index.html`
- Modify: `quishing.html`
- Modify: `privacy.html`
- Modify: `feedback.html`

**Interfaces:**
- Consumes: Task 1 tokens (`--bg-ground`, `--surface-1`, `--ink-primary`, `--accent-cyber`).
- Produces: High-tech sticky navigation header with wordmark, active link indicator, and direct CTA button.

- [ ] **Step 1: Style modern header in `styles.css`**
  Replace blurred glass background with solid flat tone step (`--bg-ground` with subtle bottom tone border, no hairline rules). Add accessible keyboard focus rings (`:focus-visible`).

- [ ] **Step 2: Update header markup across all HTML files**
  Standardize `<header>` across `index.html`, `quishing.html`, `privacy.html`, and `feedback.html`.

- [ ] **Step 3: Verify header responsiveness on mobile (390px) and desktop (1440px)**
  Check that navigation remains accessible, does not overflow horizontally, and maintains touch targets >= 44px.

---

### Task 3: Hero Section & Security Preview HUD in `index.html`

**Files:**
- Modify: `index.html`
- Modify: `styles.css`

**Interfaces:**
- Consumes: Task 1 tokens and reticle classes.
- Produces: High-impact hero section with display headline (<= 2 lines), Google Play & Ko-fi action buttons, and framed preview HUD.

- [ ] **Step 1: Structure Hero markup in `index.html`**
  Rebuild `<section class="hero">` with `<h1>Spot QR scams & fake links before they open</h1>`, technical subhead, primary flat Play Store CTA button (`.btn-cyber`), secondary support button, and `.hero-hud` container.

- [ ] **Step 2: Implement Hero styling in `styles.css`**
  Apply asymmetric 2-column grid on desktop, stacking on tablet/mobile. Frame `preview.png` inside the `.reticle-frame` HUD with telemetry markers. Add `aspect-ratio` to avoid CLS.

- [ ] **Step 3: Verify Hero in browser inspector**
  Ensure headline does not wrap past 2 lines and has a dominant display focal point.

---

### Task 4: Link Dissection Telemetry Panel (Static Demonstration)

**Files:**
- Modify: `index.html`
- Modify: `styles.css`

**Interfaces:**
- Consumes: Task 1 tokens.
- Produces: `.telemetry-panel` showing the 3-step security dissection of a suspicious short link (Incoming QR Link &rarr; Redirect Resolution & eTLD+1 &rarr; Threat Verdict).

- [ ] **Step 1: Write HTML markup for the Link Dissection Panel in `index.html`**
  Create `<section class="telemetry-section">` featuring a simulated security scan of a quishing attack:
  - Step 1: Raw QR payload (`https://bit.ly/3xParking...`)
  - Step 2: Unmasked redirect chain & isolated destination domain (`parking-pay.com.attacker-fraud.net`)
  - Step 3: Diagnostic status badge (`[FLAGGED: MALICIOUS DOMAIN]`).

- [ ] **Step 2: Add telemetry styling and monospace inspection blocks in `styles.css`**
  Style telemetry elements using clean tabular monospace blocks with syntax-highlighted domain boundaries and status tags.

- [ ] **Step 3: Validate responsive stacking for mobile displays**
  Verify that the telemetry steps wrap into an intuitive top-to-bottom pipeline on mobile viewports (< 600px).

---

### Task 5: Core Capabilities Asymmetric Grid with SVG Glyphs

**Files:**
- Modify: `index.html`
- Modify: `styles.css`

**Interfaces:**
- Consumes: Task 1 tokens.
- Produces: 6 core capability panels with technical SVG vector icons replacing emojis.

- [ ] **Step 1: Author inline SVG vector icons for the 6 capabilities**
  Design clean, geometric technical SVG icons (Shield/Radar for Quishing, External Link for App Verification, Wi-Fi Signal for Network Checks, Barcode for Recalls, Document/Scan for OCR, Keystore Lock for Privacy).

- [ ] **Step 2: Rebuild feature panels in `index.html`**
  Replace emoji cards with technical panels (`.feature-panel`) containing SVG icons, crisp headings, and concise technical feature descriptions.

- [ ] **Step 3: Style feature grid in `styles.css`**
  Use responsive grid layout with subtle tone elevation on hover (`--surface-2`), no resting shadows, and no hairline borders.

---

### Task 6: Subpage Alignment & Feedback Form Integration

**Files:**
- Modify: `quishing.html`
- Modify: `privacy.html`
- Modify: `feedback.html`
- Modify: `styles.css`

**Interfaces:**
- Consumes: Task 1 tokens and Task 5 SVG glyphs.
- Produces: Visually unified prose and feedback pages with preserved JavaScript URL parameter parsing.

- [ ] **Step 1: Update `quishing.html` prose styling & callout boxes**
  Replace generic blockquotes with high-tech security notice callouts and ensure typography hierarchy is consistent.

- [ ] **Step 2: Update `privacy.html` structure & styling**
  Harmonize typography and link styles. Ensure security disclosure link `.well-known/security.txt` remains intact.

- [ ] **Step 3: Update `feedback.html` with SVG icons and verify query string script**
  Replace emojis (🐛, 💡, 🛡️, ☕) with clean SVG glyphs. Ensure `link-bug`, `link-feat`, `link-sec`, and `detected-context` elements function correctly with URL query parameters (`v`, `lang`).

---

### Task 7: Taste-Skill Gate Verification & Visual Inspection

**Files:**
- All HTML and CSS files

**Interfaces:**
- Consumes: All updated site files.
- Produces: 0 lint FAILs, 0 inspect FAILs across 1440px, 768px, and 390px viewports, before/after comparison screenshots.

- [ ] **Step 1: Run `lint.mjs` on all modified files**
  Run: `node "C:\Users\falte\.gemini\config\plugins\taste-skill\skills\design-taste-frontend\scripts\lint.mjs" index.html quishing.html privacy.html feedback.html styles.css`
  Expected: 0 FAILs.

- [ ] **Step 2: Run `inspect.mjs` on `index.html`**
  Run: `node "C:\Users\falte\.gemini\config\plugins\taste-skill\skills\design-taste-frontend\scripts\inspect.mjs" index.html --out .taste-skill/after`
  Expected: 0 FAILs across 1440px, 768px, and 390px.

- [ ] **Step 3: Visual inspection of generated screenshots**
  Open and review screenshots in `.taste-skill/after/` across desktop, tablet, and mobile.

- [ ] **Step 4: Functional link check**
  Verify all store links, Ko-fi links, and internal navigation paths.
