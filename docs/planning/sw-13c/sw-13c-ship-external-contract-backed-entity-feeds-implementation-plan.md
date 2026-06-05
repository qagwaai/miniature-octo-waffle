# SW-13C Ship-External Contract-Backed Entity Feeds Implementation Plan (Nova + Forge)

Status: Closed
Date: 2026-05-31
Repos: laughing-octo-journey (Nova), solid-train (Forge)
Feature ID: SW-13C
Predecessors: SW-13A (ship-external-view support), SW-13B (high-poly support)

## Objective

Close the remaining ship-external-view coverage gaps by introducing contract-backed entity feeds for gates, stations, and non-player ships so Nova can validate and render those families without synthetic client-side stand-ins.

## Scope

In scope:
1. Optional `gates[]` entity feed for ship-external route payloads.
2. Optional `stations[]` entity feed for ship-external route payloads.
3. Optional `encounterShips[]` entity feed for ship-external route payloads.
4. Nova route-model and renderer updates to consume the new feeds deterministically.
5. Fixtures, route-smoke tests, and ambiguity/readability evidence for the new feeds.

Out of scope:
1. New high-poly asset sourcing policy (tracked in SW-13B).
2. New descriptor family semantics beyond the existing SW-13 baseline unless Orion approves them.
3. Client-side synthetic stand-ins used as a substitute for contract-backed entities.

## Contract Gap Closure Strategy

SW-13C is a contract and payload expansion feature. Nova-only rendering cannot close the coverage gap without Forge-backed entity streams.

Gap closure sequence:
1. Forge adds the missing entity feeds to the ship-external route contract and payload source.
2. Nova consumes the feeds in route models and scene selection.
3. Orion validates evidence on contract-backed gates, stations, and encounter ships.

## Milestones

M0C: Contract gap definition and payload shape lock
- Confirm entity feed names, payload shapes, and descriptor requirements.
- Confirm optionality and compatibility with existing route payloads.

M1C: Gate feed implementation
- Add contract-backed gate entities to ship-external route payloads.
- Validate gate landmark rendering and ambiguity checks in Nova.

M2C: Station feed implementation
- Add contract-backed station entities to ship-external route payloads.
- Validate station readability and route-smoke coverage in Nova.

M3C: Encounter ship feed implementation
- Add contract-backed non-player ship entities to ship-external route payloads.
- Validate ship-family readability and deterministic fallback behavior in Nova.

M4C: Dual-surface coverage and canary pass
- Validate that the new feeds work in ship-external-view and remain compatible with Stellar Viewer contract expectations.
- Run canary telemetry and issue triage for unresolved gaps.

## Exit Criteria

1. Gates, stations, and encounter ships are provided as contract-backed ship-external route entities.
2. Nova no longer relies on synthetic client-side stand-ins for those families.
3. Route-smoke and ambiguity/readability evidence is available for all new feeds.
4. Forge contract and payload changes remain backward-compatible or are versioned with Orion approval.
5. No contract drift from the established SW-13 family semantics.
