# Accessibility Policy

This module (`accessibility`) generates this policy. It runs no scanner and assumes no tool: the
conformance target below is this project's own commitment, checked with whatever tooling it
already uses or chooses to adopt.

## Conformance target

- The WCAG version and level this project targets (e.g. WCAG 2.2 AA), stated explicitly - "we care
  about accessibility" with no stated target is not a target a check can pass or fail against.

## What is checked

- Semantic HTML and correct ARIA usage where semantic HTML alone is insufficient.
- Keyboard operability: every interactive element reachable and operable without a mouse, in a
  focus order that matches visual/reading order.
- Focus visibility: a keyboard user can always see where focus currently is.
- Color contrast at the stated conformance level, for text and for meaningful non-text UI.
- Meaningful alternative text for non-decorative images, and correct labeling for form controls.

## Verification practice

- An automated scan catches a meaningful subset of the checks above but not all of them - keyboard
  operability and focus order specifically require a manual pass, not just a tool's PASS result.
- Verification runs on a stated cadence relative to release, not once at project start.

## Known exceptions

- Any interface or interaction this project does not currently meet its stated conformance target
  for is listed here, with the reason and, where applicable, a remediation plan - an unstated gap
  reads as an oversight; a stated one is a decision.

## What this module deliberately does not do

- Does not run a scanner, screen reader, or any other accessibility tool, and does not assume one.
- Does not guarantee legal conformance in any jurisdiction - it states and requires verification of
  a technical target, which is necessary but not sufficient for legal compliance.
- Does not define a new evidence document or finding code.
