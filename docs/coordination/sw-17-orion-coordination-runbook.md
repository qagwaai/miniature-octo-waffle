# SW-17 Orion Coordination Runbook

Status: Active
Date: 2026-05-30
Feature: SW-17 Computer Progression (Per-Ship Intelligence Tiers)
Primary plan: ../planning/sw-17/sw-17-computer-progression-implementation-plan.md
Closure checklist: ../planning/sw-17/sw-17-computer-progression-closure-checklist.md

## Purpose

Define explicit Orion coordination handoff gates for SW-17 milestones M0-M6 so Forge and Nova execution order remains consistent and release evidence is complete.

## Implementation Order

1. Forge-first contract and persistence lock.
2. Nova implementation against locked contracts and capability map.
3. Forge-to-Nova integration and end-to-end advisory flow cutover.
4. Joint hardening, canary validation, and release decision.

## Role Matrix

| Area | Orion | Forge | Nova |
| --- | --- | --- | --- |
| Capability contract and tier schema | Accountable | Responsible | Consulted |
| Per-ship persistence and gate enforcement | Accountable | Responsible | Consulted |
| Advisory UI and confirmation flow | Accountable | Consulted | Responsible |
| Drift gates and release readiness | Accountable | Responsible | Responsible |

## Handoff Gates (M0-M6)

### M0 - Contract and Capability Baseline Lock

Entry criteria:
- SW-17 scope frozen for v1.
- Tier capability ladder agreed.

Forge deliverables:
- Canonical capability contract and per-ship persistence shape.
- Strict validation and mismatch fixtures.

Nova deliverables:
- Contract review sign-off.
- Fixture compatibility validation for capability rendering paths.

Orion gate check:
- Confirms Forge-first lock is complete before Nova implementation branch is marked execution-ready.

Exit evidence:
- Baseline fixture pass and intentional mismatch failure logs.

### M1 - Tier Model and Persistence

Entry criteria:
- M0 complete with signed contract baseline.

Forge deliverables:
- Install and upgrade endpoints/events finalized.
- Per-ship installed tier persistence validated.

Nova deliverables:
- Tier state consumption integrated in UI data adapters.

Orion gate check:
- Confirms no frontend assumptions bypass Forge persistence semantics.

Exit evidence:
- Integration tests for install and upgrade lifecycle.

### M2 - Skill and Level Gate Enforcement

Entry criteria:
- M1 complete.

Forge deliverables:
- Computer Systems Installation skill and level gate checks.
- Explicit unlock reason payloads for blocked installs.

Nova deliverables:
- Gate reason rendering and blocked-state UX behavior.

Orion gate check:
- Confirms gate logic remains source-authored in Forge and surfaced transparently in Nova.

Exit evidence:
- Boundary tests (minus/equal/plus) and blocked-state UI tests.

### M3 - Advisory Feature Surfacing

Entry criteria:
- M2 complete with gate behavior validated.

Forge deliverables:
- Deterministic capability unlock mapping by tier.

Nova deliverables:
- Advisory surfaces for mandatory features at designated tiers.

Orion gate check:
- Confirms tier-driven behavior is deterministic and no shadow unlock paths exist.

Exit evidence:
- Component tests and route smoke tests for advisory panel.

### M4 - Light Automation Confirmation Safety

Entry criteria:
- M3 complete.

Forge deliverables:
- Assist action semantics finalized for confirmation-required flow.

Nova deliverables:
- Mandatory confirmation UI path with cancel-safe behavior.

Orion gate check:
- Confirms no silent auto-execution path remains.

Exit evidence:
- Negative tests for no-confirm execution and state-stability checks on cancel.

### M5 - Canary Validation

Entry criteria:
- M4 complete and quality bars met.

Forge deliverables:
- Canary payload stability verification.

Nova deliverables:
- Canary telemetry and incident intake instrumentation.

Orion gate check:
- Confirms no unresolved P1/P2 issues remain in soak window.

Exit evidence:
- Canary checklist, telemetry summary, incident triage log.

### M6 - Release Decision

Entry criteria:
- M0-M5 complete with evidence chain.

Forge deliverables:
- Final contract and persistence sign-off.

Nova deliverables:
- Final advisory UX and confirmation safety sign-off.

Orion gate check:
- Confirms sequence compliance and no open drift findings.

Exit evidence:
- Go or no-go decision record with role sign-off.

## Non-Negotiable Rules

1. Nova does not finalize SW-17 integration against unlocked contracts.
2. Any capability contract drift blocks release until source-of-truth is corrected.
3. Light automation actions never execute without explicit user confirmation.
4. All M0-M6 gates require written evidence.

## Sign-Off Table

| Role | Name | Date | Decision | Notes |
| --- | --- | --- | --- | --- |
| Orion | TBD | YYYY-MM-DD | Pending | |
| Forge lead | TBD | YYYY-MM-DD | Pending | |
| Nova lead | TBD | YYYY-MM-DD | Pending | |
| QA lead | TBD | YYYY-MM-DD | Pending | |