# SW-15 M2-A Nova Prompt

Status: Ready to Send
Date: 2026-06-05
Owner: Orion
Feature: SW-15 Minimal Character Bust Builder v0
Scope: Nova M2-A (builder baseline integration against locked Forge semantics)

## Prompt (Full URL References)

```text
SW-15 M2-A Integration Request (Nova)

Objective:
Execute Nova M2-A against locked Forge response semantics so M2 interaction work can proceed without contract drift, semantic ambiguity, or client-side compensation.

Execution mode:
- Scope: Nova M2-A only
- Goal: consume locked semantics in adapter/UI interaction baseline safely
- Drift policy: source-fix only; no Nova-side band-aids

Source Docs (full URL):
- https://github.com/qagwaai/miniature-octo-waffle/blob/main/docs/coordination/sw-15-nova-forge-implementation-sequence.md
- https://github.com/qagwaai/miniature-octo-waffle/blob/main/docs/coordination/sw-15-orion-coordination-runbook.md
- https://github.com/qagwaai/miniature-octo-waffle/blob/main/docs/planning/sw-15/sw-15-minimal-character-bust-builder-implementation-plan.md
- https://github.com/qagwaai/miniature-octo-waffle/blob/main/docs/coordination/forge-openapi-contract-policy.md

Forge semantic lock input (full URL):
- https://github.com/qagwaai/miniature-octo-waffle/blob/main/docs/coordination/sw-15-m2a-forge-verification-note-2026-06-05.md

Contract authority (full URL):
- https://github.com/qagwaai/solid-train/blob/main/openapi.yaml

M2-A Sequence Target:
- Build selector controls and live preview binding against normalized payload model while consuming locked response semantics for:
  1. Hard-reject validation error responses
  2. Blocked-save reason responses (BustBlockedSaveResponse)
  3. Normalized create/update payload echoes

Decision Lock To Preserve:
1. Character-scoped ownership only (playable-character and NPC), no account-level source-of-truth.
2. Persistence payload shape remains normalized descriptor plus presetVersion/schemaVersion.
3. Invalid payloads remain hard-rejected with explicit validationErrors entries.
4. Locked blockedSave.reason semantics are consumed exactly as contract-defined.

Nova M2-A Deliverables:
1. Interaction baseline wiring
- Implement selector-driven customization baseline for playable-character and NPC flows.
- Bind live preview updates to normalized descriptor payloads only.

2. Response-semantic handling
- Handle hard-reject validation responses via field/reason/rejectedValue mapping.
- Handle blocked-save responses with typed reason and retryable semantics.
- Ensure successful normalized responses do not carry blockedSave or validationErrors in success path handling.

3. Contract conformance checks
- Confirm request/response handling matches OpenAPI components including BustBlockedSaveResponse.
- Confirm no inferred fields or assumption-based fallback logic is introduced.

4. Drift handling
- Report any mismatch as contract drift with source ownership assignment.
- Do not merge compensating behavior for contract mismatches.

Required Evidence For Orion M2-A Gate:
1. Nova M2-A verification note containing:
- Endpoints exercised
- Schema/component names exercised
- Selector/preview baseline integration summary
- Validation and blocked-save handling summary
- Drift status and source-routing notes

2. Test evidence summary containing:
- Component/unit checks for control-to-preview mapping
- Negative-path checks for hard-reject validation handling
- Blocked-save handling checks for reason + retryable semantics

3. Handoff note:
- Explicit statement that Nova M2-A is complete and ready for Orion M2 gate intake

Acceptance Criteria:
1. Nova consumes locked M2-A semantics without drift.
2. No unresolved contract drift findings remain open.
3. No Nova-side compensating behavior masks contract mismatches.
4. Evidence package is sufficient for Orion M2 status update and gate progression.

Out of scope:
1. M2-B full save/cancel/reset interaction flow completion.
2. M3 NPC presentation and deterministic replay visual behavior.
3. Any Forge contract redefinition outside source authority.
```
