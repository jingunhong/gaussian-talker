# ACM MM 2024: GaussianTalker (Yu et al.)

## Full Title

GaussianTalker: Speaker-specific Talking Head Synthesis via 3D Gaussian Splatting

## Why It Matters Here

This paper is relevant because it provides another structured way to think about avatar deformation: bind Gaussians to a face model and let learned motion act through that structure.

That concept is more important to this repo than the exact paper pipeline.

## Main Idea

Use a structured face representation to constrain Gaussian motion, and predict speaker-specific facial dynamics from audio-derived features.

The result is more interpretable than fully free-form Gaussian motion.

## What This Repo Can Learn From It

- structured deformation is a valid simplification, not a weakness
- it can be useful to make avatar motion easier to reason about even if expressiveness is reduced
- audio-to-motion and avatar representation should fit each other conceptually

## What Not To Copy Blindly

- the full contrastive disentanglement setup
- speaker-specific modeling ambitions beyond Version 1 needs
- training complexity that is not justified for a first implementation

## Suggested Takeaway For Version 1

If the repo adopts a constrained avatar representation, this paper supports that direction.

It is especially useful as conceptual backing for not starting with fully free-form Gaussian control.

## What To Defer

- speaker-content disentanglement
- stronger cross-speaker behavior
- long training pipelines aimed at better final metrics

## Open Questions

- what is the minimum structured representation needed before it becomes too rigid?
- how much simplicity does this approach buy in practice for a first implementation?
