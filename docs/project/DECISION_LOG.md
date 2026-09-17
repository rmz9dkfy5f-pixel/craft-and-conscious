# Decision Log

| Date | Decision | Reason | Alternatives Considered | Status |
|---|---|---|---|---|
| 2026-09-08 | Adopt Project Starter Kit v3.10.0, `web_application` profile, governance layer only (no optional modules) | Bring repo under AntBrainOS governance conventions without disrupting the working static site or forcing unneeded CI/security automation | Governance + CI/security modules enabled | Accepted |
| 2026-09-16 | Enable 10 Starter Kit optional modules; re-baseline 5 pre-existing governance docs to `project`-owned | Owner requested enabling all applicable modules; a pre-existing manifest/checksum drift on 5 files was found and fixed as part of the same work | Restore drifted files to template content instead | Accepted |
| 2026-09-17 | Set WCAG 2.2 AA as the accessibility conformance target; last-2-versions evergreen browsers (no IE11) as the support matrix; performance regressions tracked-not-blocked; all site imagery/code confirmed original/business-owned | Filling the 10 module policy docs required real policy answers rather than boilerplate; owner supplied each directly | WCAG 2.1 AA; broader legacy browser support; blocking releases on performance regressions | Accepted |
