# 02 Dataset And Sample Format

## Objective

Define the accepted raw subject footage and the normalized subject package consumed by preprocessing, training, rendering, and evaluation.

## Current Baseline Subject

The first required subject is:

- source file: `data/raw/obama/obama.mp4`
- clip duration: 320.0 seconds
- frame size: 450x450
- video rate: 25 fps
- video codec: H.264 (`avc1`)
- audio codec: AAC (`mp4a`)
- audio track: 48 kHz stereo

This matches the rough data profile used by prior talking-head baselines: one mostly frontal talking clip of a single speaker with several minutes of speech.

## Raw Input Contract

Version 1 accepts raw inputs that satisfy all of the following:

- one visible primary speaker
- one continuous or nearly continuous talking-head clip
- mostly frontal or near-frontal head pose
- head occupies a stable central region of the frame
- lighting and background do not change dramatically across the clip
- audible speech is present for most of the clip
- no rapid camera cuts, overlays, or heavy editing

Preferred raw format:

- MP4 container
- H.264 video
- embedded audio track
- at least 25 fps source video
- at least 3 minutes of usable speech

For Version 1, the system should assume one source clip per subject. Multi-clip subject aggregation is deferred.

## Normalized Subject Package

After import and preprocessing, each subject should be represented as a directory at:

`data/processed/{subject_id}/`

The package should contain these required artifacts:

- `manifest.json`: subject metadata and preprocessing summary
- `source/source.mp4`: copied or symlinked raw source asset
- `frames/`: decoded source-order frames with zero-padded filenames
- `audio/audio.wav`: extracted waveform at original or archival quality
- `audio/audio_16k_mono.wav`: normalized audio for feature extraction
- `camera/transforms_train.json`: train-frame camera metadata
- `camera/transforms_val.json`: validation-frame camera metadata
- `tracking/face_params.npz` or equivalent: tracked face model parameters per frame
- `tracking/landmarks/`: per-frame landmark outputs or packed equivalent
- `motion/motion_targets.npz`: canonical frame-aligned motion targets for learning
- `splits/train_frames.txt`: source-order train frame ids
- `splits/val_frames.txt`: source-order validation frame ids

Recommended artifacts for full Version 1 training:

- `masks/face/`: face or head parsing masks
- `masks/torso_or_bg/`: background-related masks if used by the renderer
- `background/background.png`: static or median background plate
- `audio/features.npy`: cached frame-aligned audio features
- `motion/blink.csv` or `motion/blink.npy`: blink supervision or proxy signal
- `previews/`: contact sheets and quick sanity renders

## Manifest Requirements

`manifest.json` should record at least:

- `subject_id`
- `source_path`
- `duration_sec`
- `frame_count`
- `fps`
- `width`
- `height`
- `audio_sample_rate_hz`
- `audio_channels`
- `preprocess_version`
- `split_policy`
- counts of frames rejected or marked invalid

The manifest is the dataset contract. Training code should not infer clip properties by rescanning the source video when the manifest already declares them.

## Split Policy

Validation data should come from contiguous held-out time ranges, not random individual frames.

Required behavior:

- preserve temporal ordering
- hold out at least 10 percent of usable frames
- prefer one or more contiguous windows of 10 to 20 seconds each
- keep train and validation timestamps disjoint in both frames and audio features

This matters because audio-to-motion and render stability can be overstated by random frame splits.

## Reference Compatibility

TalkingGaussian and GaussianTalker both expect subject directories containing artifacts conceptually equivalent to:

- decoded images
- parsing masks
- tracking parameters
- train and validation transform JSON files
- cached audio features
- blink-related CSV signals

This repo does not need to copy their exact folder names, but the normalized subject package should be easy to export into that style if future code reuse is helpful.

## Out of Scope

- benchmark dataset ingestion frameworks
- many-subject mixed metadata schemas
- automated web-scale clip collection

## Dependencies

- [00-project-scope.md](00-project-scope.md)
- [01-repo-foundations.md](01-repo-foundations.md)

## Definition of Done

- the repo has one clear subject package format for `data/raw/obama/obama.mp4`
- preprocessing, training, and rendering can all point at the same processed subject directory
- later code does not need to guess where frames, audio, tracking, or splits live
