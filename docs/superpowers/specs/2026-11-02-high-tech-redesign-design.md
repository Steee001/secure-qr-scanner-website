# Design Doc: Secure QR Scanner Website High-Tech Redesign

**Date:** 2026-11-02  
**Topic:** Website High-Tech Redesign & Security Telemetry HUD  
**Status:** In Review (Pending Builder Check & Approval)

---

## 1. Intent & The Why

Secure QR Scanner is an Android application dedicated to quishing and phishing defense, link verification, recall checks, and on-device private scanning. While the current website is functional, its visual design relies on outdated tropes (emoji-driven card grids, soft gradients, hairline borders, and small typography) that convey a generic template instead of an advanced, trustworthy cybersecurity tool.

The goal of this redesign is to project a sharp, authoritative, modern high-tech image that commands immediate credibility, showcases all key features compellingly, ensures seamless mobile and desktop responsiveness, and guarantees 100% functionality for all critical outgoing and internal links.

---

## 2. Goals, Non-Goals, & Anti-Goals

### Goals
- **High-Tech Aesthetic & Authority:** Establish an engineered, cyber-defense visual identity utilizing the "One Motif" concept (optical scanner reticle / viewfinder brackets `[ ]` and telemetry inspection panels).
- **Substantive Feature Presentation:** Replace generic emoji cards with concrete "Security Telemetry & Inspection Panels" illustrating real app capabilities:
  1. *Quishing & Phishing Defense:* Step-by-step redirect chain resolution (`bit.ly` &rarr; destination) and eTLD+1 domain isolation.
  2. *Link Checking from Any App:* System share-sheet integration & clipboard inspection.
  3. *Wi-Fi & Action Verification:* Explicit review against unencrypted or WEP networks.
  4. *Barcode & Product Recall Alerts:* Recall matching (EU Safety Gate, FDA, CPSC) and Open Food Facts enrichment.
  5. *On-Device Document Scanning & OCR:* 100% local ML Kit models and zero cloud upload.
  6. *Privacy-First Architecture:* AES-256 Android Keystore encrypted history, no ads, no trackers, optional offline-only mode.
- **Flawless Link Functionality:**
  - Google Play Store badge / CTA (`https://play.google.com/store/apps/details?id=com.steee001.secureqrscanner`)
  - Ko-fi support link (`https://ko-fi.com/steee001`)
  - Navigation between `index.html`, `quishing.html`, `privacy.html`, `feedback.html`
  - Feedback page issue templates & query parameters (`v`, `lang`)
  - Security disclosure (`.well-known/security.txt`)
- **Strict Anti-Slop / Taste Compliance:** 0 lint FAILs, 0 inspect FAILs on desktop (1440px), tablet (768px), and mobile (390px). No emojis as UI, no hairline borders, no gradient buttons, no resting shadows.

### Non-Goals
- Migrating to a heavy JavaScript framework (React, Vue, Next.js). The site stays vanilla HTML5 and modern CSS for zero bundle bloat and near-instant load times.
- Introducing complex backend services or interactive JS games/playgrounds (the user requested a focused, static presentation with technical aesthetic).
- Modifying legal privacy text or GitHub issue schemas.

### Anti-Goals
- Generic SaaS slop (floating glassmorphism cards, pastel gradient blobs, emoji bullet points).
- Unreadable "hacker neon" tropes that destroy contrast and accessibility.
- Breakage of deep links or mobile navigation.

---

## 3. Constraints

- **Execution Environment:** Vanilla HTML/CSS running statically on GitHub Pages.
- **Responsiveness:** Flawless layout across 320px–2560px screen widths. Touch targets >= 44px.
- **Cross-page Consistency:** Header, navigation, and footer must be seamlessly unified across `index.html`, `quishing.html`, `privacy.html`, and `feedback.html`.
- **Local Verification:** No git commits before explicit review and approval by the user.

---

## 4. Approaches Considered

1. **Approach 1: Security Telemetry & Scanner HUD (Selected)**
   - *Description:* Technical cyber-security aesthetic using deep obsidian tones, high-contrast crisp text, subtle scanner reticle geometry `[ ]`, and static inspection dissection panels displaying simulated real security diagnostics.
   - *Trade-offs:* Requires meticulous CSS layout and typography craft to maintain restraint while looking high-tech.
   - *Decision:* Chosen by user for its focused static presentation and authentic cyber-security character.

2. **Approach 2: Minimalist Technical Datasheet (Editorial Precision)**
   - *Description:* Swiss-style black-and-white data sheet with large display numbers and editorial typography.
   - *Trade-offs:* Too academic/nüchtern; lacks the visual connection to visual optical scanning.
   - *Decision:* Rejected.

3. **Approach 3: App-First Product Showcase**
   - *Description:* Hero phone mockup dominating the page with surrounding card blocks.
   - *Trade-offs:* Conventional app landing page; does not deliver the elevated high-tech feeling.
   - *Decision:* Rejected.

---

## 5. Architectural & Visual Specifications

### 5.1 Color Tokens & Palette
- Ground: Obsidian night `#071110` (deep, focused security dark tone)
- Surface Elevation 1: `#0c1a18` (subtle step up for telemetry panels)
- Surface Elevation 2 / Active: `#122724`
- Ink (Primary Text): High-contrast clean white `#F4F7F6`
- Ink Muted: Technical muted teal-grey `#8FAEA9`
- Accent (Primary Action / Safe): Crisp Cyber Emerald `#00D696` (or brand pine `#0F6B64` with `#00D696` high-tech accent)
- Status Warn: `#F59E0B` (Amber)
- Status Danger: `#EF4444` (Threat Red)

### 5.2 Typography
- Modern engineered sans-serif stack: `-apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Inter", sans-serif` with tabular numbers where telemetry aligns.
- Scale: Fluid type clamp:
  - Hero display headline: clamp(2.2rem, 1.6rem + 3vw, 3.8rem) (2 lines or fewer, confident focal point).
  - Section headings: clamp(1.5rem, 1.2rem + 1.2vw, 2.2rem).
  - Body text: 16px–18px, line-height 1.55.
  - Telemetry tags / captions: 13px–14px clean sentence-case.

### 5.3 Scanner Reticle Motif `[ ]`
- Precise SVG / CSS corner brackets framing key focal points (the hero security preview and the telemetry panels).
- Replaces generic rounded cards with technical precision containers.

### 5.4 Structure of `index.html`
1. **Header & Sticky Nav:**
   - Wordmark with brand icon `icon.png`
   - Clean navigation links (`Features`, `Quishing Guide`, `Privacy Policy`, `Feedback`) with active states
   - Quick action link (`Get App`)
2. **Hero Section (The Focal Point):**
   - Left: Confident display title (*"Spot QR scams & fake links before they open"*), technical subhead, primary Google Play Store badge button, secondary Ko-fi / Support button.
   - Right: Framed Security Preview HUD showing the app's review dialog inside precision reticle corners.
3. **Telemetry Showcase: The Link Dissection Panel:**
   - Static technical demonstration showing how a real quishing attack is intercepted:
     - Input: Shortened scam URL (`bit.ly/3xParking...`)
     - Resolving: Redirect chain breakdown & eTLD+1 identification (`parking-meter-pay.com.attacker.net` &rarr; flagged)
     - Security Verdict: Threat database match & offline heuristic warning.
4. **Core Capabilities (Asymmetric High-Tech Grid):**
   - Structured panels with technical SVG glyphs (no emojis!):
     - Panel 1: Quishing & Phishing Defense (Redirect unmasking & punycode detection)
     - Panel 2: Cross-App Link Verification (Share sheet & clipboard inspection)
     - Panel 3: Wi-Fi & Action Verification (WEP warning & contact safeguards)
     - Panel 4: Product Barcodes & Recall Alerts (Safety Gate & Open Food Facts)
     - Panel 5: On-Device Document OCR (100% local ML Kit models)
     - Panel 6: Zero-Knowledge Privacy Architecture (AES-256 Android Keystore, 0 tracking, offline mode)
5. **Call to Action & Security Commitment:**
   - Clear download statement, Play Store button, Ko-fi badge, link to security.txt disclosure.
6. **Footer:**
   - Balanced, clean single-band footer with copyright and navigation links.

### 5.5 Unified Subpages (`quishing.html`, `privacy.html`, `feedback.html`)
- Align typography, surface colors, headers, and footers with the new high-tech design tokens.
- Replace emojis in `feedback.html` with clean SVG technical icons.
- Preserve all existing logic (e.g., query param detection for app version/lang in `feedback.html`).

---

## 6. What's Left to the Builder

- Exact SVG icon paths for the 6 feature areas and feedback categories.
- Specific CSS custom properties naming and responsive breakpoint tuning (768px tablet, 390px mobile).
- Optimization of image attributes (`loading="eager"` on hero preview, `width`/`height` attributes to avoid CLS).
