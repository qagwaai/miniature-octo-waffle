# SW-15 M2-A1 Nova Handoff Prompt

Status: Ready to Send
Date: 2026-06-05
Owner: Orion

## Prompt (Full URL References)

```text
SW-15 M2-A1 Implementation Request (Nova)

Objective:
Implement M2-A1 higher-fidelity Angular Three preview slice for Create Character while preserving M2-A terminal behavior semantics and contract conformance.

Source docs (full URL):
- https://github.com/qagwaai/miniature-octo-waffle/blob/main/docs/coordination/sw-15-m2a1-orion-execution-plan-2026-06-05.md
- https://github.com/qagwaai/miniature-octo-waffle/blob/main/docs/coordination/sw-15-nova-forge-implementation-sequence.md
- https://github.com/qagwaai/miniature-octo-waffle/blob/main/docs/coordination/sw-15-orion-coordination-runbook.md
- https://github.com/qagwaai/miniature-octo-waffle/blob/main/docs/coordination/forge-openapi-contract-policy.md

M2-A references (full URL):
- https://github.com/qagwaai/miniature-octo-waffle/blob/main/docs/coordination/sw-15-m2a-forge-verification-note-2026-06-05.md
- https://github.com/qagwaai/miniature-octo-waffle/blob/main/docs/coordination/sw-15-m2a-nova-verification-note-2026-06-05.md

Contract authority (full URL):
- https://github.com/qagwaai/solid-train/blob/main/openapi.yaml

Locked M2-A1 decisions:
1. Performance: desktop >=55 FPS, mobile >=30 FPS, first render <=1500ms.
2. Bust model path: src/assets/models/characters/busts/sw15/.
3. Camera presets: front, three-quarter, left profile, right profile.
4. Touch constraints: single-finger rotate, pinch zoom clamps, no inertia, reset orientation required.
5. Test depth: extended (unit/component + mobile interaction + performance assertions).

Implementation constraints:
1. Isolate 3D viewer behind dedicated component boundary.
2. Render source must be form state only.
3. Keep blocked-save/validation/retry behavior unchanged.
4. Do not add fallback bandaids for contract mismatches.

Required implementation files (ordered):
1. src/app/page/character/components/character-bust-viewer/character-bust-viewer.ts
2. src/app/page/character/components/character-bust-viewer/character-bust-viewer.html
3. src/app/page/character/components/character-bust-viewer/character-bust-viewer.css
4. src/app/page/character/components/character-bust-viewer/character-bust-viewer.spec.ts
5. src/app/page/character/character-setup.ts
6. src/app/page/character/character-setup.html
7. src/app/page/character/character-setup.css
8. src/app/page/character/character-setup.spec.ts
9. src/assets/models/characters/busts/sw15/
10. e2e/tests/character-add.spec.ts
11. e2e/tests/character-edit.spec.ts

Required evidence for Orion intake:
1. Verification note with endpoints/components exercised and drift statement.
2. Unit/component test results including selector-to-3D mapping.
3. E2E test results including mobile interaction checks.
4. Performance evidence proving thresholds.
5. Handoff note with explicit Ready/Blocked decision.

Stop condition:
If any contract mismatch appears, stop and report source-of-truth violation to Orion. Do not patch with client fallback behavior.
```
