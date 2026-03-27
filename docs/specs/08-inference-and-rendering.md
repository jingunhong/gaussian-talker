# 08 Inference And Rendering

## Objective

Define the standard offline runtime path from new audio to a rendered talking-head clip.

## Version 1 Decision

Inference is offline and subject specific.

The standard user story is:

- choose one trained subject avatar
- provide one audio clip
- predict motion
- render one talking-head video

No live streaming, batching service, or multi-identity serving layer is required.

## Required Inputs

- processed subject package
- trained avatar checkpoint
- trained audio-to-motion checkpoint
- input audio clip, typically WAV

If the input audio is not already normalized, inference must create a normalized 16 kHz mono version before feature extraction.

## Runtime Flow

### 1. Audio Normalization

- ingest custom audio
- convert to the canonical sample rate and channel format
- trim or pad only if the config says so

### 2. Audio Feature Extraction

- compute the same feature representation used in training
- align feature timestamps to the render frame rate

### 3. Motion Prediction

- run the audio model to predict `audio_motion`
- apply any post-processing such as smoothing or neutral-bias correction
- inject blink or idle priors only through explicitly separate logic

### 4. Avatar Control

- map predicted motion to the avatar deformation interface
- use the canonical render camera or a documented fixed camera mode

Version 1 should default to a canonical frontal or training-style view, not an arbitrary novel view.

### 5. Rendering

- render frames at the configured resolution
- assemble frames into a video
- mux the original or normalized audio back into the rendered clip

## Required Outputs

Each inference run should produce:

- `final.mp4`: rendered talking-head result
- `predicted_motion.npz`: motion sequence used for rendering
- `metadata.json`: subject id, checkpoints, config, audio source, frame rate, and duration

Recommended debug outputs:

- `side_by_side.mp4`: render next to a reference or diagnostic view when available
- `mouth_crop.mp4`: zoomed mouth-region preview
- `frames/`: optional per-frame image dump for debugging

## Output Defaults

For the Obama baseline subject, the default render settings should stay close to the training data:

- 25 fps output
- square head-centered framing
- short clip rendering for inspection before full-length renders

## Out of Scope

- real-time performance guarantees
- webcam or microphone streaming
- multi-subject queueing or serving APIs
- arbitrary camera-path rendering as a Version 1 requirement

## Dependencies

- [05-single-identity-avatar.md](05-single-identity-avatar.md)
- [06-audio-to-motion-model.md](06-audio-to-motion-model.md)
- [07-training-workflow.md](07-training-workflow.md)

## Definition of Done

- a user can point the repo at one subject checkpoint pair and one audio clip and receive a rendered video
- the runtime path is documented in stage order
- the produced artifacts make it possible to inspect the predicted motion separately from the final render
