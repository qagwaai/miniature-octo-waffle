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

## Scope

In scope:
1. High-poly readiness matrix for debris, ships, gates, stations, and asteroids.
2. Surface parity checks for high-poly behavior in Stellar Viewer and ship-external-view.
3. Proxy mapping policy with owners and dated replacement commitments where assets are missing.
4. Canary burn-down tracking for proxy replacement and visual fidelity gaps.

Out of scope:
1. New descriptor schema families unless explicitly approved by Orion.
2. Renderer architecture rewrite.

## High-Poly Sourcing Strategy

Use a staged sourcing funnel so SW-13B can deliver predictable quality without blocking milestones.

Priority order:
1. Internal library reuse (existing project assets upgraded or re-authored).
2. Licensed third-party marketplace acquisition.
3. Custom commissioned assets for gaps that cannot be met by options 1 or 2.

Family coverage targets:
1. Debris: hero salvage silhouettes and material variance sets.
2. Ships: role and faction readable hero silhouettes.
3. Gates: landmark-grade meshes with strong framing profiles.
4. Stations: long-range readable structural identity sets.
5. Asteroids: irregular hero variants with non-repetitive profiles.

## Source Channels and Governance

Approved channels:
1. Internal source repositories with documented ownership.
2. Curated asset marketplaces with commercial-use licenses.
3. Approved external vendors under written work-for-hire or equivalent transfer terms.

Governance rules:
1. Every sourced asset must have a provenance record: source, license, owner, acquisition date.
2. Every sourced asset must map to one SW-13 family and at least one target surface.
3. Assets lacking clear commercial rights are rejected.
4. Assets with unclear modification rights are rejected.

## Acceptance Gates for Sourced Assets

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

## Sourcing Risks and Mitigations

1. Risk: licensing mismatch discovered late.
- Mitigation: reject assets without explicit commercial and modification rights during intake.

2. Risk: visual style fragmentation across mixed sources.
- Mitigation: enforce family-level art direction checks before integration.

3. Risk: assets meet quality but fail runtime budgets.
- Mitigation: require technical validation and LOD readiness before approval.

4. Risk: proxy debt persists into release.
- Mitigation: enforce owner assignment, dated replacement commitments, and canary burn-down reporting.

## Milestones

M0B: Asset readiness baseline
- Publish high-poly matrix with owner, status, and target replacement dates.
- Publish sourcing channel and licensing status for each matrix row.

M1B: Stellar Viewer high-poly pass
- Verify high-poly readiness and fallback behavior in Stellar Viewer.

M2B: ship-external-view high-poly pass
- Verify high-poly readiness and fallback behavior in ship-external-view.

M3B: Dual-surface parity pass
- Validate visual identity parity and fallback equivalence across both surfaces.

M4B: Canary fidelity pass
- Run canary telemetry and issue triage focused on high-poly and proxy burn-down.

## Exit Criteria

1. High-poly readiness is complete or explicitly tracked through approved proxy commitments.
2. No unresolved P1/P2 visual-fidelity issues linked to missing high-poly support.
3. Dual-surface fidelity behavior is consistent with Orion acceptance criteria.
4. Contract behavior remains aligned with Forge openapi.yaml and SW-13 family semantics.
