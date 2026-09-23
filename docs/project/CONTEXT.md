# Context

Use this file for durable project context that agents need across sessions.

## Project-Specific Facts

- Static website for the Craft and Conscious business — pure HTML/CSS, no build system, no
  backend, no CI.
- 8 versioned site iterations tracked as sibling directories: `v1`-`v6`, `v8`, `v9` (no `v7` — a
  gap in the sequence, not investigated, not necessarily a problem). `v9` is current.
- AntBrainOS vault continuity for this repo lives at
  `03_PROJECTS/Active/Craft_and_Conscious_Website/` in the AntBrainOS Obsidian vault — distinct
  from `03_PROJECTS/Active/Craft_and_Conscious/`, which tracks an unrelated Apple Numbers
  spreadsheet project for the same business.

## Design-Exploration Branches (New Pattern, 2026-09-22)

`design/olive-atelier` is the first branch on this repo following the `Hair-by-Alexy` repo's
established pattern: a from-scratch, unrelated visual design direction, deliberately kept
unmerged, deployed live to its own dedicated VPS subdomain
(`https://olive-atelier.craftandconscious.com`, on the same IONOS VPS that hosts `main`'s
`craftandconscious.com`). Subdomain naming convention: `<variant-slug>.craftandconscious.com`
(no repeated business-slug, since `craftandconscious.com` is this business's own apex domain —
matching `spa.craftandconscious.com`/`promptvault.craftandconscious.com`, not the
`<business-slug>.<variant-slug>.craftandconscious.com` pattern used for *other* clients' branches
like `hair-by-alexy.luxe-noir.craftandconscious.com`). Per that same precedent, design-exploration
branches are pushed **untagged**. See `docs/project/DECISION_LOG.md`'s 2026-09-22/23 entry.

## Known Constraints

- Governance/Starter-Kit tooling must never modify `v1`-`v9`/`images/` site content.
- 10 optional Starter Kit modules are enabled as of 2026-09-16 (`threat_model`,
  `security_requirements`, `dependency_risk`, `secret_scan`, `license_policy`, `browser_matrix`,
  `accessibility`, `web_performance`, `seo`, `release_metadata`); their policy docs were filled
  with real project content 2026-09-17. No CI/build automation exists — the modules are
  documentation-only.
- Accessibility target: WCAG 2.2 AA (confirmed with owner 2026-09-17). Verified 2026-09-17 via a
  live headless-Chromium script (Playwright, installed only in a scratch directory, never a
  project dependency): keyboard operability/focus order, focus visibility, and pixel-sampled color
  contrast for `v9/index.html` — 2 contrast failures and 1 modal-dialog gap found and fixed.
  Verified again 2026-09-18 via an automated axe-core 4.13.0 scan (WCAG 2.2 AA tags, both
  initial-load and cart-open states) — 3 further real Tier 1 issues found and fixed (missing
  `<select>` labels, an `aria-hidden` container with a real focusable button, 2 more contrast
  failures). 0 axe violations remain in either state as of `v0.1.1`. Still untested: mobile/touch
  viewport. Still open (axe can't detect): the cart dialog's background isn't marked `inert` while
  open.
- Browser support: last 2 major versions of Chrome, Firefox, Safari, Edge; no Internet Explorer
  (confirmed with owner 2026-09-17).

## Repeated Corrections

- **Verify accessibility claims live before writing them into a policy doc — don't infer from
  reading CSS alone.** The 2026-09-17 session first wrote that `.btn`/`.mood-btn`/
  `.cart-line-qty-btn` "lack :focus-visible styling" based on not seeing a dedicated CSS rule for
  them. A live keyboard test the same day showed this was wrong — the browser's own default
  outline renders visibly for all of them. The real, more significant gap (no focus trap in the
  cart dialog) was only found by actually testing, not by reading the stylesheet. Prefer live
  verification over CSS inspection for any accessibility claim in this repo's docs.
