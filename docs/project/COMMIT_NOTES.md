# Commit Notes

## Suggested Commit Template

```text
<type>: <short summary>

- What changed:
- Why:
- Validation:
- Risks:
```

## Commit Types

- feat
- fix
- docs
- refactor
- test
- chore
- security
- perf

## 2026-09-23 — fix: wire up mobile nav toggle; docs: record stale untracked prod deployment

## Summary

- Fixed the owner-confirmed next task (mobile/touch-viewport accessibility): the mobile nav toggle
  had zero JavaScript wiring, making primary navigation and the cart completely unreachable below
  768px. Also documents a major discovery: `main` has a real, stale, untracked production
  deployment at `craftandconscious.com`. Also includes the 2026-09-22 governance backfill that was
  written but never actually committed in that session (staged `v9/index.html` only, not these two
  files).

## Description

- What changed: `v9/index.html` — wired `.nav-toggle` as a disclosure widget (`aria-expanded`/
  `aria-controls`, opens on tap, closes on nav-link click or `Escape` with focus return), added the
  mobile dropdown-panel CSS, hid the redundant `.nav-links-desktop-only` button in the mobile menu.
  `docs/governance/{PROJECT_CLASSIFICATION,REPOSITORY_HANDOFF_CONFIG}.md` — pulled in
  `design/olive-atelier`'s branch-scoped deploy-target note, then corrected `main`'s own
  classification from `git_backed_with_remote` to `git_backed_with_deployment` after discovering
  its real (stale, untracked) production deployment; added a Deploy Targets table row for it.
  `docs/operations/{ACCESSIBILITY_POLICY,BROWSER_MATRIX_POLICY}.md` — recorded the mobile pass and
  corrected the hamburger-toggle claim from asserted-but-untested to live-verified.
  `docs/project/{STATUS,COMMIT_NOTES,DECISION_LOG}.md` — backfilled with all of the above, plus the
  2026-09-22 work that was never committed.
- Why: owner-confirmed next task from the 2026-09-22 closeout; the deployment discovery surfaced
  during that work and the owner chose to document it now rather than fold investigation/redeploy
  into this same session.
- Validation: live headless-Chromium (Playwright, scratch-directory-only dependency) — nav toggle
  opens/closes correctly via tap, nav-link click, and `Escape` (with focus return); cart reachable
  on mobile with `inert`/focus-trap behavior intact; axe-core 4.13.0 (WCAG 2.2 AA) 0 violations
  across 3 new mobile states (initial-load, nav-open, cart-open); all 3 documented breakpoints
  behave as specified; `.cart-line-qty-btn` (22×22) confirmed to qualify for the WCAG 2.2 SC 2.5.8
  spacing exception (45px center-to-center) rather than resized. Deployment discovery verified via
  read-only `curl`/DNS only (`HTTP 200`, `Last-Modified: 2025-11-26`, resolves to the known IONOS
  VPS) — no SSH, no deploy action taken.
- Risks: none from the code change. The stale production deployment itself is a pre-existing risk
  (real visitors have been getting unfixed accessibility bugs) that this commit documents but does
  not resolve — see `docs/project/DECISION_LOG.md`'s 2026-09-23 entry for why that was deferred.

## 2026-09-22 — fix: mark .mood-buttons as a group and inert the page behind the open cart dialog

## Summary

- Fixed the 2 remaining axe-noted items from the 2026-09-18 scan.

## Description

- What changed: `v9/index.html` — added `role="group"` to `.mood-buttons`; added a `pageWrapper`
  reference and toggled the native `inert` attribute on `.page` from `openCart()`/`closeCart()`.
- Why: owner-confirmed next task from the 2026-09-18 closeout.
- Validation: live headless-Chromium (Playwright, scratch-directory-only dependency) check —
  `.mood-buttons` reports `role="group"`; opening the cart applies `inert` to `.page`, blocks a
  background nav-link click, and confirms the background element sits inside an inert subtree;
  closing the cart removes `inert`. axe-core 4.13.0 (WCAG 2.2 AA tags) re-scan: 0 violations in
  both initial-load and cart-open states. `git status` confirmed only `v9/index.html` changed.
- Risks: none identified. `inert` is native, no dependency added, supported by all evergreen
  browsers within this repo's last-2-versions/no-IE11 browser matrix.

## 2026-09-08 — chore: adopt AntBrainOS Project Starter Kit v3.10.0

## Summary

- Adopt Project Starter Kit v3.10.0 (`web_application` profile, governance layer only) via
  `scripts/starter_kit.py`'s `adopt-audit` -> `plan-migration` -> `migrate --apply` sequence.

## Description

- What changed: added `AGENTS.md`, `.agents/skills/`, `docs/governance/`, `docs/project/`,
  `ai/`, and `.starter-kit/` manifest/state files. No optional modules enabled (no CI, no
  security-baseline enforcement).
- Why: bring this repo under AntBrainOS governance/documentation conventions, matching prior
  adoptions on other project repos.
- Validation: `inspect` (PASS), `adopt-audit --allow-non-default-branch` (PASS_WITH_WARNINGS,
  only the expected non-default-branch warning), `plan-migration` (66 creates, 0 conflicts),
  `migrate --apply` (PASS, 0 conflicts), `validate` (PASS, 0 findings across all 6 layers),
  `quality --execute` (PASS_WITH_WARNINGS, expected — no modules enabled to define checks).
- Risks: none identified. `v1`-`v9`/`images/` site content confirmed untouched (no matching paths
  in the migration's file list or in `git status` before commit).

## 2026-09-09 — merge: fast-forward starter-kit-v3.10-migration into main

## Summary

- Owner-authorized fast-forward merge of `starter-kit-v3.10-migration` into `main`
  (`4a2e6b5` -> `ca09f8d`), pushed to `origin/main`.

## Description

- What changed: `main` gained all 81 governance/Starter-Kit files from the migration branch; no
  new merge commit (clean fast-forward, `main` had not moved).
- Why: owner-confirmed next task from the 2026-09-08 session — the migration was validated and
  pushed to a branch, and the owner authorized merging it into `main` this session.
- Validation: `git merge-base --is-ancestor main starter-kit-v3.10-migration` confirmed fast-forward
  eligibility before merging; `git diff` of the merge showed only governance/kit files, 0 matches
  under `v1`-`v9`/`images/`; remote sync independently verified via `git ls-remote --heads origin
  main` matching local `HEAD`.
- Risks: none identified.

## 2026-09-09/15 — docs: resolve Snapshot Contract policy fields and destination sync

## Summary

- Fill in the Snapshot Contract's remaining fields (naming rule, exclusions, verification method,
  checksum requirement, retention policy, restore/rollback procedure) using the real mechanism at
  the owner-supplied destination for `DESKTOP-8JF1MKA`.

## Description

- What changed: `docs/governance/REPOSITORY_HANDOFF_CONFIG.md`'s Snapshot Contract section, no
  longer `TBD` for any field.
- Why: the destination (`E:\WorkSync\Projects\RepoBackups\Craft and Conscious\`) turned out to
  already contain a live clone (`Primary\`) of this repo's own origin — the actual mechanism was
  observed and documented rather than invented, modeled on the same-machine `swarm-defense`
  precedent but adapted where it differs (a synced clone, not versioned export folders).
- Validation: `Primary\` clone synced via `git fetch`/`git pull --ff-only`, confirmed at the same
  `HEAD` as `origin/main` (`git rev-parse` match).
- Risks: none identified. Two legacy folders (`Branch1\`, `Branch2\`) of unknown origin found at
  the same destination — owner decided 2026-09-15 to leave them untouched; not a risk to this
  repo.

## 2026-09-16 — chore: enable 10 Starter Kit governance modules (web_application)

## Summary

- Enable `threat_model`, `security_requirements`, `dependency_risk`, `secret_scan`,
  `license_policy`, `browser_matrix`, `accessibility`, `web_performance`, `seo`, and
  `release_metadata` via the pinned v3.10.0 kit CLI (`module plan` -> `module enable --apply`, one
  at a time in dependency order). Also re-baseline ownership of 5 pre-existing governance docs from
  `starter_kit` to `project` in `.starter-kit/manifest.json`.

## Description

- What changed: 10 new policy docs under `docs/security/` and `docs/operations/`, plus
  `docs/release/RELEASE_EVIDENCE.md` and `.starter-kit/release-manifest.json`. `.starter-kit/
  manifest.json` and `capability-state.json` updated to record all 10 as enabled/configured.
  Ownership of `docs/governance/REPOSITORY_HANDOFF_CONFIG.md` and `docs/project/{STATUS,
  COMMIT_NOTES,CONTEXT,DECISION_LOG}.md` changed from `starter_kit` to `project` in the manifest.
- Why: owner selected these 10 from a read-only review of all 39 optional `web_application`
  modules (8 mechanically blocked by missing repo evidence — no database/service/cloud/CI
  validation contract; the rest filtered to what fits a static HTML site with no backend, build,
  or deployment target). The ownership re-baseline was needed because `validate` flagged those 5
  files as drifted from their template checksum — they were legitimately filled with real facts
  across the 2026-09-08/09/15 sessions, but the manifest was never updated to reflect that, so
  `validate` had been silently `BLOCKED` since 2026-09-08 without any prior session catching it.
- Validation: `module plan`/`module enable --apply` PASS for all 10 (fresh plan ID re-read after
  each apply, since applying one module invalidates plan IDs computed for the rest — each
  module's plan ID hashes the whole repo tree). `validate`: BLOCKED (5 owned_file_drift findings)
  before the ownership fix, PASS (0 findings, all 6 layers) after. `quality --execute`:
  PASS_WITH_WARNINGS (expected — no executable checks configured, same as every prior session).
  `git status` confirmed zero paths under `v1`-`v9`/`images` touched, both before and after.
- Risks: none identified. No CI workflows or live automation were generated — each module enable
  created documentation only.

## 2026-09-17 — docs: fill 10 module policy docs with real content, re-baseline ownership

## Summary

- Fill all 10 module policy docs enabled 2026-09-16 (`docs/security/{threat_model,
  security_requirements,dependency_risk,secret_scan,license_policy}.md`, `docs/operations/
  {BROWSER_MATRIX_POLICY,ACCESSIBILITY_POLICY,WEB_PERFORMANCE_POLICY,SEO_POLICY}.md`,
  `docs/release/RELEASE_EVIDENCE.md`) with real, project-specific content, replacing kit-template
  boilerplate. Re-baseline their ownership from `starter_kit` to `project` in
  `.starter-kit/manifest.json`.

## Description

- What changed: all 10 files above rewritten with facts derived directly from `v9/index.html`
  (zero third-party dependencies, zero secrets, static single-file build, inactive analytics
  placeholder, non-functional "Pretend checkout"/newsletter form, 3 responsive breakpoints,
  existing ARIA/semantic-HTML usage) plus 4 explicit owner decisions: WCAG 2.2 AA accessibility
  target, evergreen-only browser matrix (last 2 versions of Chrome/Firefox/Safari/Edge, no IE11),
  performance-regression handling (track and revisit, not blocking), and confirmation that all site
  imagery/code is original and business-owned (no third-party licenses apply). Real gaps were
  recorded explicitly rather than omitted — no keyboard/focus-order pass or color-contrast
  measurement has ever been run, and several buttons (`.btn`, `.mood-btn`, `.cart-line-qty-btn`)
  lack `:focus-visible` styling.
- Why: owner-confirmed next task carried from the 2026-09-16 session (`HANDOFF_TO_CLAUDE.md`).
- Validation: `starter_kit.py validate` went `BLOCKED` (10 fresh `owned_file_drift` findings — the
  expected consequence of editing `starter_kit`-owned template files) immediately after the doc
  edits, then `PASS` (0 findings, all 6 layers) after the ownership re-baseline, which used the
  kit's own `sha256_file`/`json_text`/`_normalized_manifest_hash` functions to keep the manifest's
  self-referential hash consistent (same method as the 2026-09-16 precedent). `quality --execute`:
  PASS_WITH_WARNINGS (expected — no executable checks configured, same as every prior session).
  `git status --porcelain=v1 --untracked-files=all` confirmed zero paths under `v1`-`v9`/`images/`
  touched.
- Risks: none identified. This session's own accessibility findings (missing `:focus-visible`
  states, no keyboard/contrast verification ever performed) are the owner-confirmed next task.

## 2026-09-17 (later same day) — fix: WCAG 2.2 AA accessibility gaps in v9/index.html

## Summary

- Ran a live headless-Chromium (Playwright) audit of `v9/index.html` against WCAG 2.2 AA:
  keyboard operability/focus order (36 focusable elements), focus visibility, and pixel-sampled
  color contrast (9 real rendered text/background locations). Fixed the 2 real contrast failures
  and 1 real modal-dialog gap the audit found; corrected an earlier unverified assumption about
  missing focus-visible styling that live testing disproved.

## Description

- What changed: `v9/index.html` — `--muted` token `#8c7a69` -> `#7b6b5c` (fixes 3.66:1-4.12:1 ->
  4.56:1-5.12:1 across subtitles/nav-links/footer/product-notes); `.btn-primary` text `#26160b` ->
  `#000` (fixes 4.22:1 -> 5.07:1-11.02:1 across its gradient background); cart dialog
  (`role="dialog" aria-modal="true"`) gained real modal keyboard behavior — focus moves to the
  close button on open, Tab/Shift+Tab is trapped inside the panel while open, Escape closes it and
  returns focus to whichever control opened it. `docs/operations/ACCESSIBILITY_POLICY.md` updated
  to record verified facts in place of the prior session's untested assumption (`.btn`/`.mood-btn`/
  `.cart-line-qty-btn` do receive a visible focus indicator by default; that part of the prior
  entry was wrong).
- Why: owner-confirmed next task from the same-day earlier closeout.
- Validation: live-tested, not just read from CSS — pixel-sampled contrast on 9 real page
  locations (all now pass AA), full 36-element keyboard Tab-order pass (0 issues, 0 elements
  without visible focus), and a dedicated cart-dialog test confirming focus-on-open, forward trap,
  backward wrap, and Escape-plus-focus-return, all via genuine keyboard interaction with 0
  console/page errors. `starter_kit.py validate`: PASS, 0 findings (docs already `project`-owned,
  no new drift). `quality --execute`: PASS_WITH_WARNINGS (expected).
- Risks: none identified. Not yet run: an automated accessibility scanner (axe-core/Lighthouse)
  for broader coverage, and mobile/touch-viewport testing — both recorded as open next-task
  candidates rather than silently skipped.

## 2026-09-18 — fix: 3 Tier 1 issues found by automated axe-core scan

## Summary

- Ran axe-core 4.13.0 (WCAG 2.2 AA tags) against `v9/index.html` in both initial-load and
  cart-open states, per the prior session's owner-confirmed next task. Fixed the 3 real Tier 1
  violations it found; 0 violations remain in either state. This push is tagged `v0.1.1`.

## Description

- What changed: `v9/index.html` — converted the 3 filter `.filter-label` divs to
  `<label for="...">` (Collection/Scent family/Price selects previously had no accessible name);
  removed `aria-hidden="true"` from `.hero-card`, which contained a real, functional "Add to cart"
  button reachable by keyboard but invisible to screen readers; changed `.journal-tag` color to
  `var(--muted)` and `.eyebrow` color to `var(--ink-soft)` (not `--muted` — one of `.eyebrow`'s two
  usage contexts renders against the hero's gradient background, where `--muted` alone still fails
  AA; `--ink-soft` clears 4.5:1 in every context either class appears in).
- Why: owner-confirmed next task from the 2026-09-17 closeout — broader automated coverage beyond
  the manual pixel-sampling/keyboard script that session used.
- Validation: axe-core re-scan after the fixes: 0 violations in both states (was 3 critical/serious
  in the initial-load state, 2 in the cart-open state). Manual spot-check confirmed each `<select>`
  now reports its correct accessible name via `el.labels`, and `.hero-card`'s `aria-hidden`
  attribute is gone. Full-page screenshot confirmed no visual regression. `git status` confirmed
  only `v9/index.html` changed.
- Risks: none identified. Remaining axe "needs manual review" items (mostly a known axe limitation
  with gradient/pseudo-element backgrounds, already cross-checked against the 9 locations verified
  2026-09-17) and 2 items axe cannot detect at all (a `.mood-buttons` `aria-label` technicality; the
  cart dialog's background not being marked `inert` while open) are carried forward as open,
  non-blocking items — not silently dropped.
