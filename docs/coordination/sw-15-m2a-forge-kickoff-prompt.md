# SW-15 M2-A Forge Kickoff Prompt

Status: Ready to Send
Date: 2026-06-05
Owner: Orion
Feature: SW-15 Minimal Character Bust Builder v0
Scope: Forge M2-A (response semantics lock)

## Prompt (Full URL References)

```text
SW-15 M2-A Kickoff Request (Forge)

Objective:
Lock M2-A response semantics for SW-15 so Nova can execute M2 interaction work against stable validation, blocked-save, and normalized payload behavior with no contract drift.

Execution mode:
- Scope: Forge M2-A only
- Goal: response semantics lock, not UI behavior
- Drift policy: source-fix only, no downstream compensating behavior

Source Docs (full URL):
- https://github.com/qagwaai/miniature-octo-waffle/blob/main/docs/coordination/sw-15-nova-forge-implementation-sequence.md
- https://github.com/qagwaai/miniature-octo-waffle/blob/main/docs/coordination/sw-15-orion-coordination-runbook.md
- https://github.com/qagwaai/miniature-octo-waffle/blob/main/docs/planning/sw-15/sw-15-minimal-character-bust-builder-implementation-plan.md
- https://github.com/qagwaai/miniature-octo-waffle/blob/main/docs/coordination/forge-openapi-contract-policy.md

Prior milestone closure inputs (full URL):
- https://github.com/qagwaai/miniature-octo-waffle/blob/main/docs/coordination/sw-15-m1-forge-verification-note-2026-06-05.md
- https://github.com/qagwaai/miniature-octo-waffle/blob/main/docs/coordination/sw-15-m1-orion-gate-note-2026-06-05.md

Contract authority (full URL):
- https://github.com/qagwaai/solid-train/blob/main/openapi.yaml

M2-A Sequence Target:
- Freeze response semantics for:
  1. Validation error responses (hard-reject path)
  2. Blocked-save reason responses
  3. Normalized payload echo responses

Decision Lock To Preserve:
1. Character-scoped ownership only (playable-character and NPC), no account-level source-of-truth.
2. Persistence payload shape remains normalized descriptor plus presetVersion/schemaVersion.
3. Invalid payloads remain hard-rejected with explicit validationErrors entries.
4. Endpoint and schema naming remains stable unless explicitly contract-updated.

M2-A Deliverables Required From Forge:
1. Validation error semantics lock
- Confirm final response shape for hard-reject validation responses.
- Confirm field/reason/rejectedValue behavior remains deterministic and stable.

2. Blocked-save reason semantics lock
- Define and lock blocked-save reason structure for Nova consumer handling.
- Ensure blocked-save reasons are explicit, typed, and contract-defined.

3. Normalized payload echo semantics lock
- Define and lock what fields are echoed after create/update operations.
- Ensure normalized responses are deterministic and schema-conformant.

4. Contract alignment updates
- Update openapi.yaml if any M2-A semantics differ from existing documented response behavior.
- If no changes are required, provide explicit no-drift/no-shape-change declaration.

5. Verification package
- Targeted tests proving locked semantics for validation errors, blocked-save reasons, and normalized echoes.
- Include at least one intentional mismatch case confirming hard-reject behavior.

6. Evidence note
- Endpoint list exercised.
- Schema/component names exercised.
- Contract drift status and source resolution notes.
- Explicit Ready-for-Nova-M2-A handoff statement.

Exit Evidence Needed For Orion M2-A Gate Intake:
1. Forge PR link(s) with M2-A scope summary.
2. Test output showing semantic lock behavior.
3. OpenAPI references or no-drift declaration.
4. M2-A verification note artifact URL.

Handoff Rule:
Nova M2-A should not finalize UI interaction logic until Forge M2-A semantic lock evidence is complete and accepted.

Non-negotiables:
1. No silent semantic changes outside OpenAPI/source evidence.
2. No weakening of hard-reject invalid payload behavior.
3. No schema drift hidden behind runtime normalization.
```
