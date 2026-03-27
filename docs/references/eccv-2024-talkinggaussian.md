# ECCV 2024: TalkingGaussian

## Full Title

TalkingGaussian: Structure-Persistent 3D Talking Head Synthesis via Gaussian Splatting

## Why It Matters Here

This is one of the best reference papers for this repo's first version because it is:

- audio-driven
- per-subject
- head-focused
- real-time capable
- conceptually understandable

It does not solve every hard problem at once. That makes it useful.

## Main Idea

Keep the Gaussian appearance relatively stable and focus learning on motion-related deformation.

The paper also separates face motion and mouth-interior motion, which is a useful reminder that different facial regions may want different treatment.

## What This Repo Can Learn From It

- a first system does not need to be generalizable
- stable deformation is more important than maximum expressiveness
- freezing or constraining some appearance-related properties can simplify the problem
- separating motion subproblems can reduce instability

## What Not To Copy Blindly

- the full training pipeline
- every preprocessing dependency
- the exact dual-branch design
- paper-specific optimization details before a baseline exists

For this repo, the most important lesson is the design philosophy, not literal reproduction.

## Suggested Takeaway For Version 1

Prefer a stable and constrained avatar over a highly flexible one.

If a design choice makes the rendered head less likely to wobble or drift, it is probably worth considering early.

## What To Defer

- region-specific architectural sophistication
- paper-level optimization for quality and speed
- reproducing reported metrics

## Open Questions

- how much of the stability comes from structure-persistent deformation versus dataset or training details?
- does Version 1 need separate treatment for inside-mouth content, or can that wait?
