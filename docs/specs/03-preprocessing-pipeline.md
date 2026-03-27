# 03 Preprocessing Pipeline

## Objective

Turn a raw monocular talking-head clip into a training-ready subject package with deterministic, inspectable artifacts.

## Design Direction

The public reference repos are informative here:

- TalkingGaussian and GaussianTalker both use a practical `video -> frames/audio -> tracking/parsing -> transforms/audio_features` pipeline
- both expose the same lesson: preprocessing must output concrete artifacts that the trainer can consume directly

This repo should keep that artifact richness while splitting the work into modular stages instead of one opaque `process.py`.

## Required Stages

### 1. Source Import

- register the raw clip under a subject id
- copy or link the source asset into the processed subject package
- record basic metadata in `manifest.json`

### 2. Frame And Audio Extraction

- decode all source frames in source order
- preserve source fps unless there is a deliberate, documented resampling step
- extract audio to `audio/audio.wav`
- create `audio/audio_16k_mono.wav` for feature extraction

For `data/raw/obama/obama.mp4`, preprocessing should preserve the native 25 fps timeline.

### 3. Basic Quality Checks

- detect unreadable frames
- detect missing or silent audio spans
- estimate face bounding-box stability across the clip
- surface likely cuts or discontinuities

Preprocessing should fail early if the clip violates the Version 1 assumptions instead of silently producing broken targets.

### 4. Face Localization And Tracking Inputs

- generate per-frame face landmarks or equivalent keypoints
- estimate a stable crop or canonical face region
- save per-frame validity flags

These outputs feed both tracking and debugging; they are not throwaway intermediate tensors.

### 5. Parsing, Masking, And Background Assets

- produce face or head masks needed by avatar fitting
- optionally produce torso/background masks if the renderer needs them
- build a reusable static or median background image if the chosen avatar pipeline uses one

TalkingGaussian and GaussianTalker both rely on region separation. Version 1 should keep this as a preprocessing responsibility, not something hidden inside the trainer.

### 6. Face Model Tracking And Camera Metadata

- fit a tracked face model or equivalent structured parameterization per frame
- estimate or recover camera parameters needed for avatar fitting
- write `camera/transforms_train.json` and `camera/transforms_val.json`
- save tracker outputs in a stable machine-readable file such as `tracking/face_params.npz`

The exact tracker may change later. The output contract may not.

### 7. Motion And Blink Precomputation

- derive canonical motion targets from the tracked parameters
- export blink-related supervision if available
- align motion targets to the frame timeline with a validity mask

Reference implementations often keep blink supervision separate from the main audio features. That separation should remain visible in this repo.

### 8. Audio Feature Caching

- compute and store frame-aligned audio features under `audio/features.npy` or an equivalent format
- record feature type, dimension, hop size, and extractor version in metadata

Precomputing audio features is the default Version 1 path. End-to-end audio feature learning is deferred.

### 9. Split And Report Generation

- create train and validation splits
- emit quick preview artifacts such as contact sheets, landmark overlays, and short inspection clips
- write a preprocessing summary with counts, durations, and failure flags

## Required Properties

- rerunning preprocessing with the same config should produce the same filenames, splits, and metadata
- failures should name the stage that failed
- each intermediate artifact should be inspectable without loading the full training code
- stage outputs should be resumable; earlier successful stages should not be redone unnecessarily

## Out of Scope

- augmentation-heavy preprocessing
- multi-subject balancing and sampling logic
- silent fallback downloads of external models or assets

## Dependencies

- [02-dataset-and-sample-format.md](02-dataset-and-sample-format.md)

## Definition of Done

- `data/raw/obama/obama.mp4` can be converted into one complete processed subject package
- the package includes frames, audio, tracking, transforms, motion targets, and splits
- a later training failure can be traced back to a concrete preprocessing artifact instead of a vague data problem
