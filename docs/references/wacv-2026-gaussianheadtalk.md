# WACV 2026: GaussianHeadTalk

## Full Title

GaussianHeadTalk: Wobble-Free 3D Talking Heads with Audio Driven Gaussian Splatting

## Why It Matters Here

This paper is useful because it frames the problem in a structured way:

- represent the head with a constrained avatar
- predict motion in a structured facial parameter space
- prioritize temporal stability

That mindset fits this repo well.

## Main Idea

Instead of asking audio to directly control everything, map audio into a constrained face-model motion space and let the avatar follow that structure.

This reduces freedom, but it can make the output more stable and easier to reason about.

## What This Repo Can Learn From It

- structured motion targets are a good idea for Version 1
- stability is a first-class goal, not a cosmetic improvement
- separating audio-to-motion from rendering makes debugging easier

## What Not To Copy Blindly

- the full transformer-heavy design
- all of the identity/style modeling
- assumptions that depend on source-video head motion transfer

For Version 1, the biggest reusable idea is the separation between motion prediction and rendering.

## Suggested Takeaway For Version 1

Define a small and understandable motion target space early.

If audio predicts a low-dimensional motion representation rather than directly predicting all Gaussian behavior, the system will be easier to train and debug.

## What To Defer

- more advanced style conditioning
- paper-specific stability metrics
- higher-capacity temporal architectures

## Open Questions

- what is the smallest useful motion parameter set for this repo?
- how much structure can be imposed before output quality suffers too much?
