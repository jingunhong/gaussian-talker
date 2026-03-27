# Gaussian Talker

A practical implementation repo for building a **simple, achievable, audio-driven 3D Gaussian Splatting talking head system**.

This project is intentionally **not** trying to start from the most advanced or most generalizable method in the literature. The goal is to build a version that is realistic for an experienced software engineer who is new to deep neural network training and wants to understand the system by implementing it.

## Who This Repo Is For

This repo is for:

- software engineers who already know how to build systems and debug pipelines
- people who want to learn talking head generation by building, not only by reading papers
- beginners in DNN training who want a narrower and more understandable first project

## Project Goal

Build a **single-identity, per-subject, audio-driven talking head system** with a constrained and understandable pipeline:

- one person
- a few minutes of talking video for training
- audio-driven lip and basic facial motion
- stable head rendering
- modest scope and modest quality target for Version 1

The goal is not to beat SOTA. The goal is to make the full pipeline understandable and buildable.

## Design Philosophy

This repo follows a few principles:

- prefer a small working system over a clever but fragile system
- separate the problem into understandable modules
- favor stable motion and stable rendering before expressiveness
- use structure and constraints instead of learning everything end-to-end at once
- treat real-time performance as a later optimization unless it comes naturally

## Intended Version 1 Scope

Version 1 should aim for:

- single identity
- per-subject training
- head-only rendering
- mostly frontal or near-frontal motion
- audio-to-motion prediction in a low-dimensional motion space
- a constrained 3DGS avatar representation

Version 1 should explicitly avoid:

- zero-shot generalization
- one-shot or few-shot identity adaptation
- full-body synthesis
- extreme head pose support
- emotion disentanglement
- large end-to-end architectures trained from scratch

## High-Level Pipeline

The planned system is roughly:

1. preprocess a talking-head video and paired audio
2. obtain per-frame facial motion targets from a tracked face model
3. build or fit a stable 3DGS-based avatar for one identity
4. train a small audio-to-motion model
5. drive the avatar with predicted motion and render the result

This keeps the project modular enough that failures can be debugged component by component.

## Why This Repo Exists

Many papers in this area are exciting, but they combine several difficult problems at once:

- geometry
- rendering
- speech-driven motion
- identity modeling
- temporal stability
- generalization

That is great for research, but it is a bad place to start implementing from scratch.

This repo exists to provide a more practical entry point: build something simpler first, understand the failure modes, and then expand toward more advanced ideas later.

## Success Criteria for the First Working Version

The first version is successful if:

- the person remains recognizable
- the mouth motion roughly follows speech timing
- the rendered output is stable enough to inspect and improve
- the codebase stays understandable to the person building it

## Planned Direction

This repo will likely grow toward:

- a concrete implementation roadmap
- notes on data preparation and preprocessing
- baseline model components
- experiments for audio-to-motion prediction
- experiments for stable 3DGS avatar control

## Data Setup

The baseline subject clip for the current specs is Obama. Download it to `data/raw/obama/obama.mp4`:

```bash
wget https://github.com/YudongGuo/AD-NeRF/blob/master/dataset/vids/Obama.mp4?raw=true -O data/raw/obama/obama.mp4
```

Repo data layout:

- `data/raw/` for immutable source assets such as downloaded videos
- `data/processed/` for derived frames, audio, tracking, masks, motion targets, and manifests
- `checkpoints/`, `outputs/`, and `renders/` for run artifacts

These directories are kept in the repo with placeholder files, but generated artifacts inside them are ignored by git.

## Status

Early scaffold. The main purpose right now is to define a clear implementation target before adding code.
