# 04 Face Motion Targets

## Objective

Define the motion representation that the learning system will predict from audio.

## In Scope

- per-frame facial motion targets derived from a tracked face model or equivalent structured representation
- the minimum motion variables needed for Version 1
- alignment between motion targets and video/audio time steps
- quality checks for motion target stability

## Out of Scope

- rich emotion control spaces
- full unconstrained facial performance capture
- end-to-end learning of motion directly from pixels without an intermediate target space

## Why This Spec Exists

For Version 1, audio should not directly predict every visual attribute. A structured motion target makes the problem smaller and easier to debug.

## Dependencies

- [03-preprocessing-pipeline.md](/Users/jingunhong/Repos/gaussian-talking-head-study/simple-gaussian-talking-head/docs/specs/03-preprocessing-pipeline.md)

## Definition of Done

- the repo defines a canonical motion target representation
- motion targets can be extracted or derived consistently per frame
- later training code can consume these targets without ambiguity

## Open Questions

- what is the smallest useful motion space for Version 1?
- how much tracker noise is acceptable before the targets become unusable?
