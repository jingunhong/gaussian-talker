# 09 Evaluation And Debugging

## Objective

Define the minimum evaluation and debugging workflow needed to tell whether the system is improving and where it is failing.

## Version 1 Decision

Evaluation is stage aware.

The repo should not rely on a single final video and subjective impressions alone. It should generate artifacts that answer four separate questions:

- was preprocessing valid?
- are motion targets trustworthy?
- can the avatar reconstruct held-out frames?
- does the audio model predict usable motion?

## Required Evaluation Layers

### 1. Preprocessing Quality

Required checks:

- total frames decoded vs expected frame count
- duration and fps consistency
- percentage of invalid or missing tracked frames
- face-bbox stability over time
- preview contact sheet and landmark overlay samples

### 2. Motion Target Quality

Required checks:

- plots of selected motion dimensions over time
- mouth-aperture and jaw-motion sanity plots
- blink signal visualization if present
- count of invalid frames and discontinuities

The goal is to catch tracker noise before it pollutes model training.

### 3. Avatar Quality

Required checks:

- train-frame reconstruction renders
- held-out validation-frame reconstruction renders
- close-up mouth crops on validation frames
- scalar image-space losses recorded over time

Useful optional metrics:

- PSNR
- SSIM
- LPIPS

Version 1 does not require paper-grade evaluation, but it does require enough evidence to distinguish “bad avatar” from “bad audio model.”

### 4. Audio-To-Motion Quality

Required checks:

- train and validation motion regression loss
- per-dimension error summaries
- rendered preview using predicted motion on held-out audio segments
- overlays or plots comparing predicted vs tracked motion

Useful optional metrics:

- mouth-aperture error
- temporal derivative error
- simple lip-sync proxy metrics if added later

### 5. End-To-End Quality

Required outputs:

- final inference video
- side-by-side validation clip when reference video exists
- short debug clips from fixed timestamps

The primary Version 1 qualitative criteria are:

- recognizable identity
- speech-timed mouth motion
- limited wobble
- absence of obvious catastrophic drift

## Required Run Report

Each significant run should emit a lightweight report directory containing:

- config used
- scalar metrics in JSON or CSV
- a small table of run metadata
- links or filenames for key qualitative artifacts

This can be plain files in `outputs/`; no external experiment tracker is required.

## Comparison Policy

Runs should be compared on the same held-out subject segments whenever possible.

For the Obama baseline clip, evaluation should reuse fixed validation windows rather than choosing new random windows each run.

## Out of Scope

- leaderboard evaluation
- exhaustive reproduction of literature metrics
- large benchmark aggregation across many identities

## Dependencies

- [03-preprocessing-pipeline.md](03-preprocessing-pipeline.md)
- [04-face-motion-targets.md](04-face-motion-targets.md)
- [07-training-workflow.md](07-training-workflow.md)
- [08-inference-and-rendering.md](08-inference-and-rendering.md)

## Definition of Done

- every major stage produces artifacts that can be reviewed independently
- the repo has a consistent way to compare runs on the same subject and held-out segments
- a poor final render can be traced back to preprocessing, motion, avatar, or audio-model issues without guesswork
