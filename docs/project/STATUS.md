# Status

## Current State

Static website, 8 versioned iterations (`v1`-`v6`, `v8`, `v9`; no `v7`), each a standalone
`index.html`; `v9` (current) also has `images/`. No build system, no backend, no CI. **A real
production deployment exists** (`craftandconscious.com`/`www.craftandconscious.com`, discovered
2026-09-23 — see Broken/Unknown below); it predates this repo and is currently stale. Separately,
branch `design/olive-atelier` has its own confirmed, current deployment
(`olive-atelier.craftandconscious.com`). AntBrainOS Project Starter Kit v3.10.0 (`web_application`
profile) adopted and
merged into `main` (2026-09-09). 10 optional governance modules are enabled (since 2026-09-16):
`threat_model`, `security_requirements`, `dependency_risk`, `secret_scan`, `license_policy`,
`browser_matrix`, `accessibility`, `web_performance`, `seo`, `release_metadata`. As of 2026-09-17,
all 10 modules' policy docs hold real project-specific content (previously kit-template
boilerplate): accessibility target WCAG 2.2 AA, browser support last-2-versions evergreen (no IE11),
zero third-party dependencies/secrets confirmed, all imagery/code confirmed original/business-owned.
The Snapshot Contract for `DESKTOP-8JF1MKA` is fully resolved and its `Primary\` clone kept in sync.

## Last Updated

2026-09-23 — **discovered an untracked, stale production deployment.** `craftandconscious.com`/
`www.craftandconscious.com` resolve to `74.208.9.49` (the same IONOS VPS as `Hair-by-Alexy`/
`design/olive-atelier`) and serve HTTP 200 from `nginx`, with `Last-Modified: Wed, 26 Nov 2025` —
predating this repo's entire Git history (initial commit 2026-09-08). Every session since then had
stated "no deployment target" for `main` without ever actually checking; that classification was
wrong the whole time. The deployed content is confirmed stale (missing every accessibility fix
shipped since 2026-09-17), has no `RELEASE.txt`, and its deploy mechanism/root are unconfirmed.
Owner decided to document this now (`docs/governance/{PROJECT_CLASSIFICATION,
REPOSITORY_HANDOFF_CONFIG}.md`, `DECISION_LOG.md`) rather than deploy or investigate further this
session — see `DECISION_LOG.md`'s 2026-09-23 entry. Also fixed the owner-confirmed next task from
2026-09-22: the mobile nav toggle (`.nav-toggle`) had zero JavaScript wiring — primary navigation
and the cart button were both completely unreachable below the 768px breakpoint. Fixed as a
disclosure widget (`aria-expanded`/`aria-controls`, opens on tap, closes on nav-link selection or
`Escape` with focus return); live-verified via headless Chromium with iPhone 13 emulation and
manual resizes through all 3 documented breakpoints. axe-core re-scan (WCAG 2.2 AA): 0 violations
in 3 states never scanned before (mobile initial-load, mobile nav-open, mobile cart-open).
`.cart-line-qty-btn` (22×22) measured against the WCAG 2.2 SC 2.5.8 spacing exception (45px
center-to-center between buttons) rather than resized, since it genuinely qualifies — confirmed,
not assumed. Not yet committed.

2026-09-22 — fixed the 2 remaining axe-noted items from the 2026-09-18 scan: added `role="group"`
to `.mood-buttons` (fixes an `aria-label`-on-non-interactive-`<div>` technicality), and marked the
cart dialog's background (`.page`) `inert` while the dialog is open (toggled from the existing
`openCart()`/`closeCart()` functions) so it's excluded from the accessibility tree and from pointer/
keyboard interaction, not just the Tab trap. Verified live via headless-Chromium (Playwright,
scratch-directory-only dependency): `.mood-buttons` reports `role="group"`; opening the cart applies
`inert` to `.page`, blocks a background nav-link click, and confirms the background sits inside an
inert subtree; closing the cart removes `inert`. Re-ran an axe-core 4.13.0 scan (WCAG 2.2 AA tags):
0 violations in both initial-load and cart-open states. Committed `900a481`, pushed,
remote-verified; `Primary\` snapshot synced to `900a481`, verified identical.

2026-09-18 — ran an automated axe-core 4.13.0 scan (WCAG 2.2 AA tags) against `v9/index.html` in
both its initial-load and cart-open states, following up on the 2026-09-17 manual pass. Found and
fixed 3 real Tier 1 issues the manual pass hadn't covered: the 3 filter `<select>` elements had no
accessible name (converted their `.filter-label` divs to `<label for="...">`); `.hero-card` was
`aria-hidden="true"` while containing a real, functional "Add to cart" button (removed the
`aria-hidden`, confirmed not required by the shared `.reveal` animation class); and `.eyebrow`/
`.journal-tag` text failed AA contrast with their own separate colors, distinct from the `--muted`
token fixed 2026-09-17 (reassigned to existing `--ink-soft`/`--muted` tokens respectively, verified
per actual rendered background context — `.eyebrow` needed `--ink-soft` specifically since one of
its two usage contexts renders against the hero gradient, not a guaranteed-white card, where
`--muted` alone would still have failed). Re-scan after the fixes: 0 violations in both states (was
3/2). This push will be tagged `v0.1.1` (applied in the session-end super prompt's Section 7) — the
first tagged release since `v0.1.0` and the first to mark an actual site-content change rather than
governance-only work.

2026-09-17 (later same day) — ran a live headless-Chromium (Playwright) audit of `v9/index.html`
against the WCAG 2.2 AA target and fixed what it found: `--muted` text and `.btn-primary` text
both measured below the 4.5:1 AA threshold at real rendered locations (pixel-sampled, not just
computed from CSS hex values) — corrected to `#7b6b5c` and `#000` respectively, re-verified at
4.56:1–11.02:1 across every sampled location. The cart dialog (`role="dialog" aria-modal="true"`)
had no real modal keyboard behavior — a keyboard user could Tab straight through it into the
obscured page behind it; fixed with focus-on-open, a real Tab/Shift+Tab trap, and Escape-to-close
with focus return, all verified live. Also corrected an earlier, unverified assumption in
`ACCESSIBILITY_POLICY.md`: `.btn`/`.mood-btn`/`.cart-line-qty-btn` do *not* lack visible focus —
the browser's default outline renders for all of them; that was established by actually testing
rather than reading the CSS.

## Working

- Site content (`v1`-`v9`, `images/`) — `v9/index.html` was deliberately modified this session
  (the first session to touch site content, by design — a real accessibility fix, not governance
  tooling); `v1`-`v8`/`images/` remain untouched, confirmed via `git status`.
- `validate` and `quality --execute` both pass against the installed Starter Kit (`quality`'s only
  finding is the expected "no executable quality checks" warning, since this repo has no toolchain
  to configure one against).
- Snapshot Contract for `DESKTOP-8JF1MKA` fully resolved; `Primary\` clone at the confirmed
  destination verified in sync with `origin/main`.
- Accessibility: keyboard operability, focus order, focus visibility, and color contrast are now
  verified against WCAG 2.2 AA for `v9` on both desktop and mobile viewports (390×664 iPhone 13
  emulation, plus all 3 documented breakpoints), including a working mobile navigation menu — see
  `docs/operations/ACCESSIBILITY_POLICY.md`.

## Broken / Unknown

- **`main`'s production deployment (`craftandconscious.com`) is stale and untracked** — discovered
  2026-09-23. Deploy mechanism, deployment root, and who/what manages the file are all unconfirmed;
  no `RELEASE.txt` exists. Owner chose to document only, not deploy or investigate further, this
  session — see `docs/governance/REPOSITORY_HANDOFF_CONFIG.md`'s Deployment Contract. This also
  reframes (does not resolve) the SEO/web-performance modules' "no deployment target" open items —
  a target does exist, it's just stale and unmanaged.
- `Validation Contract` in `docs/governance/REPOSITORY_HANDOFF_CONFIG.md` has no real
  install/test/build commands to record — this repo has no toolchain (no `package.json`, no build
  step) to discover them from.
- `MIGRATION_REPORT.md` at the repo root is still the unfilled template (`Status: Not started`)
  despite the migration it describes being complete — a known, non-blocking documentation gap, not
  yet fixed.
- Origin of `Branch1\`/`Branch2\` legacy folders at the snapshot destination is unknown; owner
  decided 2026-09-15 to leave them as-is.

## Next Actions

- Owner: decide what to do about the stale, untracked `main` production deployment — options
  include SSH-investigating the VPS's nginx config/deploy root, redeploying current `main`, or
  leaving it as-is pending further decision.
- Optional: fill in or explicitly retire the stale `MIGRATION_REPORT.md` template.
- Optional: delete the now-redundant, fully-merged `starter-kit-v3.10-migration` branch.
