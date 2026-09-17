# Dependency Risk

Purpose: Track dependency provenance, vulnerabilities, and update disposition.

Status: configured adapter — zero dependencies exist to track.

## Current State

Confirmed by repository-wide search: there is no `package.json`, `requirements.txt`, `Gemfile`,
`pyproject.toml`, or any other dependency manifest anywhere in this repository. All CSS and
JavaScript in `v1`–`v9` is hand-written and inline inside each version's own `index.html` — no
CDN-hosted library, no vendored copy of third-party code, no web font service (the font stack is
`system-ui, -apple-system, BlinkMacSystemFont, "SF Pro Text", "Segoe UI", sans-serif` — OS-provided
fonts only, no network request).

- Provenance: N/A — nothing to trace.
- Vulnerabilities: N/A — no dependency surface for a scanner (`npm audit`, `pip-audit`, etc.) to
  check.
- Update disposition: N/A — nothing to update.

## Re-Evaluation Trigger

This document must stop reading "no dependencies" the same session any of the following happens:
a JS framework or build tool is introduced, a font/icon CDN is added, an analytics snippet is
wired into the existing `<!-- Analytics placeholder -->` slot, or a real checkout SDK replaces the
current "Pretend checkout" placeholder.

This module does not install scanners or accept external licenses. Record configured commands in
`.starter-kit/validation-contract.json`, manual checks in the same contract, and release evidence in
`.starter-kit/security-evidence.json`.

Release use requires source authority, provenance, license disposition, exception state, and evidence
to pass `starter_kit.py validate --release`.
