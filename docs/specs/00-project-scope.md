# 00 Project Scope

## Objective

Define the boundaries of Version 1 so the repo stays focused on a buildable first system.

## In Scope

- single-identity talking head generation
- per-subject training
- audio-driven mouth and basic facial motion
- head-only rendering
- modest quality target suitable for iteration and debugging
- a pipeline that is understandable by an experienced software engineer with limited DNN training background

## Out of Scope

- zero-shot or few-shot identity generalization
- full-body or torso generation
- strong support for extreme head poses
- advanced emotion control
- highly optimized real-time deployment requirements
- claims of matching or beating recent papers

## Why This Spec Exists

Without a scope spec, the project will drift toward ambitious research goals before a first working system exists.

## Dependencies

- none

## Definition of Done

- the repo has a written definition of Version 1
- non-goals are explicit
- later specs can reference this scope instead of redefining it

## Open Questions

- what minimum visual quality is acceptable for the first milestone?
- how much head motion should Version 1 allow before it is considered out of scope?
