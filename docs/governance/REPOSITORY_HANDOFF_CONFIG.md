# Repository Handoff Configuration

Project-local handoff/closeout configuration. Fill in only real, confirmed values — never
placeholder paths or commands presented as facts. For any section that does not apply given this
repository's `PROJECT_CLASSIFICATION.md` entry, write `N/A — <reason>` instead of deleting the
section or inventing a value.

Store operational coordinates here, never credentials. If this repository already has equivalent
configuration in `AGENTS.md`, deployment docs, or another canonical file, reference it rather than
duplicate it.

## Repository Identity

- Project name: craft-and-conscious
- Repository root: `E:\Projects\GitHub\craft-and-conscious`
- Canonical remote: `https://github.com/rmz9dkfy5f-pixel/craft-and-conscious.git`
- Default branch: main
- Canonical handoff file: N/A — no repo-local `AGENT_HANDOFF.md`/equivalent exists yet; the
  Starter Kit template set does not ship one. `docs/project/CONTEXT.md` and `DECISION_LOG.md` are
  the nearest repo-local continuity records. AntBrainOS vault continuity lives at
  `03_PROJECTS/Active/Craft_and_Conscious_Website/`.

## Validation Contract

- Install command: N/A — no package manager or dependency file (no `package.json`,
  `pyproject.toml`, etc.); pure static HTML/CSS.
- Focused test commands: N/A — no test tooling.
- Full test command: N/A — no test tooling.
- Lint/type-check commands: N/A — none configured.
- Production build command: N/A — no build step; `index.html` files are served as-is.
- Runtime smoke test: manual — open `v9/index.html` in a browser.
- Manual or device checks: manual — visual check of `v9/index.html` after any change to site
  content.

## Snapshot Contract

Applies — this repository is `git_backed_with_remote` per `PROJECT_CLASSIFICATION.md`. Destination
for `DESKTOP-8JF1MKA` confirmed by the owner 2026-09-09 (see table below). Fields below resolved
2026-09-09 from the actual, observed mechanism at that destination, modeled on the same-machine
`swarm-defense` precedent (`E:\Projects\GitHub\swarm-defense\docs\governance\
REPOSITORY_HANDOFF_CONFIG.md`) but adapted to this repo's own mechanism, which differs.

- Snapshot required: yes.
- Naming rule: N/A — the mechanism is a persistent full clone (`Primary\`, see table below) kept
  current via `git fetch`/`git pull`, not discrete timestamped or version-labeled export folders.
  This differs from `swarm-defense`'s `commit-snapshots\v<version>__<slug>__commit-<sha>\`
  convention on this same machine — that convention does not apply here.
- Exclusions: none beyond the repo's own `.gitignore` — a live clone naturally excludes ignored/
  untracked files; there is no separate export step that needs its own exclusion list.
- Verification method: compare `Primary\`'s `git rev-parse main` (or `git log -1`) against the
  canonical remote's `main` (`git ls-remote origin main`, or the live repo's own `HEAD`) — "clone
  HEAD equals canonical remote HEAD" is the freshness check for a live-clone snapshot. Last
  verified 2026-09-09: both at `ca09f8db9ce8eeb0a4f79f7486b3c9a1a6937962`.
- Checksum requirement: not applicable — git's own content-addressed object model (SHA-1 object
  hashes) is the integrity guarantee for a clone; there is no separate export artifact requiring a
  checksum.
- Retention policy: not formally documented; kept indefinitely by convention, matching the
  `swarm-defense` precedent on this machine. This is an open policy choice the owner could tighten
  later — not a fact gap.
- Restore/rollback procedure: two layers, matching the `swarm-defense` pattern —
  1. **Repo/source rollback** (in the live repo itself): `git log --oneline`, `git tag --list`,
     `git checkout <commit-or-tag>`, `git revert <bad-commit>`.
  2. **Full-fidelity disaster recovery**: if the GitHub remote itself is lost or corrupted, the
     `Primary\` clone (kept current per the verification method above) is a complete independent
     copy of the full git history and can be re-pushed to a new remote. No scripted restore command
     exists yet — manual only, same as `swarm-defense`'s own documented state.

### Snapshot Destination by Machine

Only relevant if snapshots are machine-path-dependent (e.g. an external backup drive). Detect the
current machine before resolving a destination:

```bash
scutil --get ComputerName 2>/dev/null || hostname
```

| Machine | Detection | Snapshot destination | Notes |
|---|---|---|---|
| DESKTOP-8JF1MKA | `hostname` = `DESKTOP-8JF1MKA` | `E:\WorkSync\Projects\RepoBackups\Craft and Conscious\` | Confirmed by owner 2026-09-09; this is the only machine this repo has been worked on from as of 2026-09-08. Path contains a `Primary\` subfolder that is itself a full clone of this repo's origin remote (confirmed 2026-09-09: `git remote -v` matches this repo's canonical remote exactly), synced 2026-09-09 via `git fetch`/`git pull --ff-only` to `main` = `ca09f8d`, matching the canonical remote. Also contains `Branch1\` and `Branch2\` subfolders, each holding a partial `v1\` only — file timestamps (2026-05-04) predate this repo's Git history (initial commit 2026-09-08), so these are pre-Git legacy folders of unknown origin, not current Git branches; disposition (keep/archive/delete) is an open owner decision, not yet made — see `docs/project/DECISION_LOG.md` for the outcome once decided. `Primary\v7\` exists but is empty (no tracked or untracked files) — a candidate, unconfirmed explanation for why `v7` is missing from the live site's version sequence. |

If the current machine does not match any row above, or more than one row could plausibly match,
stop and ask before picking a destination — do not guess or infer a path pattern.

## Deployment Contract

*(Updated 2026-09-23 — first real deploy target, on a non-`main` branch.)* `main` itself still has
no deployment target. `design/olive-atelier` does, as of 2026-09-22/23 — a design-exploration
branch deployed live per the same pattern established in the `Hair-by-Alexy` repo (`design/*`
branches, each on its own dedicated VPS subdomain, kept unmerged long-term). See
`docs/project/DECISION_LOG.md`'s 2026-09-22/23 entry for the full reasoning.

### Deploy Targets

| Target name | Scope/trigger | Deployment root | Deploy mechanism | Release marker |
|---|---|---|---|---|
| olive-atelier | branch `design/olive-atelier` | `/var/www/craft-and-conscious-olive-atelier/` on the IONOS VPS (`74.208.9.49`, see `10_INFRASTRUCTURE/Homelab/Ionis_VPS_Reference.md`) | Manual: `scp` the built `v10/index.html` + `v10/images/` to the deployment root over SSH (`~/.ssh/ionis_vps`); no CI/automation exists yet | `https://olive-atelier.craftandconscious.com/RELEASE.txt` |

Nginx vhost: `/etc/nginx/sites-available/olive-atelier.craftandconscious.com` (HTTPS via Let's
Encrypt, `certbot --nginx --redirect`, cert expires 2026-12-22, auto-renews). No build step — the
deploy mechanism is a direct file copy, matching this repo's own no-build-tooling convention.

## Safety Boundaries

- Protected paths: `v1/`, `v2/`, `v3/`, `v4/`, `v5/`, `v6/`, `v8/`, `v9/`, `images/` (site content —
  governance/tooling changes must never modify these).
- Secret-bearing files: none known — no `.env`, credentials, or config files with secrets exist in
  this repo.
- Prohibited actions: force-push, history rewrite, merge without explicit owner approval (see
  Commit/push authorization rule).
- Commit/push authorization rule: commits/pushes to a feature/migration branch may proceed under
  an explicitly authorized workflow (e.g. the session-end super prompt's Authorization Envelope);
  merging a branch into `main` always requires separate, explicit owner approval — never inferred
  from push authorization alone.
- Tag/release authorization rule: same as commit/push — requires explicit authorization per
  session; no standing tag-naming convention established yet beyond the existing `vX.Y.Z` pattern
  (`v0.1.0` exists on `main`).
- Deploy/merge authorization rule: both require separate, explicit owner authorization; never
  implied by a push or by running this or any other closeout workflow.
