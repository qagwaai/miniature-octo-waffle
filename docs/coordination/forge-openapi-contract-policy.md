# Forge OpenAPI Contract Policy

Status: Active
Date: 2026-05-30
Owner: Orion

## Policy Statement

Forge-to-Nova coordination uses one contract source of truth:

- Forge repository OpenAPI file: `openapi.yaml`
- Repo URL: https://github.com/qagwaai/solid-train/blob/main/openapi.yaml

No parallel contract source is authoritative for Forge-to-Nova integration.

## Required Rules

1. Contract-first sequencing is mandatory.
- Forge updates `openapi.yaml` first.
- Nova implementation starts against the updated OpenAPI contract.

2. Contract detail is mandatory.
- Request and response schemas must be explicit enough for Nova implementation without guesswork.
- Field types, enums, required fields, nullable behavior, and error shapes must be defined.

3. No shadow contracts.
- Ad hoc docs, comments, or payload examples cannot override `openapi.yaml`.
- If implementation differs from OpenAPI, treat as contract drift and fix at source.

4. Drift blocks release.
- Any Forge/Nova behavior not represented in `openapi.yaml` is a release blocker until corrected.

5. Change visibility.
- Every feature handoff must cite the exact OpenAPI sections or schema names used.

## Definition of Ready (Forge -> Nova)

Before Nova starts implementation, Forge must provide:

1. Updated `openapi.yaml` merged or in review-ready PR.
2. Explicit schema updates for any new or changed payload fields.
3. Example payloads consistent with OpenAPI schemas.
4. A short change note listing impacted endpoints and schema components.

## Definition of Done (Joint)

1. Nova implementation aligns with `openapi.yaml`.
2. Contract tests or fixtures confirm payload conformance.
3. No unresolved drift findings remain.

## SW-13 Application Note

For SW-13, descriptor schema and enum taxonomy decisions must map to Forge contract definitions before Nova finalizes selector/render behavior.