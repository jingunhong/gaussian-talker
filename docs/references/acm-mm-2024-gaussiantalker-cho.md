# ACM MM 2024: GaussianTalker (Cho et al.)

## Full Title

GaussianTalker: Real-Time High-Fidelity Talking Head Synthesis with Audio-Driven 3D Gaussian Splatting

## Why It Matters Here

This paper is a strong reference for what a more capable per-subject 3DGS talking head system can look like.

It is not my recommended first implementation target for this repo, but it is a useful reference once the baseline direction is clear.

## Main Idea

Use spatially structured Gaussian features and audio-conditioned deformation to drive the avatar at high quality and high speed.

Compared to a more constrained first system, this is a more ambitious design.

## What This Repo Can Learn From It

- per-subject systems can already achieve strong results without generalization
- spatial structure matters when applying audio-driven motion to many Gaussians
- a clear separation between canonical avatar state and per-frame deformation is useful

## What Not To Copy Blindly

- cross-attention-heavy design choices
- richer deformation targets than Version 1 needs
- paper-level complexity introduced before baseline stability is solved

## Suggested Takeaway For Version 1

Treat this as a "Version 2 reference."

After the simplest baseline works, this paper can inform how to improve deformation quality and spatial consistency.

## What To Defer

- higher-capacity audio conditioning
- richer Gaussian attribute prediction
- optimization around real-time performance claims

## Open Questions

- which parts of this paper actually drive the quality improvement versus just increasing complexity?
- which ideas can be imported later without forcing a full redesign?
