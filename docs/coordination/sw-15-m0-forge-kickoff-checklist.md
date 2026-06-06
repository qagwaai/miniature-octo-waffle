# SW-15 M0 Forge Kickoff Checklist

Status: Active
Date: 2026-06-05
Owner: Orion
Feature: SW-15 Minimal Character Bust Builder v0
Related sequence: ./sw-15-nova-forge-implementation-sequence.md
Related runbook: ./sw-15-orion-coordination-runbook.md

## How To Use

1. Send the kickoff prompt in this document to Forge.
2. Track each checklist item to done with an evidence link.
3. Orion closes M0 only when every required row is complete.

## Forge Kickoff Prompt (Full URL References)

```text
SW-15 M0 Kickoff Request (Forge)

Objective:
Lock SW-15 M0 contract and persistence baseline so Nova can begin M1+ implementation without schema ambiguity or contract drift.

Source Docs (full URL):
- https://github.com/qagwaai/miniature-octo-waffle/blob/main/docs/coordination/sw-15-nova-forge-implementation-sequence.md
- https://github.com/qagwaai/miniature-octo-waffle/blob/main/docs/coordination/sw-15-orion-coordination-runbook.md
- https://github.com/qagwaai/miniature-octo-waffle/blob/main/docs/coordination/forge-openapi-contract-policy.md
- https://github.com/qagwaai/miniature-octo-waffle/blob/main/docs/planning/sw-15/sw-15-minimal-character-bust-builder-implementation-plan.md

Contract authority (full URL):
- https://github.com/qagwaai/solid-train/blob/main/openapi.yaml

Decision Lock to Implement:
1. Entry surfaces for v0: character creation, in-game profile/customization, and station/clinic interaction.
2. Required domains: face shape, skin tone, hair style/color, eye style/color, expression preset, apparel accent.
3. Persistence payload: normalized descriptor + presetVersion + schemaVersion.
4. NPC model: deterministic baseline + admin-tool manual overrides.
5. Invalid payloads: hard reject with explicit validation errors.
6. Downstream quality target: support Nova validation gate of <150ms median preview updates on desktop and mid-range laptop profiles.
7. No source-of-truth drift: openapi.yaml is authoritative.
8. Entity ownership model: busts are character-scoped (playable-character and NPC), not account-scoped.

M0 Deliverables Required From Forge:
1. openapi.yaml updates for SW-15:
- Bust descriptor schema components.
- Enum domains for all required customization fields.
- Request and response shapes for playable-character bust create/update/read.
- Request and response shapes for NPC bust create/update/read (including deterministic seed and override support).
- Explicit error schema for hard validation rejects.

2. Persistence model baseline:
- Playable-character bust record shape.
- NPC bust record shape.
- Required fields include presetVersion and schemaVersion.
- Normalization semantics documented.

3. Fixture package:
- Canonical pass fixture(s).
- Intentional mismatch fixture(s) that must hard-fail.
- Seed replay fixture for deterministic NPC baseline.

4. Change note:
- Exact impacted endpoints.
- Exact schema/component names.
- Validation and error behavior summary.
- Any migration notes for presetVersion/schemaVersion.

M0 Exit Evidence Needed For Orion Gate:
1. OpenAPI section and component references (exact names).
2. Fixture pass output.
3. Mismatch hard-fail output.
4. Persistence shape confirmation.
5. Ready-for-Nova handoff note.

Handoff Rule:
Nova implementation starts only after Forge M0 contract plus persistence lock evidence is complete.
```

## M0 Checklist Ledger

| ID | Owner | Item | Required Evidence | Status | Evidence Link | Notes |
| --- | --- | --- | --- | --- | --- | --- |
| M0-01 | Forge | SW-15 schema components added in openapi.yaml | OpenAPI component names and PR link | Done | [PR #2](https://github.com/qagwaai/solid-train/pull/2) | 14 new components/schemas: BustDescriptor, BustValidationErrorResponse, 6× CharacterBust*, 6× NpcBust* |
| M0-02 | Forge | Enum domains locked for all required customization fields | Enum table and schema references | Done | [PR #2](https://github.com/qagwaai/solid-train/pull/2) | 8 enum domains locked in bust-descriptor.schema.json and aligned with runtime model in src/model/bust-descriptor.js |
| M0-03 | Forge | Playable-character bust create/update/read request and response shapes locked | Endpoint list and schema references | Done | [PR #2](https://github.com/qagwaai/solid-train/pull/2) | /socket/character-bust-create, /socket/character-bust-read, /socket/character-bust-update |
| M0-04 | Forge | NPC bust create/update/read request and response shapes locked, including deterministic seed and override support | Endpoint list and schema references | Done | [PR #2](https://github.com/qagwaai/solid-train/pull/2) | /socket/npc-bust-create, /socket/npc-bust-read, /socket/npc-bust-update; deterministicSeed + overrides in request schemas |
| M0-05 | Forge | Hard reject validation error schema locked | Error schema reference and example payload | Done | [PR #2](https://github.com/qagwaai/solid-train/pull/2) | BustValidationErrorResponse: success: false, validationErrors[] with field/reason/rejectedValue |
| M0-06 | Forge | Persistence model shape locked for playable-character and NPC records with presetVersion/schemaVersion | Model definition and migration notes | Done | [PR #2](https://github.com/qagwaai/solid-train/pull/2) | Player.characters[].bust embedded subdoc + npc_busts collection; schemaVersion pinned to sw-15-m0-v1; MONGODB_SCHEMA.md updated |
| M0-07 | Forge | Canonical pass fixture package published | Fixture paths and test output | Done | [PR #2](https://github.com/qagwaai/solid-train/pull/2) | test/fixtures/sw15/character-bust-canonical-pass.json; 16/16 tests pass |
| M0-08 | Forge | Intentional mismatch fixture package published and hard-fail verified | Fixture paths and failing output | Done | [PR #2](https://github.com/qagwaai/solid-train/pull/2) | test/fixtures/sw15/character-bust-mismatch-fail.json; faceShape: "triangle" hard-fails with correct rejectedValue |
| M0-09 | Forge | Seed replay fixture published for deterministic NPC baseline | Fixture path and replay output | Done | [PR #2](https://github.com/qagwaai/solid-train/pull/2) | test/fixtures/sw15/npc-bust-seed-replay.json; seed faction:trade\|role:merchant\|id:001 → stable descriptor verified |
| M0-10 | Nova | Fixture compatibility verification completed | Adapter verification note and test output | Done | [Nova PR #2](https://github.com/qagwaai/laughing-octo-journey/pull/2) | Verification note: docs/planning/sw-15/sw-15-m0v-verification-note.md — canonical pass: PASS, mismatch: REJECTED, seed replay: COMPATIBLE, drift scan: no drift found |
| M0-11 | Orion | M0 evidence package reviewed and accepted | Gate note with all evidence links | Done | [Orion M0 Gate Note](#orion-m0-gate-note-2026-06-05) | M0-J signed after Forge PR #2 + Nova PR #2 evidence review |

## Orion M0 Gate Note (2026-06-05)

Decision: Approved, M0 closed.

Evidence reviewed:
1. Forge contract and fixture package complete: [solid-train PR #2](https://github.com/qagwaai/solid-train/pull/2)
2. Nova M0-V fixture compatibility complete: [laughing-octo-journey PR #2](https://github.com/qagwaai/laughing-octo-journey/pull/2)
3. Nova verification note: [docs/planning/sw-15/sw-15-m0v-verification-note.md](../planning/sw-15/sw-15-m0v-verification-note.md)

Gate result:
1. M0-01 through M0-11 complete.
2. No unresolved contract drift findings reported in M0 evidence package.
3. Ready-for-Nova handoff note recorded. M1 execution is authorized.

## M0 Exit Gate

M0 is closed only when:
1. All M0-01 through M0-11 rows are complete.
2. No unresolved contract drift findings are open.
3. Orion records a signed Ready-for-Nova handoff note.
