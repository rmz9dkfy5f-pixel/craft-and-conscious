# Project Classification

Determine this before any other kickoff decision. It governs which sections of
`REPOSITORY_HANDOFF_CONFIG.md` apply and how the Model Selection Gate and Agent Run Contract get
used for this project.

## Categories

The labels below are the human-readable form of this project's classification. The
canonical machine-readable value lives in `.starter-kit/manifest.json`
(`project_classification`, e.g. `git_backed_with_deployment`); validation normalizes
case, spacing, and hyphens on both sides before comparing them, so writing the prose
label verbatim (e.g. "Git-backed with deployment") is equivalent to writing the raw
token.

- **Vault-only** — lives inside a knowledge base or note vault with no Git history of its own
  (snapshot/sync governed instead of commit governed).
- **Local non-Git** — a local folder or working copy with no version control at all.
- **Git-backed** — has Git history, no configured remote.
- **Git-backed with remote** — has Git history and pushes to a remote (GitHub, GitLab, etc.), but
  nothing is deployed from it.
- **Git-backed with deployment** — has Git history, a remote, and a real deployment target (VPS,
  hosting platform, app store, package registry, etc.).

## This Project

- **Classification:** git_backed_with_deployment
- **Confirmed by:** manual discovery, 2026-09-23 — a read-only `curl`/DNS check found
  `craftandconscious.com`/`www.craftandconscious.com` resolving to `74.208.9.49` (the same IONOS
  VPS documented for `Hair-by-Alexy` and `design/olive-atelier`) and serving HTTP 200 from `nginx`.
  **This corrects a stale classification that every session since 2026-09-08 carried forward
  unverified** — `.starter-kit/manifest.json`'s `project_classification` and
  `.starter-kit/project-profile.json` still say `git_backed_with_remote`/no deployment and have
  not yet been re-run through `starter_kit.py inspect` to reflect this; do that before trusting
  those two files' deployment-related fields again.
- **Confirmed on:** 2026-09-23
- **Evidence:** `curl -I https://craftandconscious.com/` → `HTTP/1.1 200 OK`, `Server: nginx`,
  `Last-Modified: Wed, 26 Nov 2025 10:18:17 GMT`. DNS resolves to `74.208.9.49`. See
  `docs/governance/REPOSITORY_HANDOFF_CONFIG.md`'s Deployment Contract for the full finding — the
  served content is stale (predates this repo's entire Git history, and is missing every
  accessibility fix shipped since 2026-09-17) and has no `RELEASE.txt` or any other tracked
  release marker.

Never infer a classification from assumption or convenience. If unconfirmed, leave every field
above as unknown in `.starter-kit/project-profile.json` rather than guessing. (This entry itself
is exactly the failure mode that rule exists to prevent — the classification stood as
`git_backed_with_remote` for over two weeks and eleven sessions before anyone actually checked.)

**Branch-scoped note (2026-09-23, from the `design/olive-atelier` branch, still accurate):**
`design/olive-atelier` has its own, separate, independent deploy target
(`docs/governance/REPOSITORY_HANDOFF_CONFIG.md`'s Deploy Targets table) — distinct from `main`'s
own now-confirmed deployment discovered the same day. Both are real; neither implies the other.

## What Each Classification Implies

| Classification | `REPOSITORY_HANDOFF_CONFIG.md` sections that apply |
|---|---|
| Vault-only | None — use the vault's own snapshot/session-lifecycle SOPs instead, if any exist. |
| Local non-Git | Repository Identity (partial), Validation Contract only. |
| Git-backed | Repository Identity, Validation Contract, Snapshot Contract. |
| Git-backed with remote | Adds Safety Boundaries (push/tag authorization rules). |
| Git-backed with deployment | Adds the full Deployment Contract. |

Re-check this classification if the project's Git/remote/deployment status changes materially
(e.g. a local prototype gets its first remote, or a repo gets its first real deployment target) —
do not leave a stale classification in place.
