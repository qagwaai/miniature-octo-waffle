# SW-13B Nova Asteroid Code-Generation Implementation Plan (Nova + Content)

Status: Draft (Execution Ready)
Date: 2026-06-01
Repo: laughing-octo-journey (Nova)
Feature ID: SW-13B
Predecessors: SW-13 (Stellar Viewer only), SW-13A (ship-external-view support)

Companion artifacts:
- [SW-13B Asteroid Generator Specification](sw-13b-asteroid-generator-spec.md)
- [SW-13B High-Poly Support Implementation Plan](sw-13b-high-poly-support-implementation-plan.md)

## Objective

Deliver SW-13B asteroid high-poly support through deterministic, code-based runtime generation in Nova for Stellar Viewer and ship-external-view.

## Policy Lock

1. Asteroid assets for SW-13B are code-generated only.
2. Marketplace asteroid assets are not allowed.
3. Commissioned asteroid assets are not allowed.
4. Canonical mineable material source remains the Material column in the shared materials CSV.

## Scope

In scope:
1. Runtime procedural asteroid generation in Nova for both surfaces.
2. Deterministic seed governance and reproducible parameter bundles.
3. Seed coverage planning by profile, material, and target surface.
4. LOD and runtime performance validation in representative asteroid-dense scenes.
5. M0B-M4B evidence publication for registry, determinism, parity, and canary burn-down.

Out of scope:
1. Non-asteroid SW-13B families (debris, ships, gates, stations).
2. Forge runtime generation.
3. New API/schema families unless explicitly approved by Orion.

## Ownership and Working Model

1. Orion:
- Owns prioritization, milestone acceptance, and cross-team communication.

2. Nova:
- Owns generator implementation, deterministic behavior, runtime performance, and evidence publication.

3. Content:
- Owns profile intent validation and visual-language sign-off on generated outputs.

4. Forge:
- No asteroid asset sourcing work for SW-13B under this plan.
- If any contract change is later required, update Forge openapi.yaml in the same change pass.

## Delivery Workstreams

### W0: Seed and Preset Lock

1. Lock seed taxonomy and profile preset targets.
2. Lock initial parameter bundle ranges per baseline and hero tiers.
3. Define required minimum seed counts by profile and material.

Outputs:
- Seed taxonomy lock note
- Profile preset lock note
- Initial parameter bundle registry entries

### W1: Runtime Generator Implementation

1. Implement deterministic generation path for Stellar Viewer.
2. Implement deterministic generation path for ship-external-view.
3. Ensure order-stable random stream and explicit generator versioning.

Outputs:
- Generator module merged in Nova
- Generator versioning policy note

### W2: Registry and Coverage System

1. Publish asteroid generation registry with required metadata fields.
2. Publish seed coverage table by profile, material, and target surface.
3. Track gaps with named owners and target closure milestone.

Required registry fields:
1. seedId
2. generatorVersion
3. parameterBundleHash
4. profilePreset
5. targetSurfaces
6. validationStatus
7. owner

### W3: Validation and Performance

1. Determinism validation across repeated runs for the same seed.
2. Dual-surface parity validation for identity and fallback behavior.
3. Runtime budget probes in asteroid-dense scenarios.
4. LOD transition quality checks under representative camera motion.

Outputs:
- Determinism evidence pack
- Surface parity evidence pack
- Performance evidence pack

### W4: Canary and Burn-Down

1. Track unresolved visual and runtime issues through canary tags.
2. Prioritize P1/P2 issues by impact to readability, parity, or frame budget.
3. Close seed coverage and validation gaps against dated commitments.

Outputs:
- Canary issue board snapshot
- Burn-down status note per milestone

## Milestones

M0B: Baseline and Registry
- Publish seed taxonomy and initial profile preset set.
- Publish asteroid generation registry (seed IDs, generator version, parameter bundle hashes).
- Publish seed coverage table by profile, material, and target surface.
- Publish initial gap list with owners and target closure dates.

M1B: Stellar Viewer Runtime Pass
- Validate deterministic asteroid generation in Stellar Viewer.
- Confirm baseline and hero profile readability and fallback behavior in Stellar Viewer.

M2B: ship-external-view Runtime Pass
- Validate deterministic asteroid generation in ship-external-view.
- Confirm baseline and hero profile readability and fallback behavior in ship-external-view.

M3B: Dual-Surface Parity Pass
- Validate seed parity for identity semantics across both surfaces.
- Validate equivalent fallback behavior across both surfaces.

M4B: Canary Fidelity and Performance Pass
- Run canary triage for unresolved generated-asteroid fidelity issues.
- Run canary triage for runtime budget regressions in dense scenes.
- Close remaining seed coverage and validation debt or record approved carryover.

## Risks and Mitigations

1. Risk: generator divergence between surfaces.
- Mitigation: lock shared seed and parameter bundle inputs; enforce parity checks in M1B-M3B.

2. Risk: runtime budget regression under dense asteroid scenes.
- Mitigation: enforce milestone fail gates using representative performance probes.

3. Risk: profile output drift from intended visual language.
- Mitigation: require Content sign-off on profile exemplars per milestone.

4. Risk: seed coverage gaps remain late in cycle.
- Mitigation: publish owner-based gap tracker in M0B and burn down every milestone.

## Exit Criteria

1. Asteroid delivery is fully code-generated in Nova with no marketplace or commissioned dependencies.
2. Registry and seed coverage tables are published and current.
3. Determinism and dual-surface parity evidence passes Orion acceptance criteria.
4. No unresolved P1/P2 issues for generated-asteroid fidelity or runtime budget stability.
5. Any required backend contract change is reflected in Forge openapi.yaml in the same change pass.

## M0B Decision Lock (2026-06-01)

These decisions were confirmed for the first Nova asteroid M0B execution wave:

1. Coverage target:
- Balanced coverage with baseline and hero seed presence across SV and SEV.

2. Material scope:
- Include all canonical materials in M0B.

3. Determinism strictness:
- Strict evidence required: repeated runs, cross-surface consistency, and cross-environment consistency.

4. Performance gate mode:
- Soft warning gate for dense asteroid scenes in M0B.

5. Gap ownership model:
- Every unresolved gap must have one Nova owner and one Content reviewer.

6. Communication style:
- Directive execution brief for Nova handoff.

## Nova M0B Prompt Template

Use this prompt to initiate execution with Nova:

"Execute SW-13B M0B asteroid baseline under the code-generation-only policy using these reference docs:
- https://github.com/<org>/<repo>/blob/<branch>/docs/planning/sw-13b/sw-13b-asteroid-generator-spec.md
- https://github.com/<org>/<repo>/blob/<branch>/docs/planning/sw-13b/sw-13b-high-poly-support-implementation-plan.md
- https://github.com/<org>/<repo>/blob/<branch>/docs/planning/sw-13b/sw-13b-nova-asteroid-codegen-implementation-plan.md

Apply locked decisions:
- Balanced coverage with baseline and hero seed presence across SV and SEV.
- All canonical materials included in M0B.
- Strict determinism evidence: repeated runs + cross-surface + cross-environment consistency.
- Soft warning performance gate for dense asteroid scenes.
- Unresolved gaps assigned to one Nova owner and one Content reviewer.

Publish (1) asteroid generation registry with seedId, generatorVersion, parameterBundleHash, profilePreset, targetSurfaces, validationStatus, owner, and contentReviewer; (2) seed coverage table by profile, material, and target surface; (3) strict determinism evidence pack; (4) runtime performance baseline with warning thresholds and flagged scenes; and (5) initial gap list with owners/reviewers and target closure dates. Confirm no marketplace or commissioned asteroid dependencies." 
