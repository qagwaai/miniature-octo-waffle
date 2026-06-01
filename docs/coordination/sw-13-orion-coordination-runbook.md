# SW-13 Orion Coordination Runbook

Status: Closed (Stellar Viewer only)
Date: 2026-05-31
Feature: SW-13 External Object Presentation Expansion
Primary plan: ../planning/sw-13/sw-13-external-object-presentation-implementation-plan.md

## Purpose

Define explicit Orion coordination handoff gates for SW-13 milestones M0-M6 so Forge and Nova execution order stays stable and drift is blocked before release.

## Closure Decision (2026-05-31)

1. SW-13 is closed for Stellar Viewer rendering plus contract objectives only.
2. ship-external-view support is explicitly deferred to SW-13A.
3. High-poly support for Stellar Viewer and ship-external-view is explicitly deferred to SW-13B.
4. Any dual-surface or high-poly language below is historical context for the prior plan shape and is not a blocker for SW-13 closure.

## Current Milestone Status (2026-05-31)

- M0: Closed for SW-13 Stellar Viewer-only scope.
- M1: Closed for SW-13 Stellar Viewer-only scope.
- M2: Closed for SW-13 Stellar Viewer-only scope.
- M3: Closed for SW-13 Stellar Viewer-only scope.
- M4: Closed for SW-13 Stellar Viewer-only scope.
- M5: Closed for SW-13 Stellar Viewer-only scope.
- M6: Closed; release decision accepted for SW-13 Stellar Viewer-only scope.

## Follow-On Features

1. SW-13A: ship-external-view support for the SW-13 descriptor-driven presentation model.
2. SW-13B: high-poly support for Stellar Viewer and ship-external-view.
3. SW-13C: ship-external contract-backed entity feeds for gates, stations, and encounter ships.

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

## Surface Coverage Contract (Nova)

1. SW-13 implementation scope is dual-surface by default: `ship-external-view` and `stellar-viewer`.
2. A milestone touching object readability, landmark recognition, or fallback behavior must include evidence from both surfaces unless Orion issues an explicit written waiver.
3. Orion does not close SW-13 milestone gates on single-surface evidence.
4. Any temporary single-surface execution sequence must be labeled partial and include a dated completion commitment for the second surface.

## Asset Fidelity Dependency Contract (Nova)

1. SW-13 Nova implementation assumes high-poly hero assets are available for affected families (debris, ships, stations, gates, asteroids).
2. If a required high-poly hero asset is missing, Nova may use an Orion-approved temporary proxy only when the proxy mapping and replacement date are recorded in milestone evidence.
3. Orion does not close M1-M5 gates when high-poly readiness or approved proxy evidence is missing.
4. Proxy usage is temporary by policy and must include an owner and dated replacement commitment.

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

Current status note:
- Nova reports M0 deliverables complete.
- Orion gate remains open until Nova evidence is reviewed and accepted.

M0 Step 1 decision lock (for Step 2 fixture generation):
1. Fallback tier naming remains exactly: hero, standard, minimal.
2. Gate family values for this schema version remain exactly: ring-gate, segmented-arch, relay-spindle.
3. Do not add a reserved gate family value in sw-13-m0-v1; expansion requires a later schema version.
4. Faction cue unknown is permitted for unattributed objects, including canary fixtures.
5. Step 2 mismatch fixtures must hard-fail any schemaVersion other than sw-13-m0-v1.
6. displayLabel is mandatory for production descriptors and canonical pass fixtures.
7. displayLabel may be omitted only in intentional negative mismatch fixtures.

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
- High-poly asset readiness note (or approved proxy mapping with replacement date) for debris and asteroid families.

Current status note:
- Forge reports M1 deliverables complete.
- Nova reports M1 deliverables complete.
- Orion gate remains open until Nova evidence is attached and reviewed.

### M2 - Ship and Station Family Pass

Entry criteria:
- M1 complete and test baseline green.

Forge deliverables:
- Ship and station descriptor families with stable role/faction identity fields.

Nova deliverables:
- Ship and station rendering pass with recognition-distance checks in ship-external-view and stellar-viewer.

Orion gate check:
- Confirms ship-external-view and stellar-viewer readability acceptance criteria and hotspot boundaries remain intact.

Exit evidence:
- Dual-surface route-smoke evidence and recognition threshold report.
- High-poly asset readiness note (or approved proxy mapping with replacement date) for ship and station families.

M2 decision lock (for Nova evidence pass):
1. Nova recognition checks should use all 9 M2 descriptors from Forge fixture [test/fixtures/sw13/external-object-descriptor-m2-ships-stations.json](https://github.com/qagwaai/solid-train/blob/main/test/fixtures/sw13/external-object-descriptor-m2-ships-stations.json) as the canonical baseline.
2. Route-smoke scenarios may use focused subsets, but sign-off evidence must include full-9 coverage results.
3. fallbackTier is data plus behavior for M2 evidence: Nova must assert expected fallback behavior for hero, standard, and minimal tiers.
4. Component-level OpenAPI contract surfacing is sufficient for M2 handoff; no additional dedicated retrieval surface is required in this milestone.
5. Current faction mappings for frigate, interceptor, and naval-outpost are accepted for Nova readability baseline.
6. Publish a formal faction matrix before M3 as a forward guardrail, not as an M2 blocker.

Current status note:
- Forge reports M2 deliverables complete.
- Orion gate remains open until Nova route-smoke and recognition evidence is attached and reviewed.

### M3 - Jump Gate Landmark Pass

Entry criteria:
- M2 complete.

Forge deliverables:
- Gate descriptor cues and approach metadata finalized.

Nova deliverables:
- Gate landmark treatment integrated into navigation-facing flows in ship-external-view and stellar-viewer.

Orion gate check:
- Confirms dual-surface gate identity ambiguity tests fail as expected on weak-cue fixtures.

Exit evidence:
- Dual-surface ambiguity regression output and gate approach flow checks.
- High-poly asset readiness note (or approved proxy mapping with replacement date) for gate landmark families.

M3 decision lock (for Nova evidence pass):
1. Nova M3 ambiguity tests should require all three gate families in every route-smoke run.
2. Aggregate suite coverage alone is not sufficient for M3 sign-off; each route-smoke run must exercise ring-gate, segmented-arch, and relay-spindle.
3. hazardCue medium must be treated as a mandatory warning escalation in M3 evidence criteria.
4. Orion will lock numeric tolerance guidance before Nova finalizes assertion thresholds.
5. recommendedStandOffKm and approachWindowKm min/max checks should use Orion-published numeric tolerances, not ad hoc per-test values.
6. A required mapping matrix from approachCue to landmarkFraming combinations is not required for M3 if enum validation and fixture alignment are already complete.
7. Current enum validation plus fixture alignment is sufficient for this milestone.

Current status note:
- Forge reports M3 deliverables complete.
- Orion gate remains open until Nova route-smoke and ambiguity evidence is attached and reviewed.

### M4 - Balanced Performance Validation

Entry criteria:
- M3 complete with full family coverage.

Forge deliverables:
- Descriptor size and payload consistency review.

Nova deliverables:
- Fallback policy implementation and dense-scene performance checks in ship-external-view and stellar-viewer.

Orion gate check:
- Confirms fallback behavior is deterministic and does not collapse identity semantics.

Exit evidence:
- Dual-surface performance profile output and deterministic fallback assertions.
- Asset-fidelity fallback note confirming identity preservation under tier reductions.

M4 decision lock (for Nova evidence pass):
1. Nova should consume the M4 size budget from the stable fixture report and also enforce runtime guardrails against the same max envelope values.
2. The M4 envelope values are authoritative for both fixture and runtime checks: 16 descriptor entries and 3 gate entries.
3. Nova dense-scene tests should use hard numerical thresholds tied to the committed M4 report, not relative regression checks alone.
4. Current max descriptor bytes in the M4 report, including gate descriptor max 328, should be enforced as explicit thresholds in Nova evidence.
5. Artifact-to-fixture parity checks against [sw13-m4-size-consistency-report.json](https://github.com/qagwaai/solid-train/blob/main/test/fixtures/sw13/sw13-m4-size-consistency-report.json) are required for M4 sign-off.
6. The report is authoritative evidence, not merely informative context.

Current status note:
- Forge reports M4 deliverables complete.
- Orion gate remains open until Nova dense-scene, runtime-guardrail, and parity evidence is attached and reviewed.

### M5 - Canary Validation

Entry criteria:
- M4 complete and quality bars met.

Forge deliverables:
- Canary environment payload stability confirmation.

Nova deliverables:
- Canary visual telemetry instrumentation and issue intake wiring for ship-external-view and stellar-viewer.

Orion gate check:
- Confirms no unresolved P1/P2 issues remain after soak window.

Exit evidence:
- Dual-surface canary checklist, telemetry summary, issue triage log.
- High-poly/proxy burn-down note with open replacement dates and owners.

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
5. Forge `openapi.yaml` remains the single contract source for Forge-to-Nova implementation details.
6. M0 and later handoffs must reference concrete OpenAPI schema sections used by Nova.
7. SW-13A is the authoritative feature for ship-external-view enablement scope that was deferred from SW-13.
8. SW-13B is the authoritative feature for high-poly readiness across Stellar Viewer and ship-external-view.

## Sign-Off Table

| Role | Name | Date | Decision | Notes |
| --- | --- | --- | --- | --- |
| Orion | TBD | YYYY-MM-DD | Pending | |
| Forge lead | TBD | YYYY-MM-DD | Pending | |
| Nova lead | TBD | YYYY-MM-DD | Pending | |
| QA lead | TBD | YYYY-MM-DD | Pending | |