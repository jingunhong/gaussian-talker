# 00 Project Scope

## Objective

Define a Version 1 target that is small enough to build end to end, but concrete enough to drive code and data decisions.

## Version 1 Decision

Version 1 is a personalized talking-head system for one subject at a time:

- single identity
- monocular training video
- per-subject preprocessing and training
- audio-driven lip motion plus limited lower-face motion
- head-only rendering
- stability and inspectability over peak realism

The first required subject is the Obama clip at `data/raw/obama/obama.mp4`. The specs should support later clips with the same general capture style, but they should not assume a broader research scope than this first subject requires.

## In Scope

- preparing one monocular talking-head video into a reproducible subject package
- extracting structured per-frame face motion targets from tracking
- fitting a subject-specific 3D Gaussian avatar in a canonical state
- training a small audio-to-motion model against that structured target space
- offline rendering of a short talking-head clip from new audio
- producing debug artifacts that make failures attributable to a pipeline stage

## Explicit Non-Goals

- zero-shot, few-shot, or cross-identity generalization
- full-body, torso, or shoulder synthesis
- novel-view free-camera rendering as a Version 1 requirement
- extreme pose support beyond what appears in near-frontal monocular training footage
- emotion disentanglement, style transfer, or speaker-independent control
- large end-to-end systems that predict Gaussian attributes directly from raw audio
- reproducing full paper pipelines from the reference projects

## Quality Bar

Version 1 is successful if it can do all of the following on the first subject:

- keep the subject recognizable
- follow gross speech timing and mouth opening/closing behavior
- avoid obvious frame-to-frame wobble in the face region
- produce artifacts that make preprocessing, motion, avatar, and rendering failures separable

It does not need to:

- match paper metrics
- generalize to unseen identities
- run in real time
- produce convincing teeth, tongue, or expressive eyebrow motion from day one

## Reference Direction

These scope choices are intentionally aligned with the strongest Version 1 lessons from the reference set:

- [TalkingGaussian](../references/eccv-2024-talkinggaussian.md): keep appearance relatively stable and constrain deformation
- [GaussianHeadTalk](../references/wacv-2026-gaussianheadtalk.md): predict a structured motion representation rather than every render parameter
- [GaussianTalker (Cho et al.)](../references/acm-mm-2024-gaussiantalker-cho.md): per-subject pipelines can be effective, but paper-grade capacity is not required for a first build
- [MGGTalk](../references/cvpr-2025-mggtalk.md): treat generalization as a later problem, not a hidden Version 1 requirement

## Dependencies

- none

## Definition of Done

- later specs can assume a single-identity, per-subject, head-only system without re-arguing scope
- the repo has a clear reason to reject feature work that drifts toward generalization or full-body ambitions
- the first subject, `data/raw/obama/obama.mp4`, is explicitly recognized as the concrete planning baseline
