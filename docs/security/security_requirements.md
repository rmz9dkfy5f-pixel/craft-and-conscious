# Security Requirements

Purpose: Map secure-development requirements to verification evidence.

Status: configured adapter — manual requirements, no automated verification tooling installed.

## Requirements That Apply Today

- No secret, credential, API key, or token may ever be committed to this repository. Confirmed as
  of this entry: no `.env`, no credentials file, and no hardcoded key exists anywhere in `v1`–`v9`
  or the governance layer. See `secret_scan.md`.
- No third-party script, stylesheet, font, or library may be added to any `index.html` without
  first updating this file and `dependency_risk.md`. Currently: zero third-party resources are
  loaded by any version of the site.
- HTTPS-only delivery is required once a real deployment target is established. Not yet
  applicable — no deployment target is configured (`PROJECT_CLASSIFICATION.md`:
  `git_backed_with_remote`).
- Any future backend, payment integration, or analytics wiring is this site's *first* real data
  flow and must not ship without this document being updated first:
  - The cart's "Pretend checkout" button (`v9/index.html`) is explicitly a placeholder — its own
    copy says "When you're ready to sell, plug in your real checkout (Shopify, Lemon Squeezy,
    etc.)."
  - The `<!-- Analytics placeholder -->` / `<!-- [Analytics Script Here] -->` comment in the
    `<head>` is inactive — no analytics script is currently loaded.

## Requirements That Do Not Apply Today

Standard secure-development requirements around authentication, session management, server-side
input validation, and authorization do not apply — there is no backend, no login, and no server
that receives user input (see `threat_model.md`).

## Verification Evidence

None automated. `.starter-kit/validation-contract.json` has no `checks` or `manual_checks` entries
as of this session. The only current practice is manual review of any new/changed file before
push, per `docs/governance/REPOSITORY_HANDOFF_CONFIG.md`'s Validation Contract (no install/test/
build/lint tooling exists to automate this against).

This module does not install scanners or accept external licenses. Record configured commands in
`.starter-kit/validation-contract.json`, manual checks in the same contract, and release evidence in
`.starter-kit/security-evidence.json`.

Release use requires source authority, provenance, license disposition, exception state, and evidence
to pass `starter_kit.py validate --release`.
