# 05 Single Identity Avatar

## Objective

Define the representation of the subject-specific avatar that will be animated and rendered.

## In Scope

- a constrained 3DGS-based head representation for one identity
- a stable canonical state for the avatar
- the relationship between the avatar and the chosen motion target space
- enough structure to support understandable deformation and rendering

## Out of Scope

- multi-identity shared avatars
- one-shot identity creation from a single image
- highly expressive free-form deformation without constraints

## Why This Spec Exists

The avatar is the core object that later stages depend on. This spec should make clear what is being animated, even before the exact implementation is chosen.

## Dependencies

- [04-face-motion-targets.md](/Users/jingunhong/Repos/gaussian-talking-head-study/simple-gaussian-talking-head/docs/specs/04-face-motion-targets.md)

## Definition of Done

- the repo defines what the subject-specific avatar consists of
- the avatar has a clear canonical state
- the avatar can be connected to structured motion targets

## Open Questions

- how constrained should the representation be in Version 1?
- which parts of the avatar should remain fixed versus driven by motion?
