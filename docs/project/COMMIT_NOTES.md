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
