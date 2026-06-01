# Current Project State

As of 2026-05-30, Orion's current view of Stellar is:

## Project Shape

- Stellar remains a persistent, exploration-first space RPG with a scientifically grounded but playable galaxy.
- Nova owns the frontend surface area and scene readability concerns.
- Forge owns backend simulation, persistence, and contract-producing systems.
- Orion coordinates sequencing, architecture guidance, and cross-repo alignment.

## Current Direction

- The north star still centers on exploration, meaningful decisions, continuity, and consequence-driven progression.
- Horizon 1 remains the immediate focus: foundation hardening, readable spatial UX, and contract confidence.
- Horizon 2 remains the bridge for systems depth: route planning, market pressure, NPC simulation, and progression visibility.

## Immediate Priorities

- SW-R03 is the active regression intake: Expendable Dart Drone fire action is unavailable from Scavenger inventory flow.
- SW-16 remains a high-value continuity fix: preserve ship-external target state on re-entry when the target is still valid.
- SW-01 is still the main clarity win in the short list: Mission Board Status Lanes.

## Foundation Watchpoints

- SW-08 and SW-COR remain the core contract-hardening reference points.
- ship-external-view and stellar-viewer should keep getting periodic decomposition review.
- Any contract mismatch should be treated as a source-of-truth violation rather than patched over with fallback behavior.

## Current Cross-Repo Implementation Order Policy

- For descriptor-first features such as SW-13: Forge locks contract first, Nova builds and integrates second, then both run shared hardening before release decisions.
- No feature moves to release when contract and rendering semantics drift, even if one side appears locally stable.

## SW-13 Coordination Status

- SW-13 is closed as a Stellar Viewer-only rendering and contract pass.
- Deferred follow-on scope is split into SW-13A (ship-external-view support).
- Deferred high-poly fidelity scope is split into SW-13B (Stellar Viewer and ship-external-view).
- Deferred ship-external contract gap closure scope is split into SW-13C (gates, stations, encounter ships).

## Active Near-Term Feature Shape

- SW-02 Market Opportunity Pings.
- SW-03 Quick Dock to Trade Flow.
- SW-05 Ship Condition Badges in Hangar.
- SW-06 Discovery Log v1.
- SW-10 Technology Progress Tree Viewer v0.
- SW-14 In-System Short-Hop Drive.
- SW-17 Computer Progression.

## Current Knowledge Maintenance Rule

- Update this file when priorities change, regressions close, or architectural hotspots shift.
- Keep the snapshot short enough to scan quickly.
- Link to the deeper planning artifacts instead of duplicating them here.