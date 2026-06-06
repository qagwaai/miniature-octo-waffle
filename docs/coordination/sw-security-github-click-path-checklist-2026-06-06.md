# SW GitHub Settings Click-Path Checklist (Nova + Forge)

Status: Active
Date: 2026-06-06
Owner: Orion
Scope: Manual GitHub settings hardening for repositories and org-level controls

## Repositories

1. Nova: https://github.com/qagwaai/laughing-octo-journey
2. Forge: https://github.com/qagwaai/solid-train

## Usage

1. Apply each section to Nova, then Forge.
2. Capture evidence links/screenshots as you go.
3. Mark each checklist row complete before moving to the next section.

## A. Repository Security and Analysis Features

Navigation path:
1. Repo home -> Settings -> Security -> Advanced Security.

Steps:
1. Enable Dependabot alerts.
2. Enable Dependabot security updates.
3. Enable secret scanning.
4. Enable push protection for secrets.
5. Enable code scanning default setup if not already configured.

Verification:
1. Repo -> Security tab shows active alerts/scanning sections.
2. Repo -> Settings -> Security settings show all toggles enabled.

## B. Branch Protection / Rulesets

Navigation path:
1. Repo home -> Settings -> Rules -> Rulesets.

Steps:
1. Create or update ruleset targeting main and release branches.
2. Require pull request before merge.
3. Require at least 1 reviewer minimum (set 2 where high-risk changes apply).
4. Require status checks to pass.
5. Require conversation resolution.
6. Block force pushes and branch deletion.
7. Restrict direct pushes to protected branches.

Verification:
1. Ruleset appears active and assigned to target branches.
2. Test PR reflects required checks and reviewer gate.

## C. Required Status Checks Baseline

Navigation path:
1. Repo home -> Settings -> Rules -> Rulesets -> selected ruleset.

Steps:
1. Add required CI checks for tests/build/lint/security.
2. For Forge include contract/schema checks.
3. For Nova include unit/e2e baseline checks used in SW-15 flows.

Verification:
1. Required checks list is populated.
2. Merge is blocked when required checks fail.

## D. Actions and Workflow Hardening

Navigation path:
1. Repo home -> Settings -> Actions -> General.

Steps:
1. Set Actions permissions to allow only approved actions/reusable workflows.
2. Set default GITHUB_TOKEN permissions to read repository contents.
3. Require explicit permission elevation per workflow job.
4. Review workflows for third-party actions and pin them to commit SHA.

Verification:
1. Actions policy reflects restricted mode.
2. Workflow files show pinned action refs and least-privilege token scopes.

## E. Environment Protections (If Deploy Environments Exist)

Navigation path:
1. Repo home -> Settings -> Environments.

Steps:
1. For each deploy environment, require reviewers.
2. Restrict deployment branches/tags.
3. Use environment secrets (avoid broad repo secrets where possible).

Verification:
1. Environments show reviewer and branch protections.
2. Deployment requires approvals where configured.

## F. Collaborators and Team Access Review

Navigation path:
1. Repo home -> Settings -> Collaborators and teams.

Steps:
1. Remove direct user admin grants unless required.
2. Prefer team-based permissions.
3. Review outside collaborator access.
4. Remove stale/inactive access.

Verification:
1. Admin access limited to designated owners.
2. Team permissions align with least-privilege model.

## G. Organization-Level Controls (qagwaai)

Navigation path:
1. Org home -> Settings -> Security.

Steps:
1. Enforce organization-wide 2FA.
2. Review and tighten OAuth app and GitHub App restrictions.
3. Review personal access token policies (fine-grained preferred).
4. Enable org-level secret scanning and push protection where available.

Verification:
1. 2FA enforcement is enabled.
2. App/token policy reflects approved access only.

## H. Evidence Capture Template

| ID | Repo | Control | Evidence URL | Screenshot Saved | Status | Notes |
| --- | --- | --- | --- | --- | --- | --- |
| GHCP-01 | Nova | Security features enabled | TBD | No | Pending | |
| GHCP-02 | Nova | Ruleset/branch protection active | TBD | No | Pending | |
| GHCP-03 | Nova | Actions restrictions + token policy | TBD | No | Pending | |
| GHCP-04 | Nova | Environment protections configured | TBD | No | Pending | |
| GHCP-05 | Nova | Collaborator/team access reviewed | TBD | No | Pending | |
| GHCP-06 | Forge | Security features enabled | TBD | No | Pending | |
| GHCP-07 | Forge | Ruleset/branch protection active | TBD | No | Pending | |
| GHCP-08 | Forge | Actions restrictions + token policy | TBD | No | Pending | |
| GHCP-09 | Forge | Environment protections configured | TBD | No | Pending | |
| GHCP-10 | Forge | Collaborator/team access reviewed | TBD | No | Pending | |
| GHCP-11 | Org | 2FA and org security controls reviewed | TBD | No | Pending | |

## Completion Criteria

1. All GHCP-01 through GHCP-11 entries are complete with evidence.
2. Both repos block direct unreviewed merges to protected branches.
3. Secret scanning and push protection are active in both repos.
4. Actions permissions and workflow hardening are verified.
