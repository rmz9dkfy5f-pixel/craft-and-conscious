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

Applies — this repository is `git_backed_with_remote` per `PROJECT_CLASSIFICATION.md`. **Not yet
resolved as of 2026-09-08: no machine has a configured snapshot destination below.** This is a
genuine open item requiring owner input, not an oversight — see
`09_PROMPTS/Claude_Code_Prompts/04_Prompts/repo_push_handoff_snapshot_tag_prompt_snapshot_naming_refined_session_end_super_prompt.md`
Section 7 step 5, which stops rather than guessing a path when this table is unresolved.

- Snapshot required: TBD — owner to decide.
- Naming rule: TBD
- Exclusions: TBD
- Verification method: TBD
- Checksum requirement: TBD
- Retention policy: TBD
- Restore/rollback procedure: TBD

### Snapshot Destination by Machine

Only relevant if snapshots are machine-path-dependent (e.g. an external backup drive). Detect the
current machine before resolving a destination:

```bash
scutil --get ComputerName 2>/dev/null || hostname
```

| Machine | Detection | Snapshot destination | Notes |
|---|---|---|---|
| DESKTOP-8JF1MKA | `hostname` = `DESKTOP-8JF1MKA` | TBD — not yet configured | 5950X Workstation; this is the only machine this repo has been worked on from as of 2026-09-08. |

If the current machine does not match any row above, or more than one row could plausibly match,
stop and ask before picking a destination — do not guess or infer a path pattern.

## Deployment Contract

N/A — no deployment target. Classification is `git_backed_with_remote`, not `git_backed_with_deployment`;
no deploy host, CI, or release pipeline exists for this repo as of 2026-09-08.

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
