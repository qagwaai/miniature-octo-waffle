# SW-13 Orion Coordination Runbook

Status: Active
Date: 2026-05-30
Feature: SW-13 External Object Presentation Expansion
Primary plan: ../planning/sw-13/sw-13-external-object-presentation-implementation-plan.md

## Purpose

Define explicit Orion coordination handoff gates for SW-13 milestones M0-M6 so Forge and Nova execution order stays stable and drift is blocked before release.

## Implementation Order

1. Forge-first contract lock.
2. Nova implementation against locked contract.
3. Forge-to-Nova integration and payload cutover.
4. Joint hardening and release decision.

## Role Matrix

| Area | Orion | Forge | Nova |
| --- | --- | --- | --- |
| Contract schema and enum taxonomy | Accountable | Responsible | Consulted |
| Descriptor rendering behavior | Accountable | Consulted | Responsible |
| Performance fallback policy | Accountable | Consulted | Responsible |
| Drift gates and release readiness | Accountable | Responsible | Responsible |

## Handoff Gates (M0-M6)

### M0 - Descriptor Baseline Lock

Entry criteria:
- SW-13 scope frozen for v1.
- Family domains agreed: debris, ships, gates, stations, asteroids.

Forge deliverables:
- Canonical descriptor schema and enums.
- Strict validation rules and mismatch fixtures.

Nova deliverables:
- Adapter contract review sign-off.
- Fixture compatibility check for planned render selectors.

Orion gate check:
- Confirms Forge-first contract lock is complete before Nova coding branch is marked execution-ready.

Exit evidence:
- Contract fixture pass and mismatch fixture hard-fail logs attached to milestone note.

### M1 - Debris and Asteroid Identity Pass

Entry criteria:
- M0 passed with signed contract baseline.

Forge deliverables:
- Descriptor payloads for debris and asteroid families.

Nova deliverables:
- Debris and asteroid family rendering with deterministic selector tests.

Orion gate check:
- Confirms no legacy mapping fallback path appears in Nova implementation.

Exit evidence:
- Component snapshots and selector test output.

### M2 - Ship and Station Family Pass

Entry criteria:
- M1 complete and test baseline green.

Forge deliverables:
- Ship and station descriptor families with stable role/faction identity fields.

Nova deliverables:
- Ship and station rendering pass with recognition-distance checks.

Orion gate check:
- Confirms ship-external readability acceptance criteria and hotspot boundaries remain intact.

Exit evidence:
- Route-smoke evidence and recognition threshold report.

### M3 - Jump Gate Landmark Pass

Entry criteria:
- M2 complete.

Forge deliverables:
- Gate descriptor cues and approach metadata finalized.

Nova deliverables:
- Gate landmark treatment integrated into navigation-facing flows.

Orion gate check:
- Confirms gate identity ambiguity tests fail as expected on weak-cue fixtures.

Exit evidence:
- Ambiguity regression test output and gate approach flow checks.

### M4 - Balanced Performance Validation

Entry criteria:
- M3 complete with full family coverage.

Forge deliverables:
- Descriptor size and payload consistency review.

Nova deliverables:
- Fallback policy implementation and dense-scene performance checks.

Orion gate check:
- Confirms fallback behavior is deterministic and does not collapse identity semantics.

Exit evidence:
- Performance profile run output and deterministic fallback assertions.

### M5 - Canary Validation

Entry criteria:
- M4 complete and quality bars met.

Forge deliverables:
- Canary environment payload stability confirmation.

Nova deliverables:
- Canary visual telemetry instrumentation and issue intake wiring.

Orion gate check:
- Confirms no unresolved P1/P2 issues remain after soak window.

Exit evidence:
- Canary checklist, telemetry summary, issue triage log.

### M6 - Release Decision

Entry criteria:
- M0-M5 complete with evidence chain.

Forge deliverables:
- Final contract and payload stability sign-off.

Nova deliverables:
- Final rendering and performance sign-off.

Orion gate check:
- Confirms sequence compliance (Forge contract lock before Nova implementation) and no open drift findings.

Exit evidence:
- Go or no-go decision record with sign-off table.

## Non-Negotiable Rules

1. Nova does not finalize SW-13 integration against an unlocked descriptor contract.
2. Any contract drift blocks release until source-of-truth is corrected.
3. Legacy presentation fallbacks are not reintroduced.
4. All M0-M6 gates require written evidence.

## Sign-Off Table

| Role | Name | Date | Decision | Notes |
| --- | --- | --- | --- | --- |
| Orion | TBD | YYYY-MM-DD | Pending | |
| Forge lead | TBD | YYYY-MM-DD | Pending | |
| Nova lead | TBD | YYYY-MM-DD | Pending | |
| QA lead | TBD | YYYY-MM-DD | Pending | |