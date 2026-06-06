# SW-15 Orion Coordination Runbook

Status: Active — M0 closed (Orion M0-J signed), M1 execution authorized
Date: 2026-06-05
Feature: SW-15 Minimal Character Bust Builder v0
Primary plan: ../planning/sw-15/sw-15-minimal-character-bust-builder-implementation-plan.md
Sequence guide: ./sw-15-nova-forge-implementation-sequence.md
M0 kickoff checklist: ./sw-15-m0-forge-kickoff-checklist.md
M1 Forge kickoff prompt: ./sw-15-m1-forge-kickoff-prompt.md

## Purpose

Define explicit Orion coordination handoff gates for SW-15 milestones M0-M6 so Forge and Nova execution order stays stable and release evidence is complete.

## Decision Lock (2026-06-05)

1. Player-facing availability surfaces for v0: character creation, in-game profile/customization, and station/clinic interaction.
2. Required customization domains: face shape, skin tone, hair style/color, eye style/color, expression preset, and apparel accent.
3. Persistence shape: normalized descriptor plus presetVersion/schemaVersion for cross-session and cross-device reproducibility.
4. NPC policy: hybrid deterministic baseline with admin-tool manual overrides.
5. Invalid payload policy: hard reject with explicit validation errors.
6. Visual quality bar: distinct identity at profile-card and comms-dialog sizes, no uncanny placeholder look in canary captures.
7. Preview performance target: <150ms median update on desktop and mid-range laptop baseline profiles.
8. Entity ownership model: busts are character-scoped (playable-character and NPC), not account-scoped.

## Implementation Order

1. Forge-first contract and persistence lock.
2. Nova implementation against locked contracts and normalized descriptors.
3. Forge-to-Nova integration and end-to-end save/reload cutover.
4. Joint hardening, canary validation, and release decision.

## Role Matrix

| Area | Orion | Forge | Nova |
| --- | --- | --- | --- |
| Bust descriptor schema and enum domains | Accountable | Responsible | Consulted |
| Playable-character/NPC bust persistence lifecycle | Accountable | Responsible | Consulted |
| Bust builder UX and preview behavior | Accountable | Consulted | Responsible |
| Drift gates and release readiness | Accountable | Responsible | Responsible |

## Handoff Gates (M0-M6)

### M0 - Descriptor Baseline and Persistence Lock

Entry criteria:
- SW-15 v0 scope frozen.
- Descriptor domains agreed for playable-character and NPC usage.

Forge deliverables:
- Canonical bust descriptor schema and enum domain list.
- Persistence shape for playable-character and NPC bust records.
- Strict validation and mismatch fixtures.

Nova deliverables:
- Contract review sign-off.
- Fixture compatibility validation for preview mapping paths.

Orion gate check:
- Confirms Forge-first contract and persistence lock is complete before Nova implementation branch is marked execution-ready.

Exit evidence:
- Canonical pass fixture: `test/fixtures/sw15/character-bust-canonical-pass.json` — 16/16 tests pass ([PR #2](https://github.com/qagwaai/solid-train/pull/2))
- Mismatch hard-fail: `test/fixtures/sw15/character-bust-mismatch-fail.json` — `faceShape: "triangle"` hard-fails with correct `rejectedValue`
- Seed replay: `test/fixtures/sw15/npc-bust-seed-replay.json` — deterministic seed → descriptor mapping verified
- Nova M0-V fixture compatibility acknowledgment: Completed ([Nova PR #2](https://github.com/qagwaai/laughing-octo-journey/pull/2))
- Orion M0 gate note recorded: [SW-15 M0 Forge Kickoff Checklist](sw-15-m0-forge-kickoff-checklist.md#orion-m0-gate-note-2026-06-05)

### M1 - Persistence Lifecycle

Entry criteria:
- M0 complete with signed baseline.

Forge deliverables:
- Playable-character bust create/update/read lifecycle finalized.
- NPC bust preset and seed-backed persistence lifecycle finalized.

Nova deliverables:
- Adapter integration for load/save bust descriptor paths.

Orion gate check:
- Confirms Nova does not bypass Forge normalization or persistence semantics.

Exit evidence:
- Integration tests for save/reload round-trip and strict invalid-write rejection.

### M2 - Nova Builder Baseline

Entry criteria:
- M1 complete.

Forge deliverables:
- Stable validation and normalized-response semantics for builder operations.

Nova deliverables:
- Selector-based customization panel functional.
- Live preview updates from normalized descriptor payload.
- Save/cancel/reset flows integrated.

Orion gate check:
- Confirms UX behavior matches Forge-authored constraints and blocked-save reasons are surfaced.

Exit evidence:
- Component tests for control-to-preview mapping and route smoke tests for edit lifecycle.

### M3 - NPC Reuse and Deterministic Identity

Entry criteria:
- M2 complete with baseline UX verified.

Forge deliverables:
- Role/faction preset map and deterministic seed policy finalized.

Nova deliverables:
- NPC bust rendering path consumes preset plus seed outputs.
- Reloaded descriptors produce stable visual outcomes.

Orion gate check:
- Confirms deterministic replay behavior and no hidden randomization bypass.

Exit evidence:
- Seed replay fixtures and cross-session consistency test output.

### M4 - Browser Performance and Fallback Hardening

Entry criteria:
- M3 complete.

Forge deliverables:
- Descriptor payload size envelope and optional-field fallback semantics documented.

Nova deliverables:
- Preview latency and memory checks under agreed baseline hardware profile.
- Deterministic fallback behavior for missing optional presentation fields.

Orion gate check:
- Confirms fallback behavior is non-destructive and does not silently mutate saved identity.

Exit evidence:
- Performance profile report and negative tests for no silent identity mutation.

### M5 - Canary Validation

Entry criteria:
- M4 complete and quality bars met.

Forge deliverables:
- Canary payload stability confirmation for bust lifecycle endpoints/events.

Nova deliverables:
- Canary telemetry and issue intake wiring for bust builder interactions.

Orion gate check:
- Confirms no unresolved P1/P2 issues remain after soak window.

Exit evidence:
- Canary checklist, telemetry summary, incident triage log.

### M6 - Release Decision

Entry criteria:
- M0-M5 complete with evidence chain.

Forge deliverables:
- Final contract and persistence sign-off.

Nova deliverables:
- Final builder UX and preview fidelity sign-off.

Orion gate check:
- Confirms sequence compliance and no open contract drift findings.

Exit evidence:
- Go or no-go decision record with cross-role sign-off.

## Non-Negotiable Rules

1. Nova does not finalize SW-15 integration against an unlocked bust descriptor contract.
2. Any descriptor contract drift blocks release until source-of-truth is corrected.
3. Bust configuration writes must be persisted in database-backed records.
4. Deterministic seed policy is required for NPC reuse and fixture replay.
5. All M0-M6 gates require written evidence.
6. Forge openapi.yaml remains the single contract source for Forge-to-Nova implementation details.
7. Invalid bust payloads are hard-rejected with explicit validation errors; no silent correction path is permitted.

## Sign-Off Table

| Role | Name | Date | Decision | Notes |
| --- | --- | --- | --- | --- |
| Orion | Orion | 2026-06-05 | Approved | M0-J signed; evidence accepted in kickoff checklist gate note |
| Forge lead | Forge | 2026-06-05 | Approved | M0 deliverables complete — [solid-train PR #2](https://github.com/qagwaai/solid-train/pull/2); 16/16 contract hardening tests pass |
| Nova lead | Nova | 2026-06-05 | Approved | M0-V fixture compatibility complete — [laughing-octo-journey PR #2](https://github.com/qagwaai/laughing-octo-journey/pull/2) |
| QA lead | TBD | YYYY-MM-DD | Pending | |
