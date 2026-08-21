# Repository Workflow

The repository is the system of record for accepted intent, decisions, durable plans, MATLAB source, tests, codegen evidence, benchmark evidence, and unresolved questions.

## Start With The Work Shape

### Read-only request
Inspect only the smallest authoritative surface needed to answer, review, explain, diagnose, or plan. Discovery does not authorize edits.

### Learn Mode
Default for a new concept. Use `predict -> hypothesis/model -> counterexample -> RED -> learner implementation attempt -> GREEN -> explain-back`. Default hint level is H1. Increase hint level only when the learner requests it.

### Pair Mode
Use after the learner has demonstrated adequate understanding. The learner and AI may jointly design tests, interfaces, refactors, and implementations while preserving authority and verification gates.

### Execute Mode
Use for explicitly delegated low-learning-value mechanical work such as repetitive documentation, deterministic data generation, or repository maintenance.

### Bounded engineering change
Inspect authority, affected behavior, and existing proof. Make the smallest coherent change and run focused verification. A durable plan is not required when the work can be safely understood and resumed from the request and diff.

### Durable planned work
Create or resume one file in `docs/plans/active/` when work spans sessions, has meaningful dependencies, needs recovery context, or cannot be safely resumed from the diff. Keep progress, task-local decisions, risks, recovery, and validation current. Move it to `docs/plans/completed/` only after validation.

## Authority Gate

`docs/product/` owns current domain/product semantics. `docs/decisions/` owns lasting accepted choices. Tests, source patterns, toolbox defaults, generated code, and AI preferences do not create policy.

If a required choice has materially different valid interpretations, stop before mutation and request the smallest missing human decision. In particular, do not invent numeric tolerances, production dimensions, memory policy, runtime deadlines, hardware targets, CI topology, or a production optimization algorithm.

## Research Experiment

Research work may use `matlab/research/`, toolboxes, brute force, slow reference implementations, visualization, and scripts. Record reproducibility inputs when an experiment supports a conclusion. Research code does not become production merely because observed cases pass.

## Production MATLAB Change

`matlab/+pphl/` is the production/codegen-candidate boundary. Production changes must remain compatible with MATLAB R2022b. When a behavior changes, use test-first development: write a focused failing test, observe the expected failure, implement the smallest coherent change, rerun relevant tests, and refactor only while green.

## Codegen Change

MATLAB production source is authoritative; generated C/C++ is derived. Do not patch generated algorithmic behavior directly. For codegen-owned entry points, verify MATLAB behavior, successful R2022b generation, and generated behavior/equivalence under the accepted numeric contract when that contract exists.

## Debugging

For any unexpected behavior: reproduce, inspect evidence, compare working and failing patterns, form one hypothesis, test it minimally, then fix the root cause. Preserve meaningful minimized counterexamples as regression evidence and learning records.

## Validation Surfaces

Use focused unit tests for local rules, integration tests for component boundaries, differential tests against trusted reference/oracle implementations, adversarial tests for difficult structures, and codegen tests for generated boundaries. Benchmarks measure scaling; they do not prove correctness.

## Completion Report

Report the outcome, repository changes, fresh evidence run, unresolved risks, and unattempted proof. A plan, code diff, benchmark speed, or AI self-report does not substitute for behavior-level evidence.
