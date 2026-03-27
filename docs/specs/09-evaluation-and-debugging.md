# 09 Evaluation And Debugging

## Objective

Define how progress will be judged and how failures will be inspected in Version 1.

## In Scope

- simple success criteria for visual quality, sync quality, and stability
- artifact generation for qualitative inspection
- checks that help localize failures to preprocessing, motion targets, avatar quality, or audio-to-motion prediction
- lightweight comparisons across runs

## Out of Scope

- exhaustive benchmark reproduction
- paper-grade evaluation suites
- leaderboard-oriented optimization

## Why This Spec Exists

This project is likely to fail gradually rather than catastrophically. The repo needs a shared way to judge whether it is improving.

## Dependencies

- [03-preprocessing-pipeline.md](/Users/jingunhong/Repos/gaussian-talking-head-study/simple-gaussian-talking-head/docs/specs/03-preprocessing-pipeline.md)
- [04-face-motion-targets.md](/Users/jingunhong/Repos/gaussian-talking-head-study/simple-gaussian-talking-head/docs/specs/04-face-motion-targets.md)
- [07-training-workflow.md](/Users/jingunhong/Repos/gaussian-talking-head-study/simple-gaussian-talking-head/docs/specs/07-training-workflow.md)
- [08-inference-and-rendering.md](/Users/jingunhong/Repos/gaussian-talking-head-study/simple-gaussian-talking-head/docs/specs/08-inference-and-rendering.md)

## Definition of Done

- the repo defines how a run will be inspected
- qualitative review artifacts are part of the workflow
- the project has a basic way to compare runs over time

## Open Questions

- which metrics matter enough for Version 1 to track from the start?
- what kinds of debug visualizations will save the most time?
