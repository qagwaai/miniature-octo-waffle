# Stellar Brainstorming Findings

Date: 2026-05-24
Session Type: Overarching brainstorming (foundation-first, momentum-aware)
Scope: laughing-octo-journey + solid-train
Primary source: docs/stellar-project-north-star.md

## Session Intent and Constraints

The session goal was to identify feature opportunities for Stellar while keeping Horizon 1 foundation hardening as the priority.

User direction captured:
- Foundation quality and architecture stability are first priority.
- Keep visible gameplay progress and motivating features in the near term.
- Treat this as open-world direction (including future NPC/system interactions).
- Identify small wins now and note longer-term big bets.
- Add autonomous backend NPC actors as a core direction, from small asteroid-belt pirates with single ships to kingpins commanding fleets.

## North Star Alignment Summary

The north-star document defines Stellar as a persistent exploration-first space RPG with:
- Meaningful decisions in exploration, economy, missions, and logistics.
- Scientifically grounded but readable spatial behavior.
- Asynchronous-friendly operations with interpretable return outcomes.
- Consequence-driven progression and continuity over long campaigns.

Most relevant filters used in this brainstorming:
1. Increases meaningful exploration or operations decisions.
2. Preserves or improves spatial/system clarity.
3. Deepens consequence, continuity, or strategic depth.
4. Is contract- and test-validatable in current architecture.
5. Moves a horizon goal forward.

## Cross-Repo Snapshot

### laughing-octo-journey (frontend)

Strengths:
- Broad playable surface area and route/page coverage for game loops.
- Solid domain-service direction around socket interactions.
- Existing mission plugin shape for extending scene behavior.

Primary risks/gaps:
- Testing quality risk from shadow-spec patterns (coverage confidence issue).
- Large complexity hotspot in scene file decomposition needs.
- Spatial UX readability can be improved for clarity under complexity.

Practical implication:
- Prioritize visible player-facing wins that can be implemented without destabilizing scene architecture.
- Pair each feature sprint with at least one testing/contract hardening action.
- Periodically revisit decomposition of ship-external-view and stellar-viewer, since both remain recurring hotspot candidates.

### solid-train (backend)

Strengths:
- Strong economy and market mechanics with deterministic behavior.
- Good handler/service structure and mature automated test base.
- Existing data/logic primitives for routing and location-aware operations.

Primary risks/gaps:
- Centralized context file carries high coordination and change risk.
- Mission progression exists but dynamic/branching mission behavior is still limited.
- Some persistence and lifecycle features (for long-running operations) are still partial.

Practical implication:
- Leverage current stable backend primitives for small wins first.
- Stage larger systemic expansions behind explicit dependency chains.

## Prioritized Feature Opportunities (Small Wins, 1-2 Sprints)

0. High-Priority Regression: Cold Boot Dart Launch Availability (Closed 2026-05-25)
- Symptom: cold boot sequence no longer starts with Expendable Dart Drone available to launch, even though it appears in inventory.
- Expected: cold boot opening flow should allow immediate Dart launch when starting inventory contains expendable dart drone.
- Resolution: restored opening flow so Expendable Dart Drone is available to launch at cold boot.
- Validation: focused tests for inventory-to-launch availability in opening sequence and ship-external launch entry path are now part of regression coverage.

0.1. Continuity Issue: Ship-External Target Persistence on Re-Entry
- Symptom: re-entering ship-external-view does not keep the currently targeted item.
- Expected: when returning to ship-external-view in the same active context, previously selected target should persist if still valid.
- Priority: high continuity fix for interaction flow and player orientation.
- Validation: add tests for target persistence across view exit/re-entry and fallback behavior when prior target is no longer valid.

0.2. Confirmed Regression: Missing Starter Ship Inventory Components (Closed 2026-05-25)
- Symptom: ship inventory is missing expected starter components.
- Missing items: Expendable Dart Drone, Sensor Array, Tractor Beam.
- Expected: starter ship inventory should include canonical opening components so cold-boot and early ship-external actions function.
- Resolution: restored canonical starter ship inventory with Expendable Dart Drone, Sensor Array, and Tractor Beam.
- Validation: startup inventory tests now assert required starter components plus downstream availability in launch/scan/tractor flows.

0.3. New Regression: Expendable Dart Drone Fire Action Unavailable from Scavenger Inventory (Opened 2026-05-25)
- Symptom: Expendable Dart Drone appears in ship inventory view, but the player cannot fire it from Scavenger's inventory path.
- Expected: if Expendable Dart Drone is present in Scavenger's inventory, fire action should be available (matching previously working behavior).
- Priority: critical opening-loop action regression; schedule ahead of same-scope net-new feature work.
- Validation: add tests that assert inventory visibility and fire-action availability parity for Scavenger inventory flow.

Closure note:
- SW-R01 and SW-R02 are complete and moved to historical regression record as of 2026-05-25.
- SW-R03 is now the active opening-loop regression in this cluster.

1. Mission Board Status Lanes
- Add Available / Active / Completed filtering and clearer progression visibility.
- Value: Better mission comprehension and agency with low architecture risk.

2. Market Opportunity Pings
- Surface meaningful market shifts/restocks as lightweight opportunities.
- Value: Immediate economy excitement and better route/timing behavior.

3. Quick Dock to Trade Flow
- Reduce friction between spatial context and market action.
- Value: Strong short-session loop completion and player momentum.

4. Fabrication Queue Timeline (UI-first)
- Show queued/active/completed fabrication jobs with timestamps.
- Value: Tangible industrial progression and continuity feel.

5. Ship Condition Badges in Hangar
- Surface damage/condition state prominently in fleet UX.
- Value: Improves consequence readability and repair decision quality.

6. Discovery Log v1
- Record first-seen bodies, scan milestones, and key discoveries.
- Value: Reinforces wonder-through-discovery and continuity pillars.

7. Spatial Clarity Pack
- Add contextual overlays (distance bands, focus emphasis, legend/help) in key scenes.
- Value: Improves readability without reducing simulation depth.

8. Contract Safety Gate in CI
- Add a pre-merge guard to detect frontend-backend contract drift early.
- Value: Foundation resilience while feature throughput increases.

9. NPC Presence v0 (Backend Runtime Skeleton)
- Introduce a server-side NPC runtime loop with minimal actor archetypes and heartbeat ticks.
- Start with low-complexity pirates (single ship, belt-local behavior) and reserve fleet orchestration for later phases.
- Value: Establishes living-world continuity and enables future risk/economy event hooks.

10. Technology Progress Tree Viewer v0
- Add a player-facing progression tree for item unlock paths with explicit gating criteria.
- Start with mining and fabrication item paths so players can plan upgrade goals.
- Value: Improves progression readability and reduces opaque recipe/tool gating confusion.

11. Character Skills Foundation (Gating-Ready)
- Introduce skill tracks that advance through activity usage (for example mining actions increase Mining skill).
- Use skill level thresholds to gate higher-tier tools (for example Tier 2 drill requires Mining level N).
- Value: Adds consequence-driven mastery and long-term identity continuity.

12. Minimal Ship-to-Ship Encounter v0
- Add a constrained combat surface focused on interdiction, escape, and cargo theft instead of full ship destruction.
- Keep shields minimal and outcomes harsh so the game communicates that space is hard and unforgiving.
- Allow pirates to threaten cargo holds without killing the pilot, while making dart drone impacts decisively lethal to the drone.
- Value: Introduces survival pressure and piracy interactions without turning Stellar into a combat-first game.

13. External Object Presentation Expansion
- Extend ship-external-view to render detailed debris meshes, jump gates, other ship silhouettes, and space stations with clearer identity and scale.
- Use progressive detail so important objects read well at game distance without flooding the scene with clutter.
- Expand asteroid look from rocky irregular profiles to cinematic hero-style variants; reduce over-spherical repetition.
- Keep implementation data-driven (descriptor-first) with balanced-performance fallbacks and no legacy presentation mode.
- Value: Makes external space feel populated and legible, and supports future encounter and travel systems.

SW-13 high-level feature description:
1. Debris mesh identity
- Debris families should visibly communicate salvage category/value at a glance.

2. Ship silhouette families
- Ships should be distinguishable by role/faction silhouette under normal gameplay distance.

3. Jump gate landmark treatment
- Gate visuals should be unmistakable for navigation and approach decisions.

4. Station landmark treatment
- Stations should read as durable infrastructure, not background noise.

5. Asteroid style spectrum
- Fields should include both rough rocky bodies and occasional cinematic hero asteroids.

6. Delivery guardrails
- Keep scene architecture close to current structure.
- Do not perform a full 3D asset overhaul in SW-13.
- Enforce full cutover with no legacy support paths.

Implementation plan reference:
- `docs/planning/sw-13/sw-13-external-object-presentation-implementation-plan.md`

14. In-System Short-Hop Drive
- Introduce a low-level drive that enables practical travel between planets and major bodies inside a solar system.
- Charge fuel for each hop so movement remains strategic instead of free, and so route planning still matters.
- Value: Prevents in-system travel from becoming a long-duration blocker while preserving logistics and resource pressure.

15. Minimal Character Bust Builder v0 (Separate Track)
- Add a browser-friendly character builder focused on bust-level identity, not full-body customization.
- Prioritize high-value controls: facial structure presets, skin tone variation, tattoos, and scars.
- Keep this as a separate implementation track because of its higher 3D asset/runtime budget.
- Value: Strengthens identity and continuity, and can be reused for NPC portrait/bust presentation.

16. Computer Progression (Per-Ship Intelligence Tiers)
- Add a per-ship installable computer module that unlocks better intelligence features across 10 progression tiers.
- Installation is gated by character skill progression plus character level thresholds.
- Keep assistance mostly advisory with opt-in light automation for low-risk actions.
- Value: strengthens planning, threat awareness, and route economy decisions without reducing player agency.