# SW-15 Nova-Forge Implementation Sequence

Status: Active — M0 and M1 closed; Forge M2-A complete; awaiting Nova M2-A
Date: 2026-06-05
Feature: SW-15 Minimal Character Bust Builder v0
Primary implementation plan: ../planning/sw-15/sw-15-minimal-character-bust-builder-implementation-plan.md
Coordination runbook: ./sw-15-orion-coordination-runbook.md
Contract authority: ./forge-openapi-contract-policy.md
M0 kickoff checklist: ./sw-15-m0-forge-kickoff-checklist.md
M1 Forge kickoff prompt: ./sw-15-m1-forge-kickoff-prompt.md
M1 Forge verification note: ./sw-15-m1-forge-verification-note-2026-06-05.md
Nova M1-V prompt: ./sw-15-m1v-nova-prompt.md
M1 Orion gate note: ./sw-15-m1-orion-gate-note-2026-06-05.md
M2-A Forge kickoff prompt: ./sw-15-m2a-forge-kickoff-prompt.md
M2-A Forge verification note: ./sw-15-m2a-forge-verification-note-2026-06-05.md
Nova M2-A prompt: ./sw-15-m2a-nova-prompt.md

## Purpose

Define the execution choreography between Forge and Nova for SW-15 so both teams can move quickly while minimizing contract drift and rework.

## Operating Principles

1. Forge-first contract lock for each milestone slice before Nova implementation proceeds.
2. Nova begins coding only on explicit OpenAPI-backed schema sections for that slice.
3. Each milestone closes with joint conformance evidence, not independent green checks.
4. Any behavior not represented in Forge openapi.yaml is treated as drift and blocks milestone close.
5. Persistence behavior is owned by Forge and must be validated before Nova UX is marked complete.

## Decision Lock (2026-06-05)

1. v0 entry surfaces: character creation, in-game profile/customization, and station/clinic interaction.
2. Required customization domains: face shape, skin tone, hair style/color, eye style/color, expression preset, and apparel accent.
3. Persistence payload requirement: normalized descriptor plus presetVersion/schemaVersion.
4. NPC strategy: deterministic baseline plus admin-tool manual overrides.
5. Invalid payload handling: hard reject with explicit validation errors.
6. Visual acceptance gates: distinct identity at profile-card and comms-dialog sizes, no uncanny placeholder look in canary captures.
7. Performance gate: <150ms median preview update on desktop and mid-range laptop baseline profiles.
8. Entity ownership model: busts are character-scoped (playable-character and NPC), not account-scoped.

## Milestone Sequence (M0-M6)

### M0 - Descriptor and Persistence Baseline Lock

Status update (2026-06-05):
1. Closed.
2. Orion M0-J baseline lock signed.
3. M1 execution authorized.
4. Evidence chain: [solid-train PR #2](https://github.com/qagwaai/solid-train/pull/2), [laughing-octo-journey PR #2](https://github.com/qagwaai/laughing-octo-journey/pull/2), and [SW-15 M0 gate note](sw-15-m0-forge-kickoff-checklist.md#orion-m0-gate-note-2026-06-05).

Sequence:
1. Forge M0-A: Publish SW-15 schema components and enum domains in openapi.yaml.
2. Forge M0-B: Publish persistence model shape for playable-character and NPC bust records.
3. Forge M0-C: Provide pass fixture and intentional mismatch fixtures.
4. Nova M0-V: Verify fixture compatibility against planned preview mapping paths.
5. Joint M0-J: Orion signs baseline lock.

Synchronization checkpoint:
- Nova cannot start M1 implementation until Forge M0-A through M0-C are complete and reviewed.

Milestone close evidence:
- OpenAPI section references.
- Fixture pass and mismatch hard-fail logs.

### M1 - Persistence Lifecycle

Status update (2026-06-05):
1. Forge M1-A, M1-B, and M1-C reported complete.
2. Nova M1-V reported complete with adapter integration and gate-evidence package.
3. No unresolved contract drift findings reported.
4. Orion M1-J signed; M1 closed.
5. M2 execution authorized.
6. Forge evidence note: [SW-15 M1 Forge Verification Note](sw-15-m1-forge-verification-note-2026-06-05.md).
7. Orion closure note: [SW-15 M1 Orion Gate Note](sw-15-m1-orion-gate-note-2026-06-05.md).

Sequence:
1. Forge M1-A: Implement create/update/read lifecycle for playable-character bust descriptor.
2. Forge M1-B: Implement preset and seed-backed lifecycle for NPC bust descriptor.
3. Forge M1-C: Enforce validation and normalization on all write paths and return explicit hard-reject validation errors on invalid payloads.
4. Nova M1-V: Integrate adapter layer for load/save and normalized response handling.
5. Joint M1-J: Validate persistence round-trip and invalid-write rejection.

Synchronization checkpoint:
- Nova M1-V may proceed in parallel with Forge M1-C only if endpoint and schema signatures are already locked from M1-A and M1-B.

Milestone close evidence:
- Integration test results for save/reload round-trip.
- Negative tests for strict validation rejects.

### M2 - Builder Interaction Baseline

Status update (2026-06-05):
1. Forge M2-A response semantics lock reported complete.
2. `BustBlockedSaveResponse` contract addition introduced intentionally for M2-A.
3. Semantic lock coverage reported with 22 pass, 0 fail.
4. Handoff status: ready for Nova M2-A.
5. Evidence note: [SW-15 M2-A Forge Verification Note](sw-15-m2a-forge-verification-note-2026-06-05.md).

Sequence:
1. Forge M2-A: Freeze response semantics for validation errors, blocked-save reasons, and normalized payload echoes.
2. Nova M2-A: Build selector controls and live preview binding against normalized payload model.
3. Nova M2-B: Implement save/cancel/reset interaction flow.
4. Forge M2-V: Verify Nova request payloads remain schema-conformant in integration fixtures.
5. Joint M2-J: Confirm UX state transitions and response handling are deterministic.

Synchronization checkpoint:
- If Forge changes blocked-save reason schema after Nova M2-A starts, M2 returns to Forge M2-A lock state.

Milestone close evidence:
- Component tests for control-to-preview mapping.
- Route-level edit lifecycle smoke tests.

### M3 - NPC Reuse Determinism

Sequence:
1. Forge M3-A: Lock role/faction preset map and deterministic seed policy.
2. Forge M3-B: Publish seed replay fixtures and expected descriptor outputs.
3. Nova M3-A: Implement NPC bust rendering path using preset plus seed outputs.
4. Nova M3-V: Validate cross-session replay consistency.
5. Joint M3-J: Orion verifies no hidden randomization path exists.

Synchronization checkpoint:
- Any seed algorithm change after fixture publication requires fixture version bump and Nova replay re-baseline before closing M3.

Milestone close evidence:
- Seed replay test output.
- Cross-session consistency report.

### M4 - Performance and Fallback Hardening

Sequence:
1. Forge M4-A: Lock descriptor size envelope and optional-field fallback semantics in contract notes.
2. Nova M4-A: Implement performance checks for preview latency and memory under desktop and mid-range laptop baseline profiles.
3. Nova M4-B: Implement deterministic fallback behavior for missing optional presentation fields.
4. Forge M4-V: Verify fallback-triggering payloads remain contract valid.
5. Joint M4-J: Confirm no silent identity mutation under fallback paths.

Synchronization checkpoint:
- Nova cannot optimize by dropping required fields; required-field relaxations must be Forge-authored and contract-updated first.

Milestone close evidence:
- Performance profile report proving <150ms median preview update on desktop and mid-range laptop baseline profiles.
- Negative tests for identity mutation prevention.

### M5 - Canary Validation

Sequence:
1. Forge M5-A: Confirm canary payload stability for bust lifecycle operations.
2. Nova M5-A: Enable canary telemetry and incident intake for builder interactions.
3. Joint M5-J: Run soak window and triage all high-severity findings.
4. Orion M5-G: Gate closes only when no unresolved P1/P2 issues remain.

Synchronization checkpoint:
- Any canary incident traced to contract mismatch reopens the latest impacted milestone (M2-M4) before M5 can close.

Milestone close evidence:
- Canary checklist.
- Telemetry summary and incident triage log.

### M6 - Release Decision

Sequence:
1. Forge M6-A: Final contract and persistence sign-off.
2. Nova M6-A: Final builder UX and preview fidelity sign-off.
3. Joint M6-J: Orion confirms sequence compliance and drift status.
4. Orion M6-G: Go/no-go decision recorded.

Synchronization checkpoint:
- M6 cannot close if any prior milestone has unresolved drift findings.

Milestone close evidence:
- Signed go/no-go record with role approvals.

## Allowed Parallelism Rules

1. Nova may build UI scaffolding in parallel with Forge only when contracts for that UI slice are already locked.
2. Nova may not ship data-shape assumptions pending future Forge decisions.
3. Forge may refactor internals without reopening milestones as long as OpenAPI contract and persistence semantics are unchanged.
4. Parallel work must converge into shared fixture and integration evidence before milestone closure.

## Drift Prevention Controls

1. Every milestone note must cite exact OpenAPI schema names or endpoint sections touched.
2. Every milestone requires at least one intentional mismatch fixture that hard-fails.
3. Any Nova workaround for contract mismatch is temporary only in feature branch and cannot merge without source contract fix.
4. Drift findings are triaged same day and assigned to source owner immediately.

## Quick Start Checklist (Per Milestone)

1. Forge declares contract lock for the milestone slice.
2. Orion confirms lock and marks Nova execution-ready.
3. Nova implements against locked schema only.
4. Forge and Nova run joint fixture/integration checks.
5. Orion records evidence and closes gate.
