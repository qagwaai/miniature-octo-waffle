# SW-15 M2-A1 Orion Execution Plan

Status: Ready to Implement
Date: 2026-06-05
Owner: Orion
Feature Slice: SW-15 M2-A1 Higher-Fidelity Angular Three Character Preview

## Intake Answers

1. Performance targets: Desktop >=55 FPS, mobile >=30 FPS, viewer first render <=1500ms.
2. Bust model source path: src/assets/models/characters/busts/sw15/.
3. Camera presets: Front, Three-quarter, Left profile, Right profile.
4. Touch constraints: single-finger drag rotate, pinch zoom with clamps, inertial spin disabled, reset orientation required.
5. Test depth: Extended (focused + mobile interaction + performance assertions).
6. Risks/unknowns: none additional declared.

## Finalized Scope

Locked and accepted for M2-A1:
1. Goal: Higher-fidelity Angular Three character preview in Create Character.
2. Render source: form state only.
3. Interactions: drag rotate + zoom + preset camera buttons.
4. Asset strategy: new dedicated bust model at src/assets/models/characters/busts/sw15/.
5. Required gates: desktop + mobile render reliability, selector-to-3D mapping correctness, deterministic unit + e2e coverage, performance threshold compliance.
6. M2-A semantics must not regress: blocked-save, validation, retry behavior remain unchanged.

## Execution Plan

### Step 1 - Add dedicated viewer component boundary

Files:
1. src/app/page/character/components/character-bust-viewer/character-bust-viewer.ts
2. src/app/page/character/components/character-bust-viewer/character-bust-viewer.html
3. src/app/page/character/components/character-bust-viewer/character-bust-viewer.css
4. src/app/page/character/components/character-bust-viewer/character-bust-viewer.spec.ts

Actions:
1. Implement isolated Angular Three viewer component.
2. Accept typed input view-model only (descriptor + interaction config + camera preset state).
3. Expose output events for camera preset changes and viewer readiness telemetry.

Acceptance criteria:
1. No direct socket or persistence logic in viewer component.
2. Viewer component can render solely from provided form-state derived descriptor.

### Step 2 - Add dedicated bust model assets and loader configuration

Files:
1. src/assets/models/characters/busts/sw15/ (new model + texture assets)
2. src/app/page/character/components/character-bust-viewer/character-bust-viewer.ts

Actions:
1. Load dedicated bust model from locked path.
2. Apply fallback failure state that is explicit and non-silent.
3. Record first-render timing for threshold assertions.

Acceptance criteria:
1. Asset path is exactly src/assets/models/characters/busts/sw15/.
2. Viewer fails explicitly if model unavailable; no silent replacement behavior.

### Step 3 - Wire Create Character orchestration to viewer via adapter boundary

Files:
1. src/app/page/character/character-setup.ts
2. src/app/page/character/character-setup.html
3. src/app/page/character/character-setup.css
4. src/app/page/character/character-setup.spec.ts

Actions:
1. Derive viewer input model from form state only.
2. Mount viewer component and camera preset buttons.
3. Keep blocked-save/validation/retry UI and flow intact.

Acceptance criteria:
1. Selector change updates 3D preview deterministically.
2. Existing blocked-save and validation terminal states remain behaviorally unchanged.

### Step 4 - Implement interaction controls and constraints

Files:
1. src/app/page/character/components/character-bust-viewer/character-bust-viewer.ts
2. src/app/page/character/components/character-bust-viewer/character-bust-viewer.spec.ts

Actions:
1. Desktop: pointer drag rotate + wheel zoom with clamp.
2. Mobile: single-finger rotate, pinch zoom clamp, no inertia, reset orientation action.
3. Add camera presets: front, three-quarter, left profile, right profile.

Acceptance criteria:
1. Touch interactions follow constraints exactly.
2. Camera preset actions are deterministic and idempotent.

### Step 5 - Extend deterministic tests and regressions

Files:
1. src/app/page/character/components/character-bust-viewer/character-bust-viewer.spec.ts
2. src/app/page/character/character-setup.spec.ts
3. src/app/services/bust-descriptor-adapter.service.spec.ts
4. e2e/tests/character-add.spec.ts
5. e2e/tests/character-edit.spec.ts

Actions:
1. Add selector-to-3D mapping assertions.
2. Add blocked-save/validation non-regression checks.
3. Add mobile interaction e2e checks for rotate/zoom/reset.
4. Add performance assertions using deterministic telemetry thresholds.

Acceptance criteria:
1. Unit/component and e2e tests pass deterministically.
2. Existing character-add/edit flows remain green.

## Verification Gates

1. Reliability gate:
- Viewer renders on desktop and mobile without runtime errors.

2. Mapping gate:
- All eight selector fields map deterministically to 3D preview state.

3. Interaction gate:
- Drag rotate, pinch zoom clamps, camera presets, and reset orientation verified.

4. Performance gate:
- Desktop >=55 FPS median in interaction scenario.
- Mobile >=30 FPS median in interaction scenario.
- First render <=1500ms.

5. Regression gate:
- Blocked-save/validation/retry semantics unchanged from M2-A.
- Character add/edit + starter-ship bootstrap flows remain intact.

## Go or No-Go

Go.

Rationale:
1. Inputs are fully specified.
2. Scope is bounded and compatible with existing M2-A lock.
3. Acceptance thresholds and test depth are explicit.
