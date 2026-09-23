# Browser Matrix Policy

This module (`browser_matrix`) generates this policy. It runs no browser, launches no test, and
assumes no testing tool: the matrix below is this project's own statement, verified with whatever
tooling it already uses or chooses to adopt.

## Supported matrix

- **Browsers:** last 2 major versions of Chrome, Firefox, Safari, and Edge — evergreen,
  auto-updating browsers only. Confirmed with the owner 2026-09-17. No Internet Explorer support
  (any version) — the site already uses features IE never implemented (CSS custom properties,
  `backdrop-filter`, `clamp()`, CSS Grid, `:focus-visible`), so this names an existing fact rather
  than introducing a new restriction.
- **Devices/viewports:** three breakpoints, matching `v9/index.html`'s own CSS exactly:
  - Desktop: > 960px — full multi-column grid (4-column product grid, 3-column collections/journal
    grids).
  - Tablet: 768px–960px — condensed grids (3-column product grid, 2-column collections/journal),
    hero switches to a single stacked column.
  - Mobile: < 768px, with a further breakpoint at 520px — top nav collapses to a hamburger toggle
    at 768px; product grid drops to 2 columns at 768px and 1 column at 520px. **Live-verified
    2026-09-22** (previously an asserted-but-untested claim, per this doc's own prior Verification
    practice note below — corrected per this repo's standing rule to verify accessibility/behavior
    claims live rather than assume them): the toggle itself had no JavaScript wiring until
    2026-09-22 and was completely non-functional (nav and cart both unreachable below 768px); now
    fixed and confirmed live via touch interaction and DOM state checks at 390×664 (iPhone 13
    emulation) and at the documented 768/520px breakpoints.
- **Operating systems:** none verified separately from the browser matrix above — no OS-specific
  feature is used; coverage follows whichever OS each listed evergreen browser runs on (Windows,
  macOS, iOS, Android).

## Verification practice

- Manual only: resize a browser window through the three stated breakpoints and load the current
  site (`v9/index.html`) in at least one Chromium-based browser and Safari specifically before any
  content release — `backdrop-filter` and `-webkit-background-clip: text` (both used in this
  file's CSS) have a history of needing WebKit-specific handling.
- No automated cross-browser or visual-regression tool is configured — there is no CI for this
  repository (`docs/governance/REPOSITORY_HANDOFF_CONFIG.md`'s Validation Contract: no
  install/test/build tooling exists).
- Cadence: before each content release (a new version folder or a change to the current `v9`), not
  on a calendar schedule.

## Known gaps

- Internet Explorer (any version) is not supported, and cannot be without removing CSS features
  already in production use.
- No support commitment beyond "last 2 major versions" — an older evergreen-browser install (e.g.
  a far-behind Firefox ESR) is not guaranteed to render correctly.

## What this module deliberately does not do

- Does not launch, drive, or configure a browser, and does not assume a cross-browser testing
  tool, device lab, or CI provider.
- Does not run any check itself - the matrix above is what this project's own verification
  practice, whatever form it takes, is checked against.
- Does not define a new evidence document or finding code.
