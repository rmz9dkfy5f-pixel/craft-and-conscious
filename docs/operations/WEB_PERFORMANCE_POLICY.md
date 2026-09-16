# Web Performance Policy

This module (`web_performance`) generates this policy. It runs no measurement and assumes no
tool: the budget below is what this project's users actually experience, measured with whatever
tooling this project already uses or chooses to adopt.

## Performance budget

- Load and interactivity indicators a user would recognize as "fast" or "slow" - largest
  contentful paint, interaction-to-next-paint, cumulative layout shift, time to first byte -
  each with a stated numeric budget, not left as "should be fast."
- A stated budget for shipped asset size, where that is the practical lever this project has over
  the indicators above.

## Measurement practice

- Measured at a point that reflects what a user experiences - a real or realistic network and
  device condition, not a developer's local machine on a fast connection and empty cache.
- Both lab measurement (consistent, repeatable, good for catching regressions) and field
  measurement (real users, real conditions, good for knowing what actually happened) have a place;
  which this project uses, and why, is stated rather than left implicit.
- Measured on a stated cadence relative to release, not once at project start.

## Regression handling

- What happens when a budget is exceeded is stated in advance: block the release, waive with a
  recorded reason, or track and revisit - whichever this project chooses, chosen before the
  regression exists rather than decided in the moment it does.

## What this module deliberately does not do

- Does not run a measurement tool, and does not assume Lighthouse, WebPageTest, or any other
  specific tool.
- Does not optimize this project's code, assets, or infrastructure - it states the target that
  optimization work is measured against.
- Does not define a new evidence document or finding code.
