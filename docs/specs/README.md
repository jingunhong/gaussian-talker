# Specs

This directory defines the high-level specs for the first version of **Simple Gaussian Talking Head**.

The number prefix indicates the intended implementation order, not importance. Earlier specs should reduce ambiguity for later specs.

These documents are intentionally high level:

- they define what needs to exist
- they make scope and non-goals explicit
- they avoid locking the repo into one implementation too early

## Spec List

- [00-project-scope.md](/Users/jingunhong/Repos/gaussian-talking-head-study/simple-gaussian-talking-head/docs/specs/00-project-scope.md)
- [01-repo-foundations.md](/Users/jingunhong/Repos/gaussian-talking-head-study/simple-gaussian-talking-head/docs/specs/01-repo-foundations.md)
- [02-dataset-and-sample-format.md](/Users/jingunhong/Repos/gaussian-talking-head-study/simple-gaussian-talking-head/docs/specs/02-dataset-and-sample-format.md)
- [03-preprocessing-pipeline.md](/Users/jingunhong/Repos/gaussian-talking-head-study/simple-gaussian-talking-head/docs/specs/03-preprocessing-pipeline.md)
- [04-face-motion-targets.md](/Users/jingunhong/Repos/gaussian-talking-head-study/simple-gaussian-talking-head/docs/specs/04-face-motion-targets.md)
- [05-single-identity-avatar.md](/Users/jingunhong/Repos/gaussian-talking-head-study/simple-gaussian-talking-head/docs/specs/05-single-identity-avatar.md)
- [06-audio-to-motion-model.md](/Users/jingunhong/Repos/gaussian-talking-head-study/simple-gaussian-talking-head/docs/specs/06-audio-to-motion-model.md)
- [07-training-workflow.md](/Users/jingunhong/Repos/gaussian-talking-head-study/simple-gaussian-talking-head/docs/specs/07-training-workflow.md)
- [08-inference-and-rendering.md](/Users/jingunhong/Repos/gaussian-talking-head-study/simple-gaussian-talking-head/docs/specs/08-inference-and-rendering.md)
- [09-evaluation-and-debugging.md](/Users/jingunhong/Repos/gaussian-talking-head-study/simple-gaussian-talking-head/docs/specs/09-evaluation-and-debugging.md)

## Notes

- These specs are for Version 1, not the long-term vision.
- Generalization, emotion control, and SOTA ambitions are intentionally deferred.
- The main purpose is to make the required work visible before code grows.
