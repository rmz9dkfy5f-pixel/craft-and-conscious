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

## Known Constraints

- Governance/Starter-Kit tooling must never modify `v1`-`v9`/`images/` site content.
- 10 optional Starter Kit modules are enabled as of 2026-09-16 (`threat_model`,
  `security_requirements`, `dependency_risk`, `secret_scan`, `license_policy`, `browser_matrix`,
  `accessibility`, `web_performance`, `seo`, `release_metadata`); their policy docs were filled
  with real project content 2026-09-17. No CI/build automation exists — the modules are
  documentation-only.
- Accessibility target: WCAG 2.2 AA (confirmed with owner 2026-09-17) — not yet verified against
  (no keyboard/focus-order or color-contrast pass has been run).
- Browser support: last 2 major versions of Chrome, Firefox, Safari, Edge; no Internet Explorer
  (confirmed with owner 2026-09-17).

## Repeated Corrections

Add facts here when an agent makes the same mistake more than once.
