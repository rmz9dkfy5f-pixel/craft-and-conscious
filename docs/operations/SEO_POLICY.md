# SEO Policy

This module (`seo`) generates this policy. It runs no crawler and assumes no tool: what is
crawlable and how it is described below is this project's own deliberate statement, not whatever a
framework's defaults happened to produce.

## Indexability Requirements

No `robots.txt` or `sitemap.xml` exists anywhere in this repository as of this entry — both are
genuinely open items, not a decision yet, because **no deployment target is configured**
(`docs/governance/PROJECT_CLASSIFICATION.md`: classification `git_backed_with_remote`, no
deployment target). Per-page meta-robots directives and canonical URLs are moot for the same
reason: there is exactly one page per version (`index.html`) and no live URL for a crawler to
reach yet.

## Metadata Requirements

`v9/index.html`'s `<head>` currently has:

- `<title>Craft Candle Company | Niche Candles for Modern Rituals</title>` — present, specific.
- `<meta name="description" content="Craft Candle Company creates design-forward scents for home,
  gifting, and daily self-care.">` — present, specific.

Not yet present, and recorded here as open items rather than silent gaps:

- Open Graph / social-card metadata (`og:title`, `og:description`, `og:image`, etc.).
- Structured data (schema.org `Product`/`Organization` markup, or equivalent).
- A canonical `<link>` tag.

## Verification Practice

None yet — deferred until a deployment target exists, since there is no live page to crawl or
validate metadata against today.

## What This Module Deliberately Does Not Do

- Does not run a crawler or metadata validator, and does not assume one.
- Does not guarantee search ranking or traffic - it states and requires verification of what is
  crawlable and how it is described, which search engines still rank on their own terms.
- Does not define a new evidence document or finding code.

## What this module deliberately does not do

- Does not run a crawler or metadata validator, and does not assume one.
- Does not guarantee search ranking or traffic - it states and requires verification of what is
  crawlable and how it is described, which search engines still rank on their own terms.
- Does not define a new evidence document or finding code.
