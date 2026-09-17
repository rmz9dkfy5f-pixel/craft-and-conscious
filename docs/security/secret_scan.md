# Secret Scan

Purpose: Represent secret scanning as configured commands or manual checks.

Status: configured adapter — manual only, no automated scanner installed.

## Current State

Confirmed by direct inspection: no `.env` file, no credentials file, and no hardcoded API key or
token exists anywhere in `v1`–`v9` or the governance layer as of this entry. There is no CI
configuration that would need to reference a secret, since no CI exists for this repository.

- Configured commands: none. `.starter-kit/validation-contract.json`'s `checks` and
  `manual_checks` are both empty as of this session — no automated secret scanner (gitleaks,
  trufflehog, etc.) is installed.
- Manual check practice: review any new or changed file for hardcoded credentials before push —
  the only practice currently in place, and it is unautomated.

## Re-Evaluation Trigger

Revisit this immediately if a real checkout provider, analytics account, or any other service
requiring an API key is ever integrated (see `security_requirements.md`'s Requirements That Apply
Today) — that would be this site's first credential to actually protect.

This module does not install scanners or accept external licenses. Record configured commands in
`.starter-kit/validation-contract.json`, manual checks in the same contract, and release evidence in
`.starter-kit/security-evidence.json`.

Release use requires source authority, provenance, license disposition, exception state, and evidence
to pass `starter_kit.py validate --release`.
