# 03 Preprocessing Pipeline

## Objective

Define the non-learning steps that prepare raw input data for training and inference.

## In Scope

- extracting frames and audio from source recordings
- frame rate and resolution normalization
- basic quality checks
- generation of intermediate artifacts needed for later stages
- reproducible preprocessing runs

## Out of Scope

- aggressive data augmentation strategy
- complex dataset balancing logic
- multi-dataset harmonization

## Why This Spec Exists

Preprocessing is the first place where the project becomes concrete. If this stage is vague, everything after it becomes harder to debug.

## Dependencies

- [02-dataset-and-sample-format.md](/Users/jingunhong/Repos/gaussian-talking-head-study/simple-gaussian-talking-head/docs/specs/02-dataset-and-sample-format.md)

## Definition of Done

- a raw sample can be transformed into normalized training-ready artifacts
- preprocessing outputs are deterministic enough to inspect and rerun
- failures can be surfaced before model training begins

## Open Questions

- what artifacts should be considered required versus optional?
- should preprocessing produce one immutable dataset snapshot per run?
