# 07 Training Workflow

## Objective

Define how the project trains the first complete system from prepared data.

## In Scope

- training stages needed for Version 1
- required inputs and outputs for each stage
- checkpointing and resumability
- basic experiment tracking expectations
- enough visibility into losses and sample outputs to support debugging

## Out of Scope

- large-scale hyperparameter search infrastructure
- multi-node training
- automated benchmark sweeps

## Why This Spec Exists

The first end-to-end system should be trainable in a way that is inspectable, repeatable, and not dependent on hidden manual steps.

## Dependencies

- [05-single-identity-avatar.md](/Users/jingunhong/Repos/gaussian-talking-head-study/simple-gaussian-talking-head/docs/specs/05-single-identity-avatar.md)
- [06-audio-to-motion-model.md](/Users/jingunhong/Repos/gaussian-talking-head-study/simple-gaussian-talking-head/docs/specs/06-audio-to-motion-model.md)

## Definition of Done

- the repo defines the major training stages
- each stage has clear inputs, outputs, and artifacts
- interrupted training can be resumed without starting over

## Open Questions

- should avatar construction and audio-to-motion training be separate stages?
- what minimum experiment metadata is needed to make runs comparable?
