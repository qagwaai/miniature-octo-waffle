# SW-13B High-Poly Support Implementation Plan (Nova + Forge + Content)

Status: Draft (Execution Ready)
Date: 2026-05-31
Repos: laughing-octo-journey (Nova), solid-train (Forge)
Feature ID: SW-13B
Predecessors: SW-13 (Stellar Viewer only), SW-13A (ship-external-view support)

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

## Milestones

M0B: Asset readiness baseline
- Publish high-poly matrix with owner, status, and target replacement dates.

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
