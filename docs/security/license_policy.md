# License Policy

Purpose: Govern allowed, denied, unknown, restricted, and exception license states.

Status: configured adapter — no scanner installed; disposition confirmed directly with the owner.

## Current State (confirmed with owner, 2026-09-17)

- **Allowed / in use:** all site imagery (`v9/images/logo-craft-conscious.jpeg`,
  `candle-19.jpeg`, `candle-23.jpeg`, `candle-sandalwood-vanilla.jpeg`) is original,
  business-owned photography and branding — not licensed or sourced from any third party. All
  HTML/CSS/JS across `v1`–`v9` is hand-authored for this project, not copied from a licensed
  template, theme, or library.
- **Denied:** none currently in use.
- **Unknown:** none currently — every asset's provenance is confirmed above.
- **Restricted:** none currently in use — no third-party font service, icon library, or stock
  photography is loaded by any current version.
- **Exception state:** none.

## Re-Evaluation Trigger

Any future addition of a third-party font (e.g. Google Fonts), icon library, stock photo, or code
library must be recorded here with its actual license terms before it is merged — this policy
currently reads "all original" and must not silently drift out of date.

This module does not install scanners or accept external licenses. Record configured commands in
`.starter-kit/validation-contract.json`, manual checks in the same contract, and release evidence in
`.starter-kit/security-evidence.json`.

Release use requires source authority, provenance, license disposition, exception state, and evidence
to pass `starter_kit.py validate --release`.
