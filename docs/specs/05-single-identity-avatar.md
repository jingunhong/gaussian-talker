# 05 Single Identity Avatar

## Objective

Define the subject-specific 3D Gaussian avatar that is trained once per subject and later driven by structured motion targets.

## Version 1 Decision

The avatar should be constrained, canonical, and easy to reason about:

- one subject per avatar
- head-only representation
- canonical near-neutral state
- limited motion control through tracked face parameters
- appearance held as stable as possible across time

This follows the core lesson from [TalkingGaussian](../references/eccv-2024-talkinggaussian.md): stability is more valuable than maximum deformation freedom for a first working system.

## Required Avatar Components

### Canonical Gaussian State

The avatar must contain a persistent set of Gaussians representing the subject in a canonical state.

Required properties:

- subject-specific
- stored in a reusable checkpoint
- renderable without audio by applying canonical or tracked motion

### Deformation Binding

The avatar must expose a clear bridge from motion targets to Gaussian deformation.

Preferred Version 1 design:

- bind deformation to a tracked face model, deformation graph, or equivalent low-DOF structure
- use structured motion controls derived from [04-face-motion-targets.md](04-face-motion-targets.md)
- keep most Gaussian appearance attributes fixed at inference time

Avoid a fully free-form per-Gaussian audio-conditioned deformation model for the first baseline.

### Camera And Background Contract

The avatar stage must know how to render from the training-camera convention declared in preprocessing.

If the pipeline uses a static background plate or alpha composition, that asset should be treated as part of the avatar package, not re-estimated during every inference run.

## Motion Scope

Version 1 motion should primarily affect:

- jaw and mouth region
- lower-face expression
- small correlated cheek motion if it falls out of the tracked target space

Version 1 should not require:

- deliberate large head rotations at inference time
- hair or torso dynamics
- physically accurate teeth and tongue modeling
- identity edits

If mouth interior quality becomes a bottleneck, a small dedicated mouth component is acceptable as a later extension point. It is not part of the initial required design.

## Required Inputs

Avatar fitting depends on:

- processed subject frames
- camera transforms
- face masks or parsing outputs
- tracked face parameters
- train and validation splits

## Required Outputs

Each trained avatar should produce:

- a canonical avatar checkpoint
- enough metadata to reconstruct the subject and config used
- reconstruction renders on train and validation frames
- a simple canonical-view preview render

## Out of Scope

- shared multi-subject avatar spaces
- one-shot identity creation from a single image
- unconstrained audio-conditioned prediction of color, scale, opacity, and position for every Gaussian
- torso generation as a required Version 1 feature

## Dependencies

- [04-face-motion-targets.md](04-face-motion-targets.md)

## Definition of Done

- the repo has one clear description of what a trained subject avatar contains
- the avatar can be driven by the canonical motion target representation
- later stages can talk about “the avatar checkpoint” without ambiguity about cameras, deformation, or background handling
