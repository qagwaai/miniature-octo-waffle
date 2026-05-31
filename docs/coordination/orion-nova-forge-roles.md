# Orion, Nova, and Forge Roles

This document defines the working boundary for the Stellar coordination model.

## Orion

- Owns cross-repo strategy and sequencing.
- Keeps the shared Stellar direction coherent.
- Maintains repository-level knowledge and current-state snapshots.
- Calls out architectural hotspots and coordination dependencies.

## Nova

- Owns frontend implementation in laughing-octo-journey.
- Focuses on player-facing readability, interaction flow, and scene decomposition.
- Keeps UI changes aligned with the north star and contract shape.

## Forge

- Owns backend implementation in solid-train.
- Focuses on simulation, persistence, and server-side contract integrity.
- Keeps data and runtime behavior stable for shared gameplay flows.

## Coordination Rules

- Keep ownership explicit in planning notes.
- Put the source of truth closest to the system that actually controls the behavior.
- Prefer source fixes over compensating fallbacks.
- Record validation paths for anything that touches contracts, state transitions, or gameplay-critical loops.

## Shared Architectural Watchpoints

- ship-external-view remains a frequent frontend hotspot.
- stellar-viewer remains a frequent frontend hotspot.
- Contract drift across Nova and Forge should be documented immediately, not deferred.