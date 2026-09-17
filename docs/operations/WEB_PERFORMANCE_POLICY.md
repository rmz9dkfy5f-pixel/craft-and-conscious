# Web Performance Policy

This module (`web_performance`) generates this policy. It runs no measurement and assumes no
tool: the budget below is what this project's users actually experience, measured with whatever
tooling this project already uses or chooses to adopt.

## Performance Budget

Adopting the standard Core Web Vitals "good" thresholds as this project's stated target, since no
site-specific alternative has previously been set:

- Largest Contentful Paint (LCP): < 2.5s
- Interaction to Next Paint (INP): < 200ms
- Cumulative Layout Shift (CLS): < 0.1
- Time to First Byte (TTFB): < 0.8s

**Asset size budget:** each version's `index.html` plus its 4 referenced images in `images/`
should stay under 2MB transferred in total — there is no build/minification/compression step, so
shipped size is exactly source size.

## Measurement Practice

No lab or field measurement has been run against this site yet — a real, stated gap, not a passed
check. Once a deployment target exists (none is configured today — see
`docs/governance/PROJECT_CLASSIFICATION.md`), lab measurement (e.g. PageSpeed Insights/Lighthouse
against the live URL) is the natural first step, since there is no CI to wire an automated lab run
into. Field measurement (e.g. Chrome UX Report) is not available until the site has real traffic
at a real URL.

## Regression Handling

**Track and revisit** — confirmed with the owner 2026-09-17. A budget overage is logged as a known
item rather than blocking anything, since there is no release pipeline for it to block against.

## What this module deliberately does not do

- Does not run a measurement tool, and does not assume Lighthouse, WebPageTest, or any other
  specific tool.
- Does not optimize this project's code, assets, or infrastructure - it states the target that
  optimization work is measured against.
- Does not define a new evidence document or finding code.
