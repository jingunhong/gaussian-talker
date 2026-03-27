# 04 Face Motion Targets

## Objective

Define the structured facial motion representation predicted from audio and consumed by the avatar controller.

## Version 1 Decision

Version 1 will not ask audio to predict arbitrary Gaussian parameters.

Instead, audio will predict a compact lower-face motion space derived from tracked face-model parameters, following the stability-first direction suggested by:

- [TalkingGaussian](../references/eccv-2024-talkinggaussian.md)
- [GaussianHeadTalk](../references/wacv-2026-gaussianheadtalk.md)
- [GaussianTalker (Yu et al.)](../references/acm-mm-2024-gaussiantalker-yu.md)

## Motion Target Structure

The full tracked state should be separated into four groups:

### 1. Fixed Identity State

Not predicted from audio and fixed per subject:

- identity or shape coefficients
- canonical avatar pose and camera conventions
- any subject-specific appearance parameters

### 2. Tracked But Not Audio-Predicted State

Useful for fitting the avatar or analysis, but not a direct output of the audio model:

- global head pose
- camera pose
- crop transforms
- tracker confidence values

### 3. Primary Audio-Driven Motion State

This is the canonical model target and must be frame aligned:

- jaw rotation or jaw-open representation
- a compact lower-face expression vector
- optional lip-closure or mouth-aperture scalar if it improves supervision

Target dimensionality should remain small enough to inspect easily, preferably in the `8-16` range after any dimensionality reduction.

If the tracker exposes a larger FLAME or 3DMM expression vector, the preprocessing pipeline should store the full tracked parameters and also derive this smaller canonical `audio_motion` vector for learning.

### 4. Secondary Non-Audio State

Handled separately from the main audio target:

- blink or eyelid openness
- optional idle-motion priors such as slight breathing or micro-motion

This separation is intentional. Reference repos often use explicit blink supervision such as AU45-like signals because blink timing is only weakly determined by audio.

## Canonical File Contract

`motion/motion_targets.npz` should contain at least:

- `timestamps_sec`: shape `[T]`
- `audio_motion`: shape `[T, D]`
- `blink`: shape `[T, 1]` or omitted if unavailable
- `head_pose`: shape `[T, ...]` for debug and optional control
- `valid_mask`: shape `[T]`
- metadata describing the source tracker and derivation method

All arrays must share the same frame timeline as the decoded video frames and the derived audio features.

## Quality Requirements

Motion targets are only usable if they are:

- temporally smooth apart from real articulatory changes
- free of frequent dropped frames
- stable enough that the same phoneme does not map to wildly different target values without visual justification
- inspectable with simple plots and overlays

The preprocessing stage should flag:

- discontinuities from tracker resets
- excessive missing values
- implausible jaw spikes
- blink signals that are flat or saturated

## Out of Scope

- predicting brow, cheek, eye-gaze, and emotion control as first-class Version 1 outputs
- direct pixel-to-motion learning without a tracked target space
- free-form latent spaces with no semantic interpretation

## Dependencies

- [03-preprocessing-pipeline.md](03-preprocessing-pipeline.md)

## Definition of Done

- there is one canonical `audio_motion` target used across training, rendering, and evaluation
- blink handling is explicitly separated from the main audio target
- later code can load motion targets without reverse-engineering tracker-specific files
