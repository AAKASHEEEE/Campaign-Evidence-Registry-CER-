# Roadmap and go/no-go gates

## Milestone 0 — Repository foundation

- [x] Versioned schema and synthetic fixture
- [x] Cross-reference and evidence-state validation
- [x] Read-only API and CLI
- [x] CI, tests and contributor guidance

**Gate:** clean install, validation, tests and formatting/lint checks pass.

## Milestone 1 — Problem discovery

- [ ] Interview 5–8 independent Web3 researchers and developer-tool builders
- [ ] Observe a real campaign verification workflow
- [ ] Record where existing trackers and APIs are sufficient or insufficient
- [ ] Identify the first claim types worth standardizing

**Gate:** at least one repeated workflow is demonstrably painful and not already adequately served by available tools. If not, narrow or stop.

## Milestone 2 — Evidence pilot

- [ ] Curate 30–50 real claims from 5–10 projects using primary sources
- [ ] Obtain a second independent review of the same sample
- [ ] Record reviewer disagreements and revise the schema
- [ ] Review source terms and dataset licensing before publishing collected material

**Provisional gate:** all non-unverified claims have resolvable evidence; at least 95% reviewer agreement on the pilot labels; all disagreements are documented. This is a small pilot threshold, not a statistical guarantee.

## Milestone 3 — External developer validation

- [ ] Ask at least two developers to consume the API or raw JSON dataset
- [ ] Collect integration feedback and schema-change requests
- [ ] Test installation from a clean environment
- [ ] Publish a tagged 0.1.0 release only when docs and checks are reproducible

**Gate:** external developers can use the records without maintainer-only instructions.

## Milestone 4 — Reassess scope

- [ ] Decide whether source adapters are justified
- [ ] Decide whether a database is justified
- [ ] Decide whether dataset licensing is sufficiently clear
- [ ] Publish measured quality and adoption metrics without inflating them

A crawler, dashboard, notifications, wallet tools or reward predictions are not automatic next steps. Build only what validated user evidence supports.
