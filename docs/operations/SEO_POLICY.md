# SEO Policy

This module (`seo`) generates this policy. It runs no crawler and assumes no tool: what is
crawlable and how it is described below is this project's own deliberate statement, not whatever a
framework's defaults happened to produce.

## Indexability requirements

- `robots.txt` and per-page meta-robots directives state, deliberately, what is and is not meant
  to be indexed - content excluded from indexing is excluded on purpose, named here, not merely
  unindexed by accident.
- A sitemap lists the URLs this project wants discovered, kept current as content changes.
- Canonical URLs are declared wherever the same content is reachable by more than one URL, so
  duplicate-content ambiguity is resolved by this project, not guessed by a crawler.

## Metadata requirements

- Every publicly indexable page has a distinct title and description.
- Structured data (schema.org or equivalent) is used where it materially improves how this
  project's content is represented in search results, not added everywhere by default.
- Open Graph / social-card metadata is present wherever a shared link's preview matters.

## Verification practice

- Indexability and metadata are checked against the requirements above on a stated cadence
  relative to release, using a crawler, validator, or manual review - whichever this project
  chooses, stated rather than implied.

## What this module deliberately does not do

- Does not run a crawler or metadata validator, and does not assume one.
- Does not guarantee search ranking or traffic - it states and requires verification of what is
  crawlable and how it is described, which search engines still rank on their own terms.
- Does not define a new evidence document or finding code.
