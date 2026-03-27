# 06 Audio To Motion Model

## Objective

Define the learning component that maps audio input to the project's motion target space.

## In Scope

- the input audio representation used by the model
- the temporal prediction task
- the expected model outputs
- the boundary between fixed feature extraction and learned prediction

## Out of Scope

- large end-to-end multimodal systems
- identity generalization research goals
- direct prediction of all Gaussian properties from raw audio

## Why This Spec Exists

This is the main learned component of Version 1. It should stay understandable and debuggable.

## Dependencies

- [04-face-motion-targets.md](/Users/jingunhong/Repos/gaussian-talking-head-study/simple-gaussian-talking-head/docs/specs/04-face-motion-targets.md)

## Definition of Done

- the repo defines what audio goes in and what motion representation comes out
- the training target for the model is clear
- the model boundary is small enough that failures can be isolated

## Open Questions

- which audio representation is simplest while still useful?
- how much temporal context should Version 1 require?
