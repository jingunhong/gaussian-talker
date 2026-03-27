# CVPR 2025: MGGTalk

## Full Title

Monocular and Generalizable Gaussian Talking Head Animation

## Why It Matters Here

This paper matters mostly as a reminder of what this repo is **not** trying to do first.

It is an important long-term reference because it tackles:

- generalization
- monocular reconstruction
- one-shot usage
- broader deployment practicality

But those are later goals.

## Main Idea

Avoid per-subject optimization by learning a generalizable pipeline that can build and animate a head from very limited subject input.

That is compelling, but much harder than the first version this repo wants.

## What This Repo Can Learn From It

- generalization is a separate problem and should be treated as such
- monocular geometry bootstrapping is valuable for future work
- future versions may want to reduce subject-specific setup cost

## What Not To Copy Blindly

- the full one-shot ambition
- heavy reconstruction machinery
- generalization goals before a single-subject baseline works

## Suggested Takeaway For Version 1

Use this paper as a boundary marker.

If a design starts drifting toward one-shot or generalizable talking heads, it is probably leaving the intended scope of Version 1.

## What To Defer

- generalizable avatar creation
- symmetry-based full-head reconstruction
- training for unseen identities

## Open Questions

- which parts of the monocular setup become useful only after the per-subject pipeline is solid?
- when would it be worth moving from personalized avatars toward generalizable ones?
