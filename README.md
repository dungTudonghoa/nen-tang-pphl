# nen-tang-pphl

A MATLAB-first learning, research, and implementation workspace for a neutral constrained multi-resource assignment problem.

## Toolchain Baseline

- MATLAB R2022b.
- MATLAB Coder R2022b.
- MATLAB is the source of truth for production algorithms.
- Generated C++ is a derived artifact.
- The current generated target is portable C++.
- Deployment hardware, runtime budget, numeric tolerance, production size limits, and memory policy are intentionally not selected yet.

## Repository Model

- `AGENTS.md`: compact entry point for AI-assisted work.
- `docs/WORKFLOW.md`: work-shape routing, learning modes, planning, debugging, validation, and completion rules.
- `docs/product/`: current product/domain contracts.
- `docs/decisions/`: lasting accepted choices.
- `docs/research/`: knowledge progress, mistakes, and unresolved questions.
- `docs/plans/`: durable working memory for multi-session or recovery-sensitive work.
- `docs/superpowers/`: approved design specs and implementation plans.
- `matlab/+pphl/`: production/codegen-candidate MATLAB boundary.
- `matlab/research/`: flexible research, reference, experiment, and visualization space.
- `tests/`: correctness and codegen evidence guidance.
- `benchmarks/`: reproducible scale/performance evidence.
- `datasets/synthetic/`: reproducible synthetic workloads.
- `codegen/config/`: code-generation entry-point/configuration ownership.

## Learning Model

New concepts begin in Learn Mode. The default flow is:

`predict -> model/hypothesis -> counterexample -> RED -> learner attempt -> GREEN -> explain-back`

The default hint level is H1: one directional question. A concept is not considered understood merely because an implementation passes tests.

## Research and Production Boundary

Research MATLAB may use toolboxes, brute force, slow reference implementations, plots, and non-codegen constructs. Production candidates under `matlab/+pphl/` must remain compatible with the R2022b production/codegen contract.

Reference or toolbox-backed results may act as an oracle for small controlled instances without becoming production architecture.

## Current Milestone

The first domain milestone is to formulate the neutral problem model in `docs/product/problem-model.md` before implementing a solver.

No production optimization algorithm is selected by the bootstrap.

## Design Authority

The approved harness design is in:

`docs/superpowers/specs/2026-08-21-matlab-learning-harness-design.md`
