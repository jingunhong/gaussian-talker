# 02 Dataset And Sample Format

## Objective

Define the expected raw inputs and the intermediate sample format used by later stages.

## In Scope

- the kind of source video the system expects
- audio expectations and pairing with video
- assumptions about subject count, duration, framing, and quality
- a normalized sample structure that later steps can consume

## Out of Scope

- support for many heterogeneous datasets at once
- large benchmark integration
- fully automated data collection

## Why This Spec Exists

Most downstream confusion comes from weak data contracts. The project should establish early what a valid sample looks like.

## Dependencies

- [00-project-scope.md](/Users/jingunhong/Repos/gaussian-talking-head-study/simple-gaussian-talking-head/docs/specs/00-project-scope.md)
- [01-repo-foundations.md](/Users/jingunhong/Repos/gaussian-talking-head-study/simple-gaussian-talking-head/docs/specs/01-repo-foundations.md)

## Definition of Done

- the repo defines what raw input data is accepted
- the repo defines the normalized sample representation used after import
- later stages can rely on that representation without guessing

## Open Questions

- what minimum clip duration is enough for a first useful subject?
- should Version 1 assume one continuous recording or allow multiple clips per subject?
