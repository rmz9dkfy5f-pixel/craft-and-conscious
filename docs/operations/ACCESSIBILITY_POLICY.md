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
- **Keyboard operability and focus order:** not yet formally verified end-to-end. All interactive
  controls (nav links, filter `<select>` elements, mood buttons, add-to-cart buttons, the cart
  toggle, the newsletter form) are native, keyboard-operable HTML elements by default, but no
  keyboard-only pass has actually been performed and recorded.
- **Focus visibility:** `:focus-visible` styling is explicitly defined for nav links, filter
  `<select>`s, and the newsletter email input. It is **not** yet defined for `.btn`, `.mood-btn`,
  or `.cart-line-qty-btn` beyond the browser's own default outline — see Known Exceptions.
- **Color contrast:** not yet formally measured against this site's actual color tokens (e.g.
  `--muted: #8c7a69` text on `--bg: #f6f1ea`) at the WCAG 2.2 AA thresholds.
- **Alternative text:** the logo `<img>` has descriptive `alt` text
  ("Craft Candle Company logo"). Product and hero imagery are CSS background-image fills marked
  `aria-hidden="true"` rather than `<img>` elements needing alt text, since they are decorative
  fills rather than the literal product photo for each item.

## Verification Practice

No automated scanner (axe, Lighthouse accessibility audit, etc.) has been run against this site
yet — this is a real, unverified gap, not a passed check. Verification should run before each
content release once adopted, not only once at project start.

## Known Exceptions

- Color-contrast conformance against WCAG 2.2 AA has not yet been measured for any version of this
  site (`v1`–`v9`).
- Full keyboard-operability and focus-order verification has not yet been performed.
- `.btn`, `.mood-btn`, and `.cart-line-qty-btn` have no dedicated `:focus-visible` rule beyond the
  browser default — a known, specific instance of the focus-visibility gap above, not yet
  remediated.

## What this module deliberately does not do

- Does not run a scanner, screen reader, or any other accessibility tool, and does not assume one.
- Does not guarantee legal conformance in any jurisdiction - it states and requires verification of
  a technical target, which is necessary but not sufficient for legal compliance.
- Does not define a new evidence document or finding code.
