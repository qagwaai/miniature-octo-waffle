# SW-15 Minimal Character Bust Builder v0 Implementation Plan (Nova + Forge)

Status: Draft (Execution Ready)
Date: 2026-06-05
Repo: laughing-octo-journey (Nova)
Related repo: solid-train (Forge)
Feature ID: SW-15
Priority Score Reference: 3.60 (Active net-new)

## 1. Objective

Deliver a browser-friendly character bust builder that enables player identity expression and reusable NPC portrait variants without introducing a heavy 3D authoring pipeline.

This slice is preset-driven, contract-backed, persistence-first, and deterministic for testability.

## 2. Planning Inputs (Captured via Intake)

1. Feature target: Minimal Character Bust Builder v0.
2. Intent: player identity customization and NPC bust reuse.
3. Runtime constraint: browser-friendly rendering and payload sizes.
4. Architecture bias: contract-backed descriptors with strict validation.
5. Data policy: bust configuration must be persisted in database-backed player and NPC records.
6. Coordination model: Forge locks contracts and persistence semantics first, Nova integrates UI and rendering against locked contracts.
7. Player access surfaces for v0: character creation, in-game profile/customization, and station/clinic interaction.
8. v0 customization domains required: face shape, skin tone, hair style/color, eye style/color, expression preset, and apparel accent.
9. Persistence decision: store normalized descriptor payload plus presetVersion/schemaVersion for reproducible cross-session and cross-device rendering.
10. NPC reuse policy: hybrid model with deterministic baseline plus manual overrides via admin tooling.
11. Contract policy for invalid payloads: hard reject with explicit validation errors.
12. Visual acceptance baseline: distinct identity at profile-card and comms-dialog sizes with no uncanny placeholder presentation in canary captures.
13. Performance baseline: live preview target is <150ms median update on desktop and mid-range laptop baseline profiles.

## 2A. Entity Ownership Clarification

1. Bust ownership is character-scoped, not account-scoped.
2. A player may edit bust settings only for the currently selected playable character.
3. Persistence targets are playable-character records and NPC records.
4. No global player-level bust profile is used as source-of-truth in SW-15.

## 3. Scope

In scope (SW-15 v0):
1. Bust descriptor model for a constrained set of customization domains (face shape, skin tone, hair, eyes, apparel accent, expression preset).
2. Playable-character bust create/edit flow with live preview and deterministic reset-to-default action.
3. NPC bust reuse model via descriptor presets and role/faction seed variants.
4. Backend persistence for playable-character bust profile and NPC bust descriptors.
5. Contract-backed validation and normalization for all bust descriptor writes.
6. Browser-safe rendering mode with deterministic fallback for missing assets.

Out of scope (defer):
1. Full body avatar creator.
2. Free-form mesh sculpting or unrestricted slider systems.
3. Voice, animation rigging, or cinematic facial performance systems.
4. Runtime AI-generated portrait synthesis.

## 4. Core Rules

1. Contract payloads are source-of-truth for bust descriptors.
2. No hidden fallback that changes user-selected identity silently.
3. Every saved bust configuration is persisted in database records.
4. Descriptor domains are constrained enums for deterministic rendering and testing.
5. NPC reuse must be seeded and reproducible for fixture-based validation.

## 5. High-Level Feature Set

1. Descriptor domains
- Face shape preset.
- Skin tone preset.
- Hair style and hair color preset.
- Eye style and eye color preset.
- Apparel accent preset.
- Expression preset.

2. Player customization flow
- Start from a canonical default bust preset.
- Apply constrained preset selections with immediate preview.
- Save, cancel, and reset behaviors with explicit user intent.

3. NPC bust reuse
- Assign role/faction preset bands for baseline identity.
- Apply seeded variation for deterministic uniqueness.
- Allow admin-tool manual overrides for selected NPCs while preserving deterministic default generation.
- Rehydrate identical bust output from stored descriptor payload.

4. Browser-safe rendering
- Use lightweight material/texture set and constrained layering.
- Enforce deterministic fallback only for missing optional presentation fields.

## 6. Workstreams

1. Forge contract and persistence updates
- Define SW-15 bust descriptor schema and enum domains.
- Add strict request validation and descriptor normalization.
- Persist playable-character bust descriptor and NPC bust descriptor records with presetVersion/schemaVersion fields.
- Expose read/write endpoints or events for bust configuration lifecycle.

2. Nova bust builder UX and renderer integration
- Build bust builder panel with constrained selector controls.
- Render immediate preview from normalized descriptor payload.
- Wire save/cancel/reset actions against Forge contracts.
- Surface explicit validation and blocked-save reasons from contract responses.

3. Shared deterministic preset and seed policy
- Define canonical defaults for playable-character bust bootstrap.
- Define NPC role/faction preset maps and seed strategy.
- Keep descriptor-to-render mapping pure and fixture-testable.

4. Verification and release guardrails
- Add contract drift checks for domain and shape mismatches.
- Add component and route-level tests for player edit/save/reload.
- Add canary rollout with error-rate and identity-regression monitoring.

## 7. Verification Milestones

M0: Contract baseline and descriptor taxonomy lock
- Deliverables:
1. SW-15 descriptor schema and enum domains approved.
2. Persistence model for player and NPC bust descriptors approved.
- Verification:
1. Intentional enum drift fixture fails hard.
2. Canonical descriptor fixture passes.

M1: Persistence lifecycle implementation
- Deliverables:
1. Playable-character bust create/update/read path implemented.
2. NPC bust preset and seed-backed descriptor storage implemented.
- Verification:
1. Integration tests for save and reload pass.
2. Invalid descriptor writes fail strict validation.

M2: Nova builder interaction baseline
- Deliverables:
1. Selector-driven customization panel functional.
2. Live preview reflects normalized descriptor changes.
3. Save/cancel/reset flows wired end-to-end.
- Verification:
1. Component tests for control-to-preview mapping pass.
2. Route smoke tests for edit and persistence round-trip pass.

M3: NPC reuse and deterministic identity checks
- Deliverables:
1. NPC bust generation uses role/faction preset map + deterministic seed.
2. Reloaded NPC descriptors produce stable bust outputs.
- Verification:
1. Deterministic replay fixture passes for repeated seeds.
2. Cross-session consistency tests pass.

M4: Browser performance and fallback hardening
- Deliverables:
1. Bust preview meets agreed latency and memory thresholds (<150ms median) on desktop and mid-range laptop baseline profiles.
2. Missing-asset fallback remains deterministic and non-destructive.
- Verification:
1. Performance profile checks pass on agreed baseline hardware.
2. Negative fixture confirms no silent identity mutation.

M5: Canary validation
- Deliverables:
1. SW-15 enabled in canary path only.
2. Error and identity-regression telemetry dashboards active.
- Verification:
1. Canary checklist passes.
2. No unresolved P1/P2 incidents during soak window.

M6: Release decision
- Deliverables:
1. Go/no-go record with M0-M5 evidence chain.
2. Closure notes with Forge/Nova sign-off.
- Verification:
1. Planning artifacts index updated.
2. SW-15 marked complete when release gate criteria are met.

## 8. Risks and Mitigations

1. Risk: customization scope balloons into full avatar system.
- Mitigation: enforce constrained preset-only v0 scope.

2. Risk: contract drift causes mismatched renders or save failures.
- Mitigation: strict contract tests, enum drift fixtures, and no-band-aid fallback policy.

3. Risk: identity persistence regressions between sessions.
- Mitigation: persistence round-trip integration tests and seed replay fixtures.

4. Risk: browser performance degradation on preview interactions.
- Mitigation: lightweight asset budget and performance guardrails at M4.

## 9. Exit Criteria

1. Milestones M0-M6 closed with evidence.
2. Playable-character bust customization save/reload works reliably with database persistence using normalized descriptors plus presetVersion/schemaVersion.
3. NPC reuse descriptors are deterministic and reproducible.
4. Contract and renderer behavior are aligned with no silent fallback paths.
5. Canary soak completes without unresolved high-severity incidents.

## 10. Orion Coordination and Handoff Gates

Execution-order baseline for SW-15:
1. Forge locks descriptor contracts and persistence semantics first.
2. Nova integrates builder UX and preview behavior against locked contracts.
3. Forge and Nova complete shared hardening evidence before release decision.

- Orion-managed M0-M6 handoff gate details are maintained in:
- [docs/coordination/sw-15-orion-coordination-runbook.md](../../coordination/sw-15-orion-coordination-runbook.md)
- Nova-Forge milestone choreography details are maintained in:
- [docs/coordination/sw-15-nova-forge-implementation-sequence.md](../../coordination/sw-15-nova-forge-implementation-sequence.md)
