# SW-13A Ship-External-View Support Implementation Plan (Nova + Forge)

Status: Draft (Execution Ready)
Date: 2026-05-31
Repo: laughing-octo-journey (Nova)
Related repo: solid-train (Forge)
Feature ID: SW-13A
Predecessor: SW-13 (closed as Stellar Viewer only)

## Objective

Implement descriptor-driven external object presentation in ship-external-view using the SW-13 contract baseline already validated in Stellar Viewer.

## Scope

In scope:
1. ship-external-view integration for debris, ships, gates, stations, and asteroids.
2. Route-smoke and recognition-distance checks in ship-external-view.
3. Fallback behavior validation in ship-external-view.

Out of scope:
1. High-poly asset readiness and proxy burn-down policy (moved to SW-13B).
2. Contract schema expansion beyond SW-13 baseline unless Orion approves version change.

## Milestones

M0A: Surface baseline lock
- Confirm ship-external-view integration boundaries and test harness.

M1A: Family integration pass
- Integrate descriptor-driven rendering for all SW-13 families in ship-external-view.

M2A: Landmark and ambiguity pass
- Validate gate landmark readability and ambiguity regression behavior.

M3A: Performance and fallback pass
- Confirm deterministic fallback behavior and dense-scene stability for ship-external-view.

M4A: Canary and release recommendation
- Run ship-external-view canary evidence and produce go or no-go recommendation.

## Exit Criteria

1. ship-external-view supports descriptor-driven rendering for SW-13 families.
2. Recognition and ambiguity evidence meets Orion thresholds.
3. Fallback behavior remains deterministic with no identity collapse.
4. No contract drift from Forge openapi.yaml baseline.
