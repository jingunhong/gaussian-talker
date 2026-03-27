# References

This directory collects paper notes and reference material for **Simple Gaussian Talking Head**.

Unlike the study repo, this reference set is curated for a different purpose:

- not "what is the full field?"
- but "what should this implementation repo learn from the field?"

The file naming convention is:

`<conference-venue>-<year>-<paper-project-title>.md`

Examples:

- `eccv-2024-talkinggaussian.md`
- `wacv-2026-gaussianheadtalk.md`

## How To Use These Notes

These references are meant to support implementation planning, not to replace reading the original papers.

Each note should help answer:

- why this paper matters to this repo
- which ideas are useful for Version 1
- which ideas should be deferred
- what open questions remain

## Papers Index

Curated references for building the first version of **Simple Gaussian Talking Head**.

This list is not trying to be exhaustive. It prioritizes papers that help decide what to build first and what to postpone.

| Venue | Year | Title | Relevance To This Repo | Priority | Notes |
|------|------|-------|-------------------------|----------|-------|
| ECCV | 2024 | TalkingGaussian | Strong reference for a simple, per-subject, audio-driven baseline with stable deformation | High | Good conceptual starting point for Version 1. [README](eccv-2024-talkinggaussian.md) |
| WACV | 2026 | GaussianHeadTalk | Strong reference for structured motion control and stability-first design | High | Useful for thinking in terms of constrained motion spaces. [README](wacv-2026-gaussianheadtalk.md) |
| ACM MM | 2024 | GaussianTalker (Cho et al.) | Strong reference for a higher-capacity per-subject 3DGS pipeline | Medium | Good to learn from, but not the first implementation target. [README](acm-mm-2024-gaussiantalker-cho.md) |
| ACM MM | 2024 | GaussianTalker (Yu et al.) | Useful reference for FLAME-bound Gaussians and structured deformation | Medium | More complex than needed for Version 1, but valuable conceptually. [README](acm-mm-2024-gaussiantalker-yu.md) |
| CVPR | 2025 | MGGTalk | Useful long-term reference for generalization and monocular reconstruction ideas | Low | Important inspiration for later stages, not for the first build. [README](cvpr-2025-mggtalk.md) |

## Priority Guide

- `High`: directly useful for defining Version 1 scope
- `Medium`: useful after the baseline direction is fixed
- `Low`: better treated as future inspiration than immediate implementation guidance
