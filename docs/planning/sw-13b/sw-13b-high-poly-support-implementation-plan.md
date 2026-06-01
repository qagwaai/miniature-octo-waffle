# SW-13B High-Poly Support Implementation Plan (Nova + Forge + Content)

Status: Draft (Execution Ready)
Date: 2026-05-31
Repos: laughing-octo-journey (Nova), solid-train (Forge)
Feature ID: SW-13B
Predecessors: SW-13 (Stellar Viewer only), SW-13A (ship-external-view support)

Companion spec:
- [SW-13B Asteroid Generator Specification](sw-13b-asteroid-generator-spec.md)

## Objective

Deliver high-poly hero-asset readiness for external object presentation across Stellar Viewer and ship-external-view without introducing contract drift.

Asteroid family exception: SW-13B asteroids are delivered through code-based generation in Nova, not sourced through marketplace or commissioned asset channels.

## Scope

In scope:
1. High-poly readiness matrix for debris, ships, gates, stations, and asteroids.
2. Surface parity checks for high-poly behavior in Stellar Viewer and ship-external-view.
3. Proxy mapping policy with owners and dated replacement commitments where sourced assets are missing.
4. Canary burn-down tracking for proxy replacement and visual fidelity gaps.
5. Asteroid generation registry and seed coverage tracking for code-generated asteroid outputs.

Out of scope:
1. New descriptor schema families unless explicitly approved by Orion.
2. Renderer architecture rewrite.

## High-Poly Sourcing Strategy

Use a staged sourcing funnel so SW-13B can deliver predictable quality without blocking milestones.

Asteroid exception:
1. The staged sourcing funnel applies to debris, ships, gates, and stations.
2. Asteroids are excluded from sourcing and are generated in code by Nova according to the companion asteroid generator spec.

Priority order:
1. Internal library reuse (existing project assets upgraded or re-authored).
2. Licensed third-party marketplace acquisition.
3. Custom commissioned assets for gaps that cannot be met by options 1 or 2.

Family coverage targets:
1. Debris: hero salvage silhouettes and material variance sets.
2. Ships: role and faction readable hero silhouettes.
3. Gates: landmark-grade meshes with strong framing profiles.
4. Stations: long-range readable structural identity sets.
5. Asteroids: irregular baseline and hero variants produced through deterministic code generation with seed governance.

## Source Channels and Governance

Approved channels:
1. Internal source repositories with documented ownership.
2. Curated asset marketplaces with commercial-use licenses.
3. Approved external vendors under written work-for-hire or equivalent transfer terms.
4. Asteroids are not sourced from approved channels and must be generated through the Nova runtime generator path.

Governance rules:
1. Every sourced asset must have a provenance record: source, license, owner, acquisition date.
2. Every sourced asset must map to one SW-13 family and at least one target surface.
3. Assets lacking clear commercial rights are rejected.
4. Assets with unclear modification rights are rejected.

## Acceptance Gates for Sourced Assets

Applies to non-asteroid families only.

Technical acceptance:
1. Imports cleanly into project pipeline without format workarounds.
2. Includes LOD strategy compatible with fallback policy.
3. Meets agreed budget envelopes for memory and frame-time impact in representative scenes.

Visual acceptance:
1. Family identity is readable at gameplay distance.
2. Asset does not collapse into existing silhouettes at target camera ranges.
3. Material and shape language remains consistent with the Stellar direction.

Operational acceptance:
1. Owner is assigned for fixes and replacement lifecycle.
2. Proxy replacement date is recorded when final hero asset is deferred.
3. Canary triage tags are defined for each asset family.

## Sourcing Workflow

1. Demand definition
- Orion and Nova define required hero asset slots per family and per surface.

2. Candidate intake
- Content owner collects candidates from approved channels with provenance data.

3. Triage and scoring
- Score candidates on readability fit, technical fit, legal fit, and cost or lead time.

4. Technical validation
- Run import and performance probes in both Stellar Viewer and ship-external-view.

5. Approval and assignment
- Orion approves selected candidates, assigns owners, and records replacement commitments when proxies are used.

6. Integration and evidence
- Nova integrates accepted assets and publishes family and surface evidence for M1B through M4B.

7. Canary burn-down
- Track unresolved fidelity gaps and close proxy debt against dated commitments.

## Asteroid Code-Generation Workflow

1. Generator definition and lock
- Orion and Nova lock seed taxonomy, profile presets, and parameter bundles.

2. Runtime implementation
- Nova implements deterministic runtime generation for both Stellar Viewer and ship-external-view paths.

3. Validation and evidence
- Nova publishes deterministic reproducibility evidence, parity evidence, and performance evidence by seed set.

4. Registry and coverage reporting
- Orion and Nova publish and maintain asteroid generation registry and seed coverage table through M0B to M4B.

## Sourcing Risks and Mitigations

1. Risk: licensing mismatch discovered late.
- Mitigation: reject assets without explicit commercial and modification rights during intake.

2. Risk: visual style fragmentation across mixed sources.
- Mitigation: enforce family-level art direction checks before integration.

3. Risk: assets meet quality but fail runtime budgets.
- Mitigation: require technical validation and LOD readiness before approval.

4. Risk: proxy debt persists into release.
- Mitigation: enforce owner assignment, dated replacement commitments, and canary burn-down reporting.

5. Risk: runtime generator divergence across surfaces.
- Mitigation: enforce deterministic seed governance, shared parameter bundle hashes, and parity validation in M1B-M3B.

6. Risk: generated asteroids exceed runtime budget in dense scenes.
- Mitigation: enforce per-seed performance probes and fail gates before milestone sign-off.

## Milestones

M0B: Asset readiness baseline
- Publish high-poly matrix with owner, status, and target replacement dates for sourced families.
- Publish sourcing channel and licensing status for each non-asteroid sourced matrix row.
- Publish asteroid generation registry with seed IDs, generator version, and parameter bundle hashes.
- Publish asteroid seed coverage table by profile, material, and target surface.

M1B: Stellar Viewer high-poly pass
- Verify high-poly readiness and fallback behavior in Stellar Viewer.
- Verify runtime code-generated asteroid behavior and determinism in Stellar Viewer.

M2B: ship-external-view high-poly pass
- Verify high-poly readiness and fallback behavior in ship-external-view.
- Verify runtime code-generated asteroid behavior and determinism in ship-external-view.

M3B: Dual-surface parity pass
- Validate visual identity parity and fallback equivalence across both surfaces.
- Validate asteroid seed parity across surfaces using shared registry records.

M4B: Canary fidelity pass
- Run canary telemetry and issue triage focused on high-poly and proxy burn-down.
- Run canary telemetry and issue triage for generated asteroid fidelity and runtime budget stability.

## Exit Criteria

1. High-poly readiness is complete or explicitly tracked through approved proxy commitments.
2. No unresolved P1/P2 visual-fidelity issues linked to missing high-poly support.
3. Dual-surface fidelity behavior is consistent with Orion acceptance criteria.
4. Contract behavior remains aligned with Forge openapi.yaml and SW-13 family semantics.
5. Asteroid family has no marketplace or commissioned asset dependencies for SW-13B.
6. Asteroid generation registry and seed coverage table are published and current.
