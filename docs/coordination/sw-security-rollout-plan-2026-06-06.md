# SW Security Rollout Plan (Nova + Forge)

Status: Active
Date: 2026-06-06
Owner: Orion
Window: 7-day hardening sprint

## Goal

Deliver high-impact security controls quickly across repository internals and GitHub settings with minimal delivery disruption.

## Day 0 - Decision Lock

1. Confirm security owner(s) for Nova and Forge.
2. Confirm branch policy requirements and review minimums.
3. Freeze exceptions policy for high/critical vulnerabilities.

## Day 1-2 - GitHub Settings Baseline

1. Apply 2FA enforcement and access cleanup.
2. Apply branch protections/rulesets on main and release branches.
3. Enable security features: secret scanning, push protection, Dependabot, code scanning.
4. Harden Actions permissions and third-party action pinning policy.

Success criteria:
1. GH-SEC-01 through GH-SEC-06 are enabled in both repositories.

## Day 2-4 - Repo Internal Hardening

1. Add or tighten secret hygiene patterns and env examples.
2. Add dependency vulnerability and static analysis checks in CI.
3. Add API schema and security-oriented regression checks.
4. Add release integrity and security checklist gates.

Success criteria:
1. REP-SEC-01 through REP-SEC-13 complete in both repositories.

## Day 4-6 - Validate and Burn Down Findings

1. Triage all findings from dependency and code scanning runs.
2. Fix or formally waive with dated exception and owner.
3. Re-run CI/security scans until gates are green.

Success criteria:
1. No open critical findings without approved exception.
2. No branch/workflow bypass path without explicit owner sign-off.

## Day 7 - Closure

1. Produce Orion closure note with evidence links.
2. Create monthly security cadence tasks.
3. Lock baseline as required for future milestone gate progression.

## Metrics

1. High/critical vulnerabilities open count.
2. Median time to remediate security alerts.
3. Secret leak incidents per month.
4. Protected-branch bypass events per month.

## Ready or Blocked Statement Template

Ready:
1. Baseline controls are active in both repos and evidence is complete.

Blocked:
1. List missing GH-SEC or REP-SEC IDs, owners, and due dates.
