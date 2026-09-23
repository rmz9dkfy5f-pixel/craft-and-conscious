# Status

## Current State

Static website, 8 versioned iterations (`v1`-`v6`, `v8`, `v9`; no `v7`), each a standalone
`index.html`; `v9` also has `images/`. No build system, no backend, no CI. `main` has no confirmed
deployment target. AntBrainOS Project Starter Kit v3.10.0 (`web_application` profile) adopted and
merged into `main` (2026-09-09). 10 optional governance modules are enabled (since 2026-09-16):
`threat_model`, `security_requirements`, `dependency_risk`, `secret_scan`, `license_policy`,
`browser_matrix`, `accessibility`, `web_performance`, `seo`, `release_metadata`. As of 2026-09-17,
all 10 modules' policy docs hold real project-specific content: accessibility target WCAG 2.2 AA,
browser support last-2-versions evergreen (no IE11), zero third-party dependencies/secrets
confirmed, all imagery/code confirmed original/business-owned. The Snapshot Contract for
`DESKTOP-8JF1MKA` is fully resolved and its `Primary\` clone kept in sync with `main`.

**New as of this branch (`design/olive-atelier`, off `main` @ `900a481`):** a tenth site version,
`v10/`, is a from-scratch design-exploration mockup (distinct visual direction from `v1`-`v9`) built
against a supplied reference screenshot per this vault's
`claude-code-visual-mockup-website-execution-plan.md` two-phase workflow (Phase 1 plan approved,
Phase 2 implemented). This is the same "unmerged, long-lived showcase branch on its own VPS
subdomain" pattern already established by the `Hair-by-Alexy` repo's three `design/*` branches —
matching that precedent, `v1`-`v9` are untouched and this branch is not intended to merge into
`main`.

## Last Updated

2026-09-22/23 — built `v10/index.html` (self-contained, inline CSS, no build step — matching this
repo's per-version convention) plus `v10/images/` (14 real photos, Pexels-sourced, `CREDITS.md`
logs each source URL) on new branch `design/olive-atelier`. Live-verified via headless Chromium:
no console errors, no broken images/requests, no horizontal scroll at mobile width, demo
cart/wishlist/mobile-nav all functional, `inert` correctly applied to the page behind the open cart
dialog (same pattern as `v9`'s own 2026-09-22 fix). Deployed live to
`https://olive-atelier.craftandconscious.com` on the existing IONOS VPS (owner set DNS; this
session added the Nginx vhost, issued a Let's Encrypt cert via `certbot --nginx --redirect`, copied
`v10/` to `/var/www/craft-and-conscious-olive-atelier`, and wrote `RELEASE.txt`) — owner-authorized
this session. No git tag for this push, matching the `Hair-by-Alexy design/*` precedent (design
branches don't receive a version tag) and this repo's own standing rule that tags mark real
`main`-branch site releases only. **Confirmed final deployed commit: `f88ec2909560136a822354458d59660d6df76573`**
(`design/olive-atelier`) — `RELEASE.txt` re-verified against this exact commit after the push
(build-input SHA-256 of `v10/index.html` matches local and deployed byte-for-byte), superseding an
earlier same-session deploy of the pre-commit working tree.

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
  verified against WCAG 2.2 AA for `v9` via a live scripted pass (not yet a full automated
  scanner) — see `docs/operations/ACCESSIBILITY_POLICY.md`.

## Broken / Unknown

- No deployment target has been confirmed for this repo — this also blocks the SEO module's
  indexability requirements (`robots.txt`/sitemap/OG tags) and the web-performance module's field
  measurement, both recorded as open items in their respective policy docs.
- Mobile/touch-viewport accessibility (tap target sizing, screen-reader gestures) is untested —
  this session's pass used a 1280×900 desktop viewport only.
- `Validation Contract` in `docs/governance/REPOSITORY_HANDOFF_CONFIG.md` has no real
  install/test/build commands to record — this repo has no toolchain (no `package.json`, no build
  step) to discover them from.
- `MIGRATION_REPORT.md` at the repo root is still the unfilled template (`Status: Not started`)
  despite the migration it describes being complete — a known, non-blocking documentation gap, not
  yet fixed.
- Origin of `Branch1\`/`Branch2\` legacy folders at the snapshot destination is unknown; owner
  decided 2026-09-15 to leave them as-is.

## Next Actions

- Owner: pick specific candle product photography for `v10` (current photos are stock/placeholder,
  logged in `v10/images/CREDITS.md`).
- Optional: test mobile/touch-viewport accessibility on `main`'s `v9` (still untested).
- Owner: decide whether/when to establish a deployment target for `main` itself — several module
  docs are blocked on this; unrelated to `design/olive-atelier`'s own new deploy target.
- Optional: fill in or explicitly retire the stale `MIGRATION_REPORT.md` template.
- Optional: delete the now-redundant, fully-merged `starter-kit-v3.10-migration` branch.
- Optional: add a `### Deploy Targets` row for `olive-atelier.craftandconscious.com` to
  `docs/governance/REPOSITORY_HANDOFF_CONFIG.md`'s Deployment Contract so `REPO_VPS_DEPLOY.md` can
  resolve it automatically on a future redeploy (deployed manually this session; not yet formalized
  in that table).
