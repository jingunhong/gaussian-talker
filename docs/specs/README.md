# Specs

This directory defines the implementation-driving specs for Version 1 of `gaussian-talker`.

These docs are no longer just scope placeholders. They are meant to answer:

- what each pipeline stage must produce
- which decisions are fixed for the first working system
- which ideas from the reference projects are worth borrowing now
- which ideas are explicitly deferred

## Current Baseline Anchor

The first complete subject pipeline is anchored to `data/raw/obama/obama.mp4`.

That clip is currently the concrete planning example for Version 1:

- single identity
- monocular talking-head video
- 320 seconds
- 450x450 pixels
- 25 fps
- 48 kHz stereo AAC audio inside MP4

The specs should work for later subjects with similar properties, but they should stay grounded in what is needed to process this clip first.

## Reference Guidance

The most useful reference inputs for these specs are:

- [ECCV 2024 TalkingGaussian](../references/eccv-2024-talkinggaussian.md)
- [WACV 2026 GaussianHeadTalk](../references/wacv-2026-gaussianheadtalk.md)
- [ACM MM 2024 GaussianTalker (Cho et al.)](../references/acm-mm-2024-gaussiantalker-cho.md)
- [ACM MM 2024 GaussianTalker (Yu et al.)](../references/acm-mm-2024-gaussiantalker-yu.md)
- [CVPR 2025 MGGTalk](../references/cvpr-2025-mggtalk.md)

Two reference repos currently provide the most concrete public implementation signals:

- TalkingGaussian: clear preprocessing split, subject-specific training, stable deformation mindset
- GaussianTalker (Cho et al.): explicit dataset contract with `transforms_*.json`, tracking artifacts, and cached audio features

The other references are still important, but mainly as design guidance rather than code to mirror directly.

## Spec List

- [00-project-scope.md](00-project-scope.md)
- [01-repo-foundations.md](01-repo-foundations.md)
- [02-dataset-and-sample-format.md](02-dataset-and-sample-format.md)
- [03-preprocessing-pipeline.md](03-preprocessing-pipeline.md)
- [04-face-motion-targets.md](04-face-motion-targets.md)
- [05-single-identity-avatar.md](05-single-identity-avatar.md)
- [06-audio-to-motion-model.md](06-audio-to-motion-model.md)
- [07-training-workflow.md](07-training-workflow.md)
- [08-inference-and-rendering.md](08-inference-and-rendering.md)
- [09-evaluation-and-debugging.md](09-evaluation-and-debugging.md)

## Repo-Level Decisions

- Internal doc links must stay repo-relative.
- Specs should prefer modular stages over one giant paper-style training script.
- Version 1 optimizes for stability and debuggability before realism or generalization.
- If a future implementation needs a heavier design than what is described here, the spec should be updated first.
