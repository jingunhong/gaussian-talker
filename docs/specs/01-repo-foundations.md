# 01 Repo Foundations

## Objective

Define the repo-level structure needed to support experiments without over-designing the project.

## In Scope

- a basic directory structure for code, configs, docs, scripts, and outputs
- a clear place for datasets and generated artifacts
- a small set of entry points for preprocessing, training, and inference
- lightweight conventions for configuration and experiment naming

## Out of Scope

- a complex platform or framework abstraction
- distributed training infrastructure
- production deployment packaging

## Why This Spec Exists

The repo should make it obvious where new code and experiment outputs belong. This reduces friction before the technical work becomes harder.

## Dependencies

- [00-project-scope.md](/Users/jingunhong/Repos/gaussian-talking-head-study/simple-gaussian-talking-head/docs/specs/00-project-scope.md)

## Definition of Done

- a new contributor can identify where to put source code, configs, and outputs
- the repo has a small number of canonical workflows
- experiment artifacts do not end up scattered across the repo

## Open Questions

- how much structure is enough before it becomes premature architecture?
- should experiment outputs live inside the repo tree or in an external workspace path?
