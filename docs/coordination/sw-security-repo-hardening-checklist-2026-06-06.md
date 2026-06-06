# SW Security Repo Hardening Checklist (Nova + Forge)

Status: Active
Date: 2026-06-06
Owner: Orion
Scope: Repository-level controls inside Nova and Forge codebases

## Objective

Establish minimum secure-by-default controls in each repository so source, dependencies, and CI workflows are protected against common compromise paths.

## A. Secrets and Sensitive Data Hygiene

| ID | Control | Nova | Forge | Evidence | Status |
| --- | --- | --- | --- | --- | --- |
| REP-SEC-01 | Add and enforce .gitignore patterns for secret files and local env variants | Pending | Pending | PR link | Pending |
| REP-SEC-02 | Add .env.example files with placeholder values only | Pending | Pending | File path + PR link | Pending |
| REP-SEC-03 | Add secret scanning baseline script/check in CI | Pending | Pending | CI job link | Pending |
| REP-SEC-04 | Rotate any exposed keys/tokens found in git history | Pending | Pending | Rotation ticket reference | Pending |

## B. Dependency and Supply Chain Controls

| ID | Control | Nova | Forge | Evidence | Status |
| --- | --- | --- | --- | --- | --- |
| REP-SEC-05 | Pin runtime/toolchain versions (Node, package manager) | Pending | Pending | Config file links | Pending |
| REP-SEC-06 | Lock dependency graph with committed lockfiles | Pending | Pending | Lockfile path | Pending |
| REP-SEC-07 | Add automated dependency update policy (Dependabot or equivalent) | Pending | Pending | Config file + PR policy | Pending |
| REP-SEC-08 | Add dependency vulnerability scan in CI (fail on high/critical) | Pending | Pending | CI job result | Pending |

## C. CI/CD Workflow Hardening

| ID | Control | Nova | Forge | Evidence | Status |
| --- | --- | --- | --- | --- | --- |
| REP-SEC-09 | Restrict workflow token permissions to least privilege | Pending | Pending | Workflow file diff | Pending |
| REP-SEC-10 | Pin third-party actions by commit SHA | Pending | Pending | Workflow file diff | Pending |
| REP-SEC-11 | Block untrusted workflow execution paths for privileged jobs | Pending | Pending | Workflow policy note | Pending |
| REP-SEC-12 | Separate release/deploy jobs from PR-context jobs | Pending | Pending | Workflow map | Pending |

## D. Code and API Security Gates

| ID | Control | Nova | Forge | Evidence | Status |
| --- | --- | --- | --- | --- | --- |
| REP-SEC-13 | Add CodeQL or equivalent static security analysis | Pending | Pending | Security tab run link | Pending |
| REP-SEC-14 | Add mandatory lint rule set for unsafe patterns | Pending | Pending | Lint config + CI output | Pending |
| REP-SEC-15 | Enforce API schema validation tests for external-facing contracts | Pending | Pending | Test job link | Pending |
| REP-SEC-16 | Add test for authz/authn boundaries where applicable | Pending | Pending | Test case links | Pending |

## E. Release Integrity and Provenance

| ID | Control | Nova | Forge | Evidence | Status |
| --- | --- | --- | --- | --- | --- |
| REP-SEC-17 | Require signed commits or verified identity for protected branches | Pending | Pending | Branch rule screenshot/link | Pending |
| REP-SEC-18 | Generate and retain build artifacts with immutable run links | Pending | Pending | CI artifact policy | Pending |
| REP-SEC-19 | Add release checklist requiring security gate pass | Pending | Pending | Checklist path | Pending |

## Exit Criteria

1. All high-priority controls (REP-SEC-01 to REP-SEC-13) are complete in both repos.
2. No unresolved high/critical dependency vulnerabilities remain open without approved exception.
3. Branch and workflow protections prevent direct unreviewed production-impacting changes.
4. Orion evidence package contains links for each checklist item.
