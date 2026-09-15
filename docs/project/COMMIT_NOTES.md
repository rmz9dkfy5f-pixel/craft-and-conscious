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
