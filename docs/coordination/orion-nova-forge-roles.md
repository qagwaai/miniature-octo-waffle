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
- Forge `openapi.yaml` is the single contract source of truth for Forge-to-Nova coordination.
- Contract updates in `openapi.yaml` must be detailed enough for Nova implementation without guesswork.

## Shared Architectural Watchpoints

- ship-external-view remains a frequent frontend hotspot.
- stellar-viewer remains a frequent frontend hotspot.
- Contract drift across Nova and Forge should be documented immediately, not deferred.

## Feature Coordination Runbooks

- SW-13 handoff and gate runbook: [docs/coordination/sw-13-orion-coordination-runbook.md](sw-13-orion-coordination-runbook.md)
- SW-15 handoff and gate runbook: [docs/coordination/sw-15-orion-coordination-runbook.md](sw-15-orion-coordination-runbook.md)
- SW-15 Nova-Forge sequence guide: [docs/coordination/sw-15-nova-forge-implementation-sequence.md](sw-15-nova-forge-implementation-sequence.md)
- SW-17 handoff and gate runbook: [docs/coordination/sw-17-orion-coordination-runbook.md](sw-17-orion-coordination-runbook.md)

## Security Coordination Artifacts

- SW security repo hardening checklist: [docs/coordination/sw-security-repo-hardening-checklist-2026-06-06.md](sw-security-repo-hardening-checklist-2026-06-06.md)
- SW GitHub settings security baseline: [docs/coordination/sw-security-github-settings-baseline-2026-06-06.md](sw-security-github-settings-baseline-2026-06-06.md)
- SW security rollout plan: [docs/coordination/sw-security-rollout-plan-2026-06-06.md](sw-security-rollout-plan-2026-06-06.md)
- SW GitHub settings click-path checklist: [docs/coordination/sw-security-github-click-path-checklist-2026-06-06.md](sw-security-github-click-path-checklist-2026-06-06.md)

## Contract Authority

- Forge OpenAPI policy: [docs/coordination/forge-openapi-contract-policy.md](forge-openapi-contract-policy.md)