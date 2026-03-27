# 06 Audio To Motion Model

## Objective

Define the learned module that maps speech audio into the canonical `audio_motion` target space.

## Version 1 Decision

The audio model is intentionally narrow:

- input: normalized speech audio or cached audio features
- output: frame-aligned `audio_motion`
- no direct rendering
- no identity generalization
- no prediction of arbitrary Gaussian attributes

The design should follow the structured-prediction philosophy of [GaussianHeadTalk](../references/wacv-2026-gaussianheadtalk.md) without inheriting its full model complexity.

## Input Contract

Required runtime inputs:

- `audio/audio_16k_mono.wav` during training
- `audio/features.npy` if preprocessing caches features
- target fps and frame timestamps from the processed subject package

Version 1 should assume offline clip inference, not streaming. That means the model may use future context if that materially simplifies the baseline.

## Feature Boundary

The default Version 1 path is:

- extract audio features during preprocessing
- cache them in the subject package
- train a compact temporal predictor on top of those features

Acceptable feature families:

- log-mel or MFCC features for the simplest baseline
- frozen self-supervised speech embeddings if they provide a clear benefit

Not acceptable for Version 1:

- learning the full audio front end end to end as a required baseline
- hiding feature extraction details outside the dataset manifest

## Output Contract

The model predicts:

- `audio_motion[t]` for each frame-aligned timestamp

The model does not need to predict:

- blink
- head pose
- camera parameters
- every expression coefficient from the tracker if those are outside the canonical target space

## Model Shape

Preferred Version 1 model families:

- small 1D temporal convolution stack
- GRU or LSTM
- light transformer or conformer only if the simpler baselines are clearly inadequate

Start with the smallest model that can regress the target sequence. The repo should not begin with a transformer-heavy design just because later papers do.

## Training Objective

Required losses:

- regression loss on `audio_motion`
- temporal smoothness or velocity regularization if needed for stability

Useful optional diagnostics:

- mouth-aperture-specific error
- per-dimension validation curves
- neutral-frame bias checks

The model should predict motion in the canonical target space, not copy tracker files verbatim.

## Out of Scope

- cross-speaker training
- style or emotion tokens
- adversarial training for the audio model
- direct audio-to-render supervision as the required first path

## Dependencies

- [04-face-motion-targets.md](04-face-motion-targets.md)

## Definition of Done

- the repo defines one stable boundary between audio features and motion prediction
- a model can be trained and validated on `audio_motion` without invoking the renderer
- failures can be interpreted as audio-to-motion failures rather than avatar or camera failures
