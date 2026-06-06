# SW-15 M1 Forge Kickoff Prompt

Status: Ready to Send
Date: 2026-06-05
Owner: Orion
Feature: SW-15 Minimal Character Bust Builder v0

## Prompt (Full URL References)

```text
SW-15 M1 Kickoff Request (Forge)

Objective:
Execute M1 Persistence Lifecycle for SW-15 with contract-safe, character-scoped persistence behavior and zero contract drift from the M0 baseline.

Source Docs (full URL):
- https://github.com/qagwaai/miniature-octo-waffle/blob/main/docs/coordination/sw-15-nova-forge-implementation-sequence.md
- https://github.com/qagwaai/miniature-octo-waffle/blob/main/docs/coordination/sw-15-orion-coordination-runbook.md
- https://github.com/qagwaai/miniature-octo-waffle/blob/main/docs/coordination/sw-15-m0-forge-kickoff-checklist.md
- https://github.com/qagwaai/miniature-octo-waffle/blob/main/docs/planning/sw-15/sw-15-minimal-character-bust-builder-implementation-plan.md

M0 closure reference (full URL):
- https://github.com/qagwaai/miniature-octo-waffle/blob/main/docs/coordination/sw-15-m0-forge-kickoff-checklist.md#orion-m0-gate-note-2026-06-05

Contract authority (full URL):
- https://github.com/qagwaai/solid-train/blob/main/openapi.yaml

M1 Sequence Targets:
1. Forge M1-A: Implement create/update/read lifecycle for playable-character bust descriptor.
2. Forge M1-B: Implement preset and seed-backed lifecycle for NPC bust descriptor.
3. Forge M1-C: Enforce validation and normalization on all write paths and return explicit hard-reject validation errors for invalid payloads.

Decision Lock To Preserve:
1. Bust ownership remains character-scoped (playable-character + NPC), never account-scoped.
2. Persistence payload remains normalized descriptor + presetVersion + schemaVersion.
3. Invalid payload handling remains hard reject with explicit validation error shape.
4. Deterministic NPC seed behavior remains reproducible and fixture-verifiable.

M1 Deliverables Required From Forge:
1. Persistence lifecycle implementation
- Playable-character bust create/read/update fully wired and persisted.
- NPC bust create/read/update fully wired and persisted.
- SchemaVersion and presetVersion persisted on writes and returned on reads.

2. Validation and normalization behavior
- Invalid enum/domain/value writes hard-rejected with explicit validationErrors[] output.
- Valid writes normalized consistently with deterministic output semantics.

3. Contract alignment update
- openapi.yaml updated only if behavior/shape changed from M0 lock.
- If no shape changes, provide explicit no-drift confirmation note.

4. Integration verification package
- Save -> read round-trip tests for playable-character bust lifecycle.
- Save -> read round-trip tests for NPC bust lifecycle.
- Negative tests for invalid-write rejection with expected field/reason/rejectedValue evidence.

5. Evidence note
- List exact endpoints exercised.
- List exact schema/component names exercised.
- State whether any drift was discovered and how it was resolved at source.

Exit Evidence Needed For Orion M1 Gate Review:
1. PR link(s) with implementation scope summary.
2. Round-trip integration test output for playable-character and NPC paths.
3. Negative validation test output for hard-reject behavior.
4. Contract no-drift confirmation (or explicit OpenAPI updates with references).
5. Ready-for-Nova M1-V handoff note.

Handoff Rule:
Nova M1-V adapter integration may proceed in parallel only after endpoint and schema signatures are confirmed stable for M1-A and M1-B.

Non-negotiables:
1. No Nova-side compensating behavior should be required to consume M1 payloads.
2. No silent correction path for invalid payloads.
3. No account-level bust source-of-truth introduced.
```
