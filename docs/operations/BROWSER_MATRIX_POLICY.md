# Browser Matrix Policy

This module (`browser_matrix`) generates this policy. It runs no browser, launches no test, and
assumes no testing tool: the matrix below is this project's own statement, verified with whatever
tooling it already uses or chooses to adopt.

## Supported matrix

- The browsers this project supports, each with its supported version or version window (e.g.
  "last 2 major versions", not just a name with no bound).
- The devices and viewports this project supports - phone, tablet, desktop breakpoints - stated as
  ranges a reviewer can check a screenshot against, not implied by a CSS framework's defaults.
- The operating systems this project's browser/device combinations are verified on, where that
  differs from the browser vendor's own default platform.

## Verification practice

- Behavior is verified against every entry in the matrix above, not against whichever browser a
  developer happens to be using - a bug that only reproduces in one matrix entry is still a bug in
  that entry.
- Verification may be manual or automated; what matters is that it runs against the stated matrix,
  on a stated cadence relative to release, not once at project start and never again.
- A change that narrows the matrix (a browser dropped) is itself a decision, recorded here with a
  reason, not a silent contraction of what "supported" means.

## Known gaps

- Any browser, device, or viewport combination this project deliberately does not support is
  stated here, with the reason - an unstated gap reads as an oversight; a stated one is a decision.

## What this module deliberately does not do

- Does not launch, drive, or configure a browser, and does not assume a cross-browser testing
  tool, device lab, or CI provider.
- Does not run any check itself - the matrix above is what this project's own verification
  practice, whatever form it takes, is checked against.
- Does not define a new evidence document or finding code.
