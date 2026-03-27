# AGENTS.md

## Purpose

This repository is an implementation-first study project for a practical, single-identity, audio-driven 3D Gaussian Splatting talking head system.

Agents working in this repo should optimize for:

- a small, understandable baseline before ambition
- modular pipeline boundaries that match the project specs
- reproducible local workflows
- minimal dependency sprawl

The repository is still early. When in doubt, preserve clarity and leave obvious extension points instead of premature abstractions.

## Project Scope

Treat Version 1 as:

- single identity
- per-subject training
- head-only rendering
- audio-driven lip and basic facial motion
- stability and debuggability over state-of-the-art quality

Do not quietly expand the repo toward:

- zero-shot identity generalization
- full-body generation
- extreme pose support
- large end-to-end research reproductions
- mixed-framework experiments without explicit approval

Read the relevant spec in `docs/specs/` before making changes to a pipeline stage.

## Source Of Truth

The main repo intent is defined by:

- `README.md`
- `docs/specs/00-project-scope.md`
- `docs/specs/02-dataset-and-sample-format.md`
- `docs/specs/03-preprocessing-pipeline.md`
- `docs/specs/04-face-motion-targets.md`
- `docs/specs/05-single-identity-avatar.md`
- `docs/specs/06-audio-to-motion-model.md`
- `docs/specs/07-training-workflow.md`
- `docs/specs/08-inference-and-rendering.md`
- `docs/specs/09-evaluation-and-debugging.md`

When implementing a feature, keep the code and docs aligned with the relevant spec instead of inventing parallel terminology.

## Approved Stack

- Python is managed with `pyenv`, and the repo is initialized with `uv`.
- The default interpreter should be the newest practical CPython pinned in `.python-version`.
- Use `uv` for dependency management, virtualenv creation, locking, and command execution.
- Use PyTorch as the only ML framework unless the repo owner explicitly approves otherwise.
- NumPy is allowed and expected for array handling, preprocessing, metrics, and interoperability.
- Do not introduce TensorFlow or JAX by default.

Package support may force a Python downgrade later for rendering or CUDA-bound libraries. If that happens, update `.python-version`, `pyproject.toml`, and this file together, and explain the reason in the change.

## Dependency Policy

- Do not add core ML, rendering, tracking, or data packages until they are needed by real code.
- Add dependencies only through `uv add`.
- Keep the base runtime dependency list small.
- Prefer dependency groups or extras for heavier areas such as `audio`, `vision`, `tracking`, `render`, or `train`.
- Avoid overlapping libraries that solve the same problem unless there is a documented reason.
- Prefer PyTorch ecosystem packages over alternative ML stacks when there is a reasonable choice.

## Repository Structure

As code is added, keep it organized around the pipeline:

- `src/gaussian_talker/` for importable project code
- `scripts/` for CLI entrypoints and one-off utilities that are still worth keeping
- `configs/` for experiment and pipeline configuration
- `tests/` for unit and smoke tests
- `docs/` for specs, references, and design notes

Keep boundaries clear between:

- preprocessing
- motion target extraction
- avatar representation
- audio-to-motion modeling
- training orchestration
- inference/rendering
- evaluation/debugging

Do not collapse the whole system into a single monolithic script.

## Data And Artifacts

- Do not commit raw datasets, preprocessed data snapshots, checkpoints, renders, or experiment outputs.
- Keep generated artifacts in dedicated top-level paths such as `data/`, `artifacts/`, `outputs/`, `checkpoints/`, and `renders/`.
- Code should not assume machine-specific absolute paths.
- Internal documentation should use repo-relative links, not local absolute filesystem paths.

## Quality Gates

- Run commands with `uv run`.
- Use `ruff` for linting and formatting.
- Use `pytest` for tests.
- Keep pre-commit hooks fast. Lint and format on commit; run `pytest` on pre-push.
- Add at least a smoke test when introducing new executable workflows.
- Prefer small tests around data contracts, CLI behavior, and utility code over large brittle integration tests.

Useful commands:

- `uv run ruff check .`
- `uv run ruff format .`
- `uv run pytest`
- `uv run pre-commit run --all-files`

## Change Discipline

- Make the smallest coherent change that moves the repo forward.
- If you add a new pipeline component, document where it fits in the specs.
- If you choose a package with CUDA, native extensions, or platform constraints, document that decision near the code and in the relevant setup docs.
- If a design decision conflicts with the Version 1 scope, raise it before implementing it.
