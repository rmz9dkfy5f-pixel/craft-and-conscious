# Threat Model

Purpose: Track assets, trust boundaries, threats, mitigations, and residual risk.

Status: configured adapter — no automated scanner installed; this document is the manual threat
model for a static, dependency-free, backend-free site.

## Assets

- Site content: the HTML/CSS/JS in each of `v1`–`v9` (each a standalone `index.html`) and the
  images in `v9/images/`.
- The GitHub repository itself (`rmz9dkfy5f-pixel/craft-and-conscious`) — its source and full
  history.
- Push/write access to `origin` (the owner's GitHub credentials) — not this site's data, but the
  thing that controls what the site ever says.

**No user data is collected or stored by the site itself.** The newsletter form
(`#newsletter-form` in `v9/index.html`) calls `event.preventDefault()` and never submits
anywhere — no request is sent, no address is stored. The cart is explicitly a client-side-only
demo (labelled "Pretend checkout" in the UI) that never contacts a payment processor and is lost
on page reload. There is no cookie, no `localStorage`/`sessionStorage` write, no server, and no
database anywhere in this build.

## Trust Boundaries

- The browser is the only runtime — there is no server round-trip for any user action.
- GitHub Pages/hosting (if ever configured) would only ever serve static files as-is; no
  server-side code runs.
- No deployment target is currently configured at all (see
  `docs/governance/PROJECT_CLASSIFICATION.md` — classification `git_backed_with_remote`), so there
  is currently no live boundary between this repo and the public internet.

## Threats Considered

- **Malicious or mistaken edit to site content** (e.g. a bad merge shipping unintended copy or
  script): mitigated by the standing rule that every push/merge to `main` requires explicit owner
  authorization (`docs/governance/REPOSITORY_HANDOFF_CONFIG.md` Safety Boundaries) and by there
  being no CI/CD able to auto-deploy a change.
- **Compromise of the GitHub account used to push**: out of this doc's scope (account-level, not
  code-level) — standard GitHub account hygiene (2FA, credential rotation) applies but is not
  tracked here.
- **Supply-chain risk via a third-party dependency**: not currently applicable — there is no
  `package.json` or any dependency manifest anywhere in this repo; zero third-party JS/CSS is
  loaded (no CDN scripts, no web fonts — the font stack is `system-ui` and OS defaults only). See
  `dependency_risk.md`.
- **Client-side injection (XSS)**: no user input is ever transmitted to a server, so there is no
  server-side injection surface. Noted for future attention: the cart-rendering code in
  `v9/index.html`'s inline `<script>` builds cart-line HTML via `innerHTML` template literals
  (`cartBody`/`line.innerHTML`), but the values it interpolates (`item.name`, `item.price`,
  `item.qty`) come only from the hardcoded `data-product-*` attributes already in this file, not
  from any user-controllable input — not exploitable today, but would become a real risk the
  moment product data is ever sourced dynamically (a CMS, a query string, etc.).

## Residual Risk

Low. The current build's static, dependency-free, backend-free nature closes off most standard web
threat classes by construction. The main residual risk is process-level (who can push to `main`),
not code-level.

## Re-Evaluation Trigger

This model must be revisited the moment any of the following becomes real: a live deployment
target, a real checkout/payment integration (replacing the current "Pretend checkout" placeholder),
an analytics script (there is an inactive `<!-- Analytics placeholder -->` comment in
`v9/index.html`'s `<head>`), or any first real dependency.

This module does not install scanners or accept external licenses. Record configured commands in
`.starter-kit/validation-contract.json`, manual checks in the same contract, and release evidence in
`.starter-kit/security-evidence.json`.

Release use requires source authority, provenance, license disposition, exception state, and evidence
to pass `starter_kit.py validate --release`.
