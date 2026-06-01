# SW-13B Asteroid Generator Specification

Status: Draft (Execution Ready)
Date: 2026-05-31
Owner: Orion with Nova + Content implementation
Feature: SW-13B High-Poly Support

## Purpose

Define a deterministic asteroid generation specification for SW-13B that supports:
1. Multiple mineable raw-material families sourced from the canonical materials catalog.
2. Hero variants for landmark-grade visual moments.
3. Reproducible outputs across Stellar Viewer and ship-external-view.

## Generation Model

Primary model:
1. Start mesh: high-subdivision icosphere.
2. Macro displacement: low-frequency layered noise for silhouette.
3. Meso detail: medium-frequency noise for ridge and shelf structures.
4. Micro detail: high-frequency noise for small surface roughness.
5. Crater pass: subtractive crater masks with depth and rim controls.
6. Erosion pass: directional smoothing and edge break-up.
7. Material zone pass: assign masks for rock strata, metallic inclusions, and dusted zones.
8. Base material pass: select one canonical raw material from the materials catalog and apply its shading and breakup bias.

Pipeline mode:
1. Offline generation and bake (not runtime procedural generation in Forge).
2. Deterministic seed-driven output for exact reproducibility.

## Canonical Material Source

The base-material catalog is the Material column in [laughing-octo-journey/docs/Stellar mineable raw elements - Mineable Materials.csv](c:\Development\Projects\Github\laughing-octo-journey\docs\Stellar%20mineable%20raw%20elements%20-%20Mineable%20Materials.csv).

The generator must treat that file as the source of truth for allowed base materials, including future additions or renames.

## Seed Taxonomy

Seed format:
- Family-Surface-Tier-Material-Profile-Ordinal-Revision
- Example: AST-SV-B-Carbon-RK-042-r1

Seed tokens:
1. Family:
- AST = asteroid

2. Surface target:
- SV = Stellar Viewer
- SEV = ship-external-view
- DS = dual-surface validated

3. Tier:
- B = rocky baseline
- H = hero

4. Material:
- Carbon
- Iron
- Copper
- Magnesium
- Nickel
- Silicon
- Lithium
- Mercury
- Chromium
- Tungsten
- Titanium
- Silver
- Cobalt
- Palladium
- Uranium
- Iridium
- Platinum
- Gold
- Rhodium
- Antimony
- Unobtainium

5. Profile:
- RK = rocky irregular
- SH = shelf-ridge
- CR = crater-heavy
- FR = fractured-boulder
- MT = metallic-vein
- DS = dusty smooth
- SP = spined shard
- PN = pancake slab
- HO = hollow pocket
- GL = glassy fused
- BR = broken ring
- NK = knotted cluster

6. Ordinal:
- 001-999 sequence within profile

7. Revision:
- r1, r2, r3...

Seed governance rules:
1. A seed ID must always map to one frozen parameter bundle.
2. Parameter bundle changes require revision bump.
3. Hero seeds must have dual-surface validation before approval.
4. Deprecated seeds remain in registry with superseded status.

## Parameter Specification

All ranges are normalized unless stated otherwise.

### Global Parameters

1. baseRadiusMeters
- Rocky baseline: 20-180
- Hero: 120-420

2. axisStretchXYZ
- Rocky baseline: x,y,z each 0.80-1.30
- Hero: x,y,z each 0.65-1.45

3. macroNoiseAmplitude
- Rocky baseline: 0.10-0.28
- Hero: 0.18-0.40

4. macroNoiseFrequency
- Rocky baseline: 0.7-2.2
- Hero: 0.5-1.8

5. mesoNoiseAmplitude
- Rocky baseline: 0.05-0.16
- Hero: 0.08-0.24

6. mesoNoiseFrequency
- Rocky baseline: 2.0-6.5
- Hero: 1.8-5.5

7. microNoiseAmplitude
- Rocky baseline: 0.01-0.06
- Hero: 0.015-0.08

8. microNoiseFrequency
- Rocky baseline: 8-22
- Hero: 6-18

### Crater Parameters

1. craterCount
- Rocky baseline: 2-18
- Hero: 8-42

2. craterRadiusRatio
- Rocky baseline: 0.03-0.18 of local asteroid radius
- Hero: 0.05-0.30 of local asteroid radius

3. craterDepthRatio
- Rocky baseline: 0.08-0.35 of crater radius
- Hero: 0.12-0.55 of crater radius

4. craterRimHeightRatio
- Rocky baseline: 0.02-0.12 of crater radius
- Hero: 0.04-0.20 of crater radius

5. craterClustering
- Rocky baseline: 0.00-0.35
- Hero: 0.10-0.60

### Fracture and Erosion Parameters

1. fracturePasses
- Rocky baseline: 0-2
- Hero: 1-4

2. fractureIntensity
- Rocky baseline: 0.00-0.25
- Hero: 0.10-0.45

3. erosionStrength
- Rocky baseline: 0.08-0.30
- Hero: 0.05-0.24

4. edgeSharpness
- Rocky baseline: 0.30-0.75
- Hero: 0.35-0.85

### Material Zone Parameters

1. metallicVeinCoverage
- Rocky baseline: 0.00-0.10
- Hero: 0.02-0.18

2. dustCoverage
- Rocky baseline: 0.10-0.55
- Hero: 0.08-0.45

3. albedoVariance
- Rocky baseline: 0.08-0.30
- Hero: 0.12-0.40

### Base Material Parameters

1. materialSlug
- Must be a normalized representation of the CSV Material value.
- Use the canonical material name in metadata and a safe slug in filenames if required by the exporter.

2. materialBiasMap
- Derived from the canonical CSV entry, especially rarity, primary use, mining requirement, and typical location.
- Default implementation should bias darker, dustier, or more metallic shading based on the selected material row rather than an invented composition class.

## Profile Presets

### Rocky Baseline Presets

1. RK-Field-01
- Target: common belt filler
- Parameter intent: moderate macro shape, low crater density, high repeatability

2. RK-Field-02
- Target: rough irregular variety
- Parameter intent: stronger axis stretch and ridge bias

3. RK-Field-03
- Target: dusty rounded variant
- Parameter intent: softer edges, lower fracture, higher dust coverage

4. SH-Field-01
- Target: layered shelf asteroid
- Parameter intent: medium macro amplitude, shelf-biased meso noise, moderate crater count

5. FR-Field-01
- Target: chipped boulder field filler
- Parameter intent: low crater clustering, moderate fracture passes, sharper edges

6. DS-Field-01
- Target: dust-coated smooth drift variant
- Parameter intent: lower edge sharpness, higher dust coverage, reduced micro noise

7. PN-Field-01
- Target: flattened slab variant for silhouette diversity
- Parameter intent: strong axis compression on one axis with moderate ridge detail

8. NK-Field-01
- Target: clustered-lobe asteroid
- Parameter intent: multi-lobe macro displacement with low fracture and moderate crater rims

### Hero Presets

1. H-Landmark-01 (Crater Crown)
- Target: high-recognition landmark
- Parameter intent: large clustered craters with pronounced rims

2. H-Landmark-02 (Fracture Spine)
- Target: navigation-anchoring silhouette
- Parameter intent: strong fracture passes and elongated axis profile

3. H-Landmark-03 (Metal Scar)
- Target: mining-interest visual cue
- Parameter intent: higher metallic vein coverage and shelf structures

4. H-Landmark-04 (Shard Halo)
- Target: high-threat visual anchor
- Parameter intent: high edge sharpness, spined silhouette bias, moderate crater depth

5. H-Landmark-05 (Broken Ring)
- Target: navigation-recognition set piece
- Parameter intent: ring-like macro void with reinforced rim structures and fracture accents

6. H-Landmark-06 (Hollow Cathedral)
- Target: landmark with internal cavity silhouette
- Parameter intent: hollow-pocket profile, large crater overlaps, strong directional erosion

7. H-Landmark-07 (Glassy Relic)
- Target: rare anomalous asteroid cue
- Parameter intent: low crater count, high fused-surface look, elevated albedo variance

8. H-Landmark-08 (Knotted Mass)
- Target: deep-space anchor object
- Parameter intent: clustered lobe profile with high macro amplitude and mixed ridge orientation

## LOD and Runtime Budget Targets

Per-asset mesh targets:
1. LOD0 (hero source for close range)
- Rocky baseline: 120k-350k triangles
- Hero: 250k-900k triangles

2. LOD1
- Rocky baseline: 35k-110k triangles
- Hero: 70k-220k triangles

3. LOD2
- Rocky baseline: 8k-30k triangles
- Hero: 20k-55k triangles

4. LOD3
- Rocky baseline: 1.5k-8k triangles
- Hero: 4k-16k triangles

Runtime constraints:
1. LOD switching must preserve silhouette class identity.
2. Fallback behavior must not collapse hero into indistinguishable baseline class.
3. Both surfaces must pass parity checks for identity at representative camera distances.

## Determinism and Reproducibility

1. Seed and parameter bundle are the source of truth.
2. Generator version is recorded with every output artifact.
3. Random stream must be deterministic and order-stable for all passes.
4. Any algorithm change requires generator version bump and revalidation.

## Artifact Naming Convention

Mesh export names:
- ast_{tier}_{materialSlug}_{profile}_{ordinal}_{surface}_{rev}_lod{n}.glb
- Example: ast_h_carbon_cr_042_ds_r1_lod0.glb

Companion metadata:
- ast_{tier}_{materialSlug}_{profile}_{ordinal}_{surface}_{rev}.json

Required metadata fields:
1. seedId
2. generatorVersion
3. parameterBundleHash
4. profilePreset
5. triangleCountsByLod
6. sourcePipelineCommit
7. validationStatus

## Validation and Acceptance

### Geometry Validation

1. Non-manifold and self-intersection checks must pass.
2. Normal orientation and tangent generation must pass.
3. UV set completeness must pass for required material workflow.
4. Base material classification must resolve to one row in the canonical materials catalog.

### Visual Validation

1. Family readability at gameplay distance must pass.
2. Silhouette uniqueness against nearest 20 catalog neighbors must pass.
3. Hero assets must pass dual-surface landmark readability checks.

### Performance Validation

1. LOD transitions must be free of severe popping under standard camera motion.
2. Scene budget checks must pass for asteroid-dense scenarios.
3. Fallback tier transitions must preserve identity semantics.
4. Base-material transitions must preserve the selected catalog material identity.

## SW-13B Milestone Mapping

1. M0B
- Publish seed taxonomy, profile presets, and initial parameter bundles.
- Build initial matrix with source channel, license status, owner, and replacement date (if proxy).

2. M1B
- Validate baseline and hero asteroid sets in Stellar Viewer.

3. M2B
- Validate baseline and hero asteroid sets in ship-external-view.

4. M3B
- Validate dual-surface parity for identity, LOD behavior, and fallback semantics.

5. M4B
- Canary burn-down for unresolved proxy and fidelity issues.

## Open Decisions for Orion Lock

1. Final triangle budgets by target hardware tier.
2. Required minimum count of hero seeds per asteroid profile.
3. Whether metallic-vein profile requires explicit gameplay tag in future contract revisions.
