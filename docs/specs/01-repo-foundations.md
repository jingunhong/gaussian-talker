# 01 Repo Foundations

## Objective

Define the minimum repo structure that keeps the pipeline modular and reproducible without turning the project into a framework.

## Required Top-Level Layout

As implementation is added, the repo should converge toward this layout:

- `src/gaussian_talker/`: importable code
- `scripts/`: thin CLI entrypoints and orchestration wrappers
- `configs/`: YAML or Python config files grouped by stage
- `tests/`: unit and smoke tests
- `docs/`: specs, references, and design notes
- `data/raw/`: immutable raw subject source assets
- `data/processed/`: processed subject packages and derived metadata
- `outputs/`: stage reports, diagnostics, manifests, and intermediate exports worth inspecting
- `checkpoints/`: training checkpoints
- `renders/`: final and debug render outputs

The baseline raw clip should live at `data/raw/obama/obama.mp4`, and later raw subject assets should follow the same `data/raw/{subject_id}/...` convention.

## Required Code Boundaries

The codebase should keep these modules separate:

- `preprocess`: video/audio import, frame extraction, tracking, masks, manifests
- `motion`: tracker outputs, motion target derivation, blink handling
- `avatar`: canonical 3DGS state and deformation control
- `audio_model`: audio features and audio-to-motion prediction
- `train`: stage-specific training loops and checkpoint handling
- `render`: offline inference and video assembly
- `eval`: metrics, plots, and qualitative artifact generation

Avoid paper-style monoliths where one script both preprocesses data and trains the model.

## Canonical Entry Points

Version 1 should eventually expose a small set of standard CLIs, whether implemented as files in `scripts/` or `python -m` entrypoints:

- `prepare_subject`
- `extract_motion_targets`
- `train_avatar`
- `train_audio_to_motion`
- `render_clip`
- `evaluate_run`

Reference repos such as TalkingGaussian and GaussianTalker often collapse several steps into a single script. This repo should keep a convenience wrapper if useful, but the underlying stages should remain separately callable.

## Configuration Rules

- each stage gets its own config namespace under `configs/`
- configs should describe inputs, outputs, and model hyperparameters for one stage only
- the effective config used for a run must be copied into that run's output directory
- subject-specific values such as `subject_id`, source clip path, fps, and split definitions should live in a manifest or subject config rather than being embedded in training code

## Run And Artifact Naming

Use predictable paths and names so runs are easy to compare:

- `data/processed/{subject_id}/...`
- `checkpoints/{subject_id}/{stage}/{run_name}/...`
- `outputs/{subject_id}/{stage}/{run_name}/...`
- `renders/{subject_id}/{run_name}/...`

Each run directory should contain:

- the resolved config
- a short manifest with subject id, git commit if available, and stage name
- scalar metrics in machine-readable form
- a small set of qualitative artifacts

## Out of Scope

- plugin systems or registry-heavy abstractions
- distributed training orchestration
- service deployment packaging
- experiment tracking platforms as a hard dependency

## Dependencies

- [00-project-scope.md](00-project-scope.md)

## Definition of Done

- a contributor can tell where preprocessing code ends and training code begins
- data, checkpoints, renders, and docs have non-overlapping homes
- later implementation can follow a small number of canonical workflows instead of inventing new paths per script
