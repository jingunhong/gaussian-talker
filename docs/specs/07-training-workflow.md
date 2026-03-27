# 07 Training Workflow

## Objective

Define the staged training procedure for the first complete personalized talking-head system.

## Version 1 Decision

Training is staged, not end to end.

That is a deliberate divergence from more ambitious paper pipelines. The first system should make it possible to answer:

- is preprocessing valid?
- are motion targets stable?
- can the avatar reconstruct the subject?
- can audio predict the chosen motion space?

before the repo attempts any joint optimization.

## Required Stages

### Stage 0. Subject Preparation

Input:

- raw subject clip such as `data/raw/obama/obama.mp4`

Output:

- processed subject package under `data/processed/{subject_id}/`

### Stage 1. Motion Target Derivation

Input:

- tracking outputs from preprocessing

Output:

- canonical `motion/motion_targets.npz`

This stage may be performed as part of preprocessing, but it is conceptually separate and should be debuggable on its own.

### Stage 2. Avatar Fitting

Input:

- processed subject package
- tracked motion and camera metadata

Output:

- avatar checkpoint
- train and validation reconstruction artifacts

This stage should train only against tracked ground-truth motion, not predicted audio motion.

### Stage 3. Audio-To-Motion Training

Input:

- processed subject package
- canonical motion targets
- cached audio features or normalized waveform

Output:

- audio-model checkpoint
- train and validation motion metrics
- example motion plots and optional rendered previews

### Stage 4. End-To-End Offline Rendering

Input:

- avatar checkpoint
- audio-model checkpoint
- validation or custom audio clip

Output:

- rendered talking-head video
- predicted motion file
- debug side-by-side artifacts

This stage is evaluation and productization of the pipeline, not a joint fine-tuning stage.

## Optional Later Stage

Deferred until the staged baseline is working:

- joint fine-tuning of avatar and audio model using predicted motion

This is explicitly optional because it makes failure attribution harder.

## Run Management Requirements

Each trainable stage must:

- write checkpoints periodically
- support resume from the latest or a named checkpoint
- write scalar metrics per epoch or iteration
- emit a small set of qualitative artifacts
- store the resolved config in the run directory

## Minimum Run Metadata

Every run should record:

- `subject_id`
- stage name
- run name
- source processed-data path
- config path and resolved config contents
- random seed
- output directory
- checkpoint path

Including a git commit or dirty-worktree flag is recommended when available.

## Out of Scope

- sweep managers
- distributed training
- benchmark orchestration across many identities

## Dependencies

- [05-single-identity-avatar.md](05-single-identity-avatar.md)
- [06-audio-to-motion-model.md](06-audio-to-motion-model.md)

## Definition of Done

- the repo has a stage order that can be followed without hidden paper knowledge
- avatar fitting and audio-to-motion training are explicitly separate
- an interrupted run can be resumed and its artifacts can still be interpreted later
