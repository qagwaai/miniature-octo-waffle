# SW-15 M1-V Nova Prompt

Status: Ready to Send
Date: 2026-06-05
Owner: Orion
Feature: SW-15 Minimal Character Bust Builder v0

## Prompt (Full URL References)

```text
SW-15 M1-V Adapter Integration Request (Nova)

Objective:
Complete Nova M1-V integration against Forge M1 persistence lifecycle and produce gate-quality evidence for Orion M1-J review, with zero contract drift and no compensating client-side behavior.

Execution mode:
- Scope: M1-V adapter integration and verification
- Contract policy: Forge openapi.yaml is source of truth
- Drift policy: source-fix only; no Nova-side band-aids

Source Docs (full URL):
- https://github.com/qagwaai/miniature-octo-waffle/blob/main/docs/coordination/sw-15-nova-forge-implementation-sequence.md
- https://github.com/qagwaai/miniature-octo-waffle/blob/main/docs/coordination/sw-15-orion-coordination-runbook.md
- https://github.com/qagwaai/miniature-octo-waffle/blob/main/docs/planning/sw-15/sw-15-minimal-character-bust-builder-implementation-plan.md
- https://github.com/qagwaai/miniature-octo-waffle/blob/main/docs/coordination/forge-openapi-contract-policy.md

Forge M1 evidence input (full URL):
- https://github.com/qagwaai/miniature-octo-waffle/blob/main/docs/coordination/sw-15-m1-forge-verification-note-2026-06-05.md

Contract authority (full URL):
- https://github.com/qagwaai/solid-train/blob/main/openapi.yaml

M1-V Sequence Target:
- Integrate Nova adapter layer for load/save paths against stable M1 endpoint and schema signatures for:
  - /socket/character-bust-create
  - /socket/character-bust-read
  - /socket/character-bust-update
  - /socket/npc-bust-create
  - /socket/npc-bust-read
  - /socket/npc-bust-update

Decision Lock To Preserve:
1. Bust ownership is character-scoped (playable-character + NPC), not account-scoped.
2. Persistence payload remains normalized descriptor + presetVersion + schemaVersion.
3. Invalid payloads are hard-rejected and surfaced with explicit validationErrors.
4. NPC deterministic seed behavior remains reproducible and replay-safe.

Nova M1-V Deliverables:
1. Adapter integration completion
- Wire create/read/update adapter paths for playable-character bust lifecycle.
- Wire create/read/update adapter paths for NPC bust lifecycle.
- Consume normalized responses without introducing inferred fields.

2. Error-path integration
- Surface hard reject validation errors cleanly to Nova consumers.
- Preserve field/reason/rejectedValue mapping fidelity.

3. Contract conformance verification
- Confirm request/response payloads match OpenAPI component expectations used in M1.
- Confirm no data-shape assumptions outside published schema.

4. Drift scan and source-routing
- Report any endpoint/schema mismatch as drift.
- Route drift to Forge contract source; do not merge compensating behavior.

Required Evidence For Orion M1 Gate:
1. Verification note in Nova repo docs with:
- Endpoints exercised
- Schema/component names exercised
- Adapter integration summary for character and NPC paths
- Drift status and source-routing notes

2. Test evidence summary with:
- Round-trip compatibility checks for character and NPC flows
- Negative-path checks proving hard reject handling on invalid payloads

3. Handoff note:
- Explicitly state whether Nova M1-V is ready for Orion M1-J gate close

Acceptance Criteria:
1. Nova M1-V adapter integration complete for both playable-character and NPC paths.
2. No unresolved contract drift findings remain open.
3. No Nova-side fallback/normalization workaround masks contract mismatches.
4. Evidence package is sufficient for Orion M1 gate review.

Out of scope:
1. M2 UI interaction behavior (selector controls, save/cancel/reset UX).
2. M3 NPC presentation behavior beyond M1 adapter compatibility.
3. Any contract redefinition outside Forge source of truth.
```
