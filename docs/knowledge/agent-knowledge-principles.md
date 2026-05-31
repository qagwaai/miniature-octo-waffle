# Agent Knowledge Principles

Orion should treat this repository as a durable working memory for the Stellar project.

## Best Practices

1. Keep one source of truth per concern.
- North star for direction.
- Current-state docs for live priorities and risks.
- Planning docs for ranked near-term work.
- Coordination docs for role boundaries and handoffs.

2. Prefer explicit summaries over implicit recall.
- Record what is true now, why it is true, and what would change it.
- Add the validation path for major claims when it matters.

3. Keep state and history separate.
- Current-state documents should be easy to scan and refresh.
- Historical planning artifacts should stay dated and preserved.
- Do not bury active regressions inside broad planning notes.

4. Make cross-repo responsibility visible.
- Orion handles strategy, sequencing, and synthesis.
- Nova handles frontend and scene-facing implementation concerns.
- Forge handles backend, persistence, and simulation concerns.

5. Treat contract drift as a source-of-truth problem.
- Prefer source fixes over fallback behavior.
- Keep contract language specific enough to validate.
- Preserve the actual decision chain, not just the symptom.

6. Revisit architectural hotspots on a cadence.
- ship-external-view remains a recurring review point.
- stellar-viewer remains a recurring review point.
- When a hotspot reappears, document the reason and the preferred seam.

## What This Repository Is For

- Durable architectural notes.
- Shared project state across Orion, Nova, and Forge.
- Planning artifacts that should survive sprint churn.
- Explicit reminders about the current Stellar direction.

## What This Repository Is Not For

- Ephemeral scratch notes.
- One-off implementation dumps.
- Unversioned decision guesses.
- Replacing the source repos for Nova or Forge.