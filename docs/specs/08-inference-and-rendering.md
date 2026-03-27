# 08 Inference And Rendering

## Objective

Define the runtime flow that turns new audio into rendered talking head output.

## In Scope

- inference inputs and outputs
- how audio, motion prediction, avatar control, and rendering connect at runtime
- expected output formats for video previews or rendered sequences
- a simple user-facing inference path for one trained subject

## Out of Scope

- real-time product deployment requirements
- live webcam or streaming integration
- multi-subject serving infrastructure

## Why This Spec Exists

The project needs a clear definition of what it means to "run the model" after training.

## Dependencies

- [05-single-identity-avatar.md](/Users/jingunhong/Repos/gaussian-talking-head-study/simple-gaussian-talking-head/docs/specs/05-single-identity-avatar.md)
- [06-audio-to-motion-model.md](/Users/jingunhong/Repos/gaussian-talking-head-study/simple-gaussian-talking-head/docs/specs/06-audio-to-motion-model.md)
- [07-training-workflow.md](/Users/jingunhong/Repos/gaussian-talking-head-study/simple-gaussian-talking-head/docs/specs/07-training-workflow.md)

## Definition of Done

- the repo defines the standard inference path for a trained subject
- the runtime inputs and expected artifacts are clear
- users can generate outputs without relying on undocumented manual steps

## Open Questions

- should Version 1 generate single clips only, or support batched render jobs?
- what preview outputs are most useful during early iteration?
