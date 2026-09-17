# Accessibility Policy

This module (`accessibility`) generates this policy. It runs no scanner and assumes no tool: the
conformance target below is this project's own commitment, checked with whatever tooling it
already uses or chooses to adopt.

## Conformance target

**WCAG 2.2 Level AA** — confirmed with the owner 2026-09-17.

## What is checked

- **Semantic HTML:** already used in `v9/index.html` — `<header>`, `<nav aria-label="Primary
  navigation">`, `<main>`, `<footer>`, and `<article>` for product/collection/journal cards.
- **ARIA usage beyond semantic HTML:** the cart panel uses `role="dialog" aria-modal="true"
  aria-labelledby="cart-heading"`; the newsletter status message uses `aria-live="polite"`;
  decorative imagery (the CSS background-image fills used for hero/product cards, which are not
  real product photos) is marked `aria-hidden="true"`.
- **Keyboard operability and focus order:** verified 2026-09-17 via a live headless-Chromium pass
  (Playwright), tabbing through every one of the 36 focusable elements on the page. Tab order
  matches visual/reading order throughout (logo → nav → hero CTAs → filter controls → product
  grid, in DOM/visual order). All reachable controls are native HTML elements (`<a>`, `<button>`,
  `<select>`, `<input>`) and are keyboard-operable by default — no custom widget needed a bespoke
  keydown handler except the cart dialog (see below).
- **Focus visibility:** verified live — every one of the 34 reachable main-page elements receives
  a visible focus indicator on genuine keyboard Tab (Chromium's default `outline: auto`, or an
  explicit `:focus-visible` rule where one is defined, e.g. filter `<select>`s and the newsletter
  input). **Correction to this doc's prior entry:** `.btn`, `.mood-btn`, and the cart's
  `.cart-line-qty-btn`/close button do *not* lack a visible focus indicator, as previously assumed
  here before live testing — the browser's own default outline renders visibly for all of them.
- **Color contrast:** measured 2026-09-17 by pixel-sampling the actual rendered page (not just
  reading CSS hex values) across 9 real text/background locations, including text over the hero's
  radial-gradient background and the header's translucent overlay. Two real AA failures were found
  and fixed: `--muted` text (was `#8c7a69`, used for subtitles, nav links, footer, product notes)
  measured 3.66:1–4.12:1 depending on background (needs 4.5:1) — darkened to `#7b6b5c`, now
  4.56:1–5.12:1 across every sampled location. `.btn-primary` text (was `#26160b` on the
  `#b46a3c`→`#e6b27b` gradient) measured 4.22:1 at the gradient's darker stop — changed to `#000`,
  now 5.07:1–11.02:1 across the gradient. Both fixes verified against live rendered pixels, not
  just computed hex math.
- **Modal dialog behavior:** the cart panel's `role="dialog" aria-modal="true"` was not backed by
  real modal keyboard behavior — found and fixed 2026-09-17, see Known Exceptions.
- **Alternative text:** the logo `<img>` has descriptive `alt` text
  ("Craft Candle Company logo"). Product and hero imagery are CSS background-image fills marked
  `aria-hidden="true"` rather than `<img>` elements needing alt text, since they are decorative
  fills rather than the literal product photo for each item.

## Verification Practice

2026-09-17: a live headless-Chromium pass (Playwright) verified keyboard operability, focus order,
focus visibility, and pixel-sampled color contrast against WCAG 2.2 AA for the current `v9`
version — see the What Is Checked entries above for exact method and results. No automated
scanner (axe, Lighthouse accessibility audit) has been run; the manual/scripted pass above is the
only verification performed so far. Re-run this pass before each future content release, not only
once.

## Known Exceptions

- No axe-core/Lighthouse automated scan has been run — the 2026-09-17 pass was a targeted script,
  not a comprehensive automated audit; a broader scan could still surface issues it didn't check
  for (e.g. ARIA attribute correctness beyond the elements sampled, screen-reader announcement
  behavior).
- Mobile/touch-specific accessibility (tap target sizing, screen-reader gesture navigation on
  iOS/Android) has not been tested — the 2026-09-17 pass used a 1280×900 desktop viewport only.
- **Fixed 2026-09-17 (previously an open exception, now resolved):** the cart dialog
  (`role="dialog" aria-modal="true"`) did not move focus into itself on open, did not trap
  Tab/Shift+Tab within it, and had no Escape-to-close handler — a keyboard user could tab straight
  through an open, visually-blocking dialog into the obscured page behind it. Fixed in
  `v9/index.html`: opening the cart now moves focus to its close button, Tab/Shift+Tab cycles only
  within the panel while open, Escape closes it and returns focus to whichever control opened it.
  Verified live: focus-on-open, forward trap, backward wrap, and Escape-plus-focus-return all
  confirmed via genuine keyboard interaction, zero console/page errors.

## What this module deliberately does not do

- Does not run a scanner, screen reader, or any other accessibility tool, and does not assume one.
- Does not guarantee legal conformance in any jurisdiction - it states and requires verification of
  a technical target, which is necessary but not sufficient for legal compliance.
- Does not define a new evidence document or finding code.
