# SW GitHub Settings Security Baseline (Nova + Forge)

Status: Active
Date: 2026-06-06
Owner: Orion
Scope: GitHub organization/repository settings outside code

## Objective

Define the minimum GitHub-side security posture for Nova and Forge repositories.

## 1. Access and Identity Controls

1. Require organization-wide 2FA for all members and outside collaborators.
2. Use teams, not direct user grants, for repo access where possible.
3. Remove admin rights from day-to-day contributors unless operationally required.
4. Review dormant/inactive accounts and revoke stale access monthly.

## 2. Branch Protection Rules

Apply to main and release branches in both repos:
1. Require pull request before merge.
2. Require at least 2 approvals for sensitive paths and 1 minimum globally.
3. Dismiss stale approvals on new commits.
4. Require conversation resolution before merge.
5. Require status checks to pass before merge.
6. Require branch up-to-date before merge.
7. Block force pushes and branch deletion.
8. Restrict who can push to protected branches.

## 3. Rulesets and File Path Protections

1. Add ruleset for workflow files under .github/workflows/ requiring senior review.
2. Add ruleset for security policy/config files requiring Orion or security-owner review.
3. Add CODEOWNERS enforcement for high-risk paths.

## 4. Security and Analysis Features

Enable for both repos:
1. Dependabot alerts.
2. Dependabot security updates.
3. Secret scanning.
4. Push protection for secrets.
5. Code scanning with default setup or custom CodeQL workflow.
6. Private vulnerability reporting where applicable.

## 5. Pull Request and Merge Hygiene

1. Disable merge methods that bypass review policy if not needed.
2. Require linear history or squash-only policy (pick one and enforce).
3. Enable auto-delete branches after merge.
4. Require signed commits if team workflow supports it.

## 6. Actions and Workflow Security

1. Restrict GitHub Actions to approved actions and reusable workflows.
2. Require full-length commit SHA pinning for third-party actions.
3. Default workflow permissions to read-only and elevate only per job.
4. Restrict self-hosted runner groups by repository and environment.
5. Require environment protection rules for production deploy environments.

## 7. Token and Secret Governance

1. Prefer environment-scoped secrets over repo-wide secrets for deployment credentials.
2. Replace long-lived personal access tokens with GitHub Apps or fine-grained tokens.
3. Rotate all sensitive secrets on a fixed cadence and after personnel changes.
4. Add incident playbook for leaked secret response.

## 8. Audit and Monitoring

1. Enable and review audit logs weekly.
2. Track security alert MTTR and open critical alert count.
3. Track branch protection bypass events and require post-incident review.

## Verification Checklist

| ID | Control | Nova | Forge | Evidence | Status |
| --- | --- | --- | --- | --- | --- |
| GH-SEC-01 | 2FA enforcement enabled | Pending | Pending | Settings screenshot/link | Pending |
| GH-SEC-02 | Branch protection/rulesets configured | Pending | Pending | Rule links | Pending |
| GH-SEC-03 | Secret scanning + push protection enabled | Pending | Pending | Settings screenshot/link | Pending |
| GH-SEC-04 | Dependabot alerts + updates enabled | Pending | Pending | Security settings link | Pending |
| GH-SEC-05 | Code scanning enabled and running | Pending | Pending | Code scanning run link | Pending |
| GH-SEC-06 | Actions restricted and SHA pinning policy enforced | Pending | Pending | Actions settings + workflow diff | Pending |
| GH-SEC-07 | Environment protection rules enabled | Pending | Pending | Environment settings link | Pending |
| GH-SEC-08 | Token/secret rotation policy documented | Pending | Pending | Policy link | Pending |
