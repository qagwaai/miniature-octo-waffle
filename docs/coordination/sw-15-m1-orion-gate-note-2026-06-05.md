# SW-15 M1 Orion Gate Note

Decision Date: 2026-06-05
Owner: Orion
Milestone: M1 Persistence Lifecycle
Decision: Approved, M1 closed

## Evidence Intake Summary

Forge evidence input:
- https://github.com/qagwaai/miniature-octo-waffle/blob/main/docs/coordination/sw-15-m1-forge-verification-note-2026-06-05.md

Nova evidence inputs:
- https://github.com/qagwaai/laughing-octo-journey/blob/main/docs/planning/sw-15/sw-15-m1v-verification-note-2026-06-05.md
- https://github.com/qagwaai/laughing-octo-journey/blob/main/docs/planning/sw-15/sw-15-m1v-handoff-note-2026-06-05.md

Reported Nova implementation coverage:
1. Adapter service implemented for all six bust lifecycle paths.
2. Typed adapter contract promoted from placeholder to concrete methods.
3. Request model updates for correlation autofill support.
4. Focused adapter tests covering hard-reject mapping and concurrent out-of-order isolation.

Reported Nova verification results:
1. Focused unit tests: 7 pass, 0 fail.
2. Targeted Playwright checks: 6 pass, 0 fail.
3. No unresolved Nova-side contract drift.
4. No compensating Nova fallback behavior introduced.

## Contract and Drift Disposition

1. Character-scoped ownership remains intact.
2. Persistence payload contract remains normalized descriptor plus presetVersion/schemaVersion.
3. Hard-reject validation behavior remains intact.
4. Forge evidence URL in Nova intake returned 404 at Nova run time; Nova documented this and remained anchored to Forge contract authority openapi.yaml.

## Gate Result

1. M1-A, M1-B, M1-C (Forge) accepted.
2. M1-V (Nova) accepted.
3. Orion M1-J signed.
4. M2 execution authorized.

## Follow-up

1. Ensure M1 evidence URLs resolve from main branch post-merge to avoid future intake friction.
