# MATLAB Harness Bootstrap Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Establish the repository protocol, learning workflow, MATLAB R2022b/codegen contracts, research tracking, and navigable skeleton without adding a production solver or domain algorithm.

**Architecture:** Keep `repository-harness` principles as the repository protocol, add project-specific learning and MATLAB Coder boundaries, and keep the repository as the durable source of truth. MATLAB research code and production/codegen candidates are separated so reference/oracle work can remain flexible while `matlab/+pphl/` stays constrained by the R2022b codegen contract.

**Tech Stack:** Markdown, Git, MATLAB R2022b, MATLAB Coder R2022b.

**Spec:** `docs/superpowers/specs/2026-08-21-matlab-learning-harness-design.md`

## Global Constraints

- MATLAB compatibility baseline is R2022b.
- MATLAB Coder compatibility baseline is R2022b.
- MATLAB is the source of truth for production algorithms; generated C++ is derived.
- Current generated target is portable C++; no hardware-specific optimization is authorized.
- `matlab/research/` may use toolboxes and non-codegen constructs.
- `matlab/+pphl/` is the production/codegen candidate boundary.
- Learn Mode is the default for new concepts; H1 is the default hint level.
- No production solver or domain algorithm is part of this bootstrap.
- No numeric tolerance, array-size limit, runtime deadline, memory policy, or hardware target may be invented in this bootstrap.
- CI is intentionally deferred until a real MATLAB validation path and environment constraints exist.

---

### Task 1: Establish repository routing and workflow

**Files:**
- Create: `AGENTS.md`
- Create: `README.md`
- Create: `docs/WORKFLOW.md`

**Interfaces:**
- Consumes: approved design spec and repository-harness workflow principles.
- Produces: the compact entry point and work-shape routing that all later agents and contributors must follow.

- [x] **Step 1: Create `AGENTS.md`** with only high-value routing rules: repository as system of record, MATLAB R2022b baseline, generated-code ownership, research/production boundary, Learn Mode defaults, human authority gate, durable plan routing, and evidence-before-completion.
- [x] **Step 2: Create `README.md`** describing project purpose, toolchain baseline, repository map, current non-goals, and the first learning milestone.
- [x] **Step 3: Create `docs/WORKFLOW.md`** covering read-only work, Learn/Pair/Execute modes, bounded changes, durable planned work, research experiments, production changes, codegen changes, debugging, validation, and completion reporting.
- [x] **Step 4: Verify** the three files contain no algorithm choice, numeric tolerance, hardware assumption, CI choice, or fabricated validation command.

### Task 2: Record accepted contracts and decisions

**Files:**
- Create: `docs/product/problem-model.md`
- Create: `docs/product/codegen-contract.md`
- Create: `docs/decisions/0001-toolchain-baseline.md`
- Create: `docs/decisions/0002-research-production-boundary.md`
- Create: `docs/decisions/0003-learning-mode-policy.md`

**Interfaces:**
- Consumes: approved design spec.
- Produces: authoritative product/codegen boundaries and lasting decisions future work must inherit.

- [x] **Step 1: Create `problem-model.md`** with sections for purpose, entities, inputs, outputs, decision variables, constraints, objectives, assumptions, unresolved semantics, intended scale, and non-goals; keep unresolved domain semantics explicit rather than guessed.
- [x] **Step 2: Create `codegen-contract.md`** with accepted R2022b facts and an explicit list of intentionally unresolved production contracts such as numeric tolerance, array sizing, dynamic memory, runtime deadline, and target hardware.
- [x] **Step 3: Create the three decision records** for toolchain, research/production boundary, and learning policy, including context, decision, consequences, and status.
- [x] **Step 4: Verify** that decisions agree with the spec and do not promote currently unresolved items into policy.

### Task 3: Establish learning and durable-memory surfaces

**Files:**
- Create: `docs/research/knowledge-map.md`
- Create: `docs/research/mistake-log.md`
- Create: `docs/research/open-questions.md`
- Create: `docs/templates/exec-plan.md`
- Create: `docs/plans/active/.gitkeep`
- Create: `docs/plans/completed/.gitkeep`

**Interfaces:**
- Consumes: Learn Mode policy and repository-harness durable-plan model.
- Produces: persistent learning state, misconception evidence, unresolved-question ownership, and resumable work memory.

- [x] **Step 1: Create `knowledge-map.md`** with the status vocabulary `UNSEEN`, `LEARNING`, `IMPLEMENTED`, `VERIFIED`, `UNDERSTOOD` and initial neutral knowledge areas: mathematical modeling, graph theory, computational geometry, combinatorial optimization, complexity, MATLAB implementation, testing, and MATLAB Coder engineering.
- [x] **Step 2: Create `mistake-log.md`** with a reusable record format containing belief, contradicting evidence, smallest counterexample, root cause/missing concept, learned invariant, and regression evidence.
- [x] **Step 3: Create `open-questions.md`** with only questions already known to be unresolved: geometric-conflict semantics, endpoint-touch policy, numeric precision/tolerance, production size limits, memory policy, runtime budget, and deployment hardware.
- [x] **Step 4: Create `exec-plan.md`** based on repository-harness durable-plan fields: status, outcome, context, scope, approach, risks/recovery, progress, decisions, validation, and result.
- [x] **Step 5: Add plan directory keepers** so the active/completed contract is visible before the first durable task.

### Task 4: Establish MATLAB/test/benchmark navigation skeleton

**Files:**
- Create: `matlab/+pphl/README.md`
- Create: `matlab/research/README.md`
- Create: `tests/README.md`
- Create: `benchmarks/README.md`
- Create: `datasets/synthetic/README.md`
- Create: `codegen/config/README.md`
- Create: `.gitignore`

**Interfaces:**
- Consumes: production/research boundary, validation strategy, generated-artifact policy.
- Produces: visible ownership boundaries without fake code or generated output.

- [x] **Step 1: Create production MATLAB boundary README** documenting the planned package areas (`model`, `geometry`, `assignment`, `constraints`, `solver`) without creating algorithm implementations.
- [x] **Step 2: Create research README** documenting permitted toolbox/reference/experiment/visualization use and the rule that research correctness does not automatically confer production status.
- [x] **Step 3: Create tests README** defining unit, integration, differential, adversarial, and codegen evidence surfaces and the `predict -> RED -> GREEN -> explain` Learn Mode flow.
- [x] **Step 4: Create benchmark and dataset READMEs** defining reproducibility requirements, including generator/dataset version, seed, configuration, instance size, and revision.
- [x] **Step 5: Create codegen config README** documenting that entry points/configuration belong here while generated output is derived and excluded by default.
- [x] **Step 6: Create `.gitignore`** for MATLAB temporary files, MATLAB Coder/code generation output, common compiled objects, editor/OS noise, and local worktree folders; do not ignore authoritative source, tests, docs, configs, or reproducible datasets by default.

### Task 5: Repository-level verification and handoff

**Files:**
- Inspect: all files created by Tasks 1-4
- Inspect: `docs/superpowers/specs/2026-08-21-matlab-learning-harness-design.md`

**Interfaces:**
- Consumes: full bootstrap diff.
- Produces: evidence that the scaffold matches the approved design and contains no accidental domain implementation.

- [x] **Step 1: Compare the feature branch to `main`** and enumerate every changed path.
- [x] **Step 2: Check spec coverage**: toolchain, generated-code ownership, research/production boundary, learning modes, authority gate, durable plans, codegen contract, validation taxonomy, benchmark reproducibility, and deferred CI must each map to a concrete repository artifact.
- [x] **Step 3: Scan for forbidden premature policy**: numeric tolerances, hardware target, runtime deadline, maximum production dimensions, specific production optimization algorithm, production toolbox solver, or CI provider.
- [x] **Step 4: Verify** there is no MATLAB production algorithm or generated C/C++ in the bootstrap diff.
- [x] **Step 5: Review** the diff for Markdown consistency and navigability, then report remaining intentionally unresolved questions.

## Execution Result

Repository-level verification on 2026-08-21 showed the feature branch adds only Harness documentation, contracts, decision records, navigation skeletons, plan keepers, and `.gitignore`. The diff contains no MATLAB production implementation and no generated C/C++ output. MATLAB executable tests are not yet applicable because this bootstrap intentionally introduces no production behavior.

Intentionally unresolved items remain numeric tolerance/representation, production size limits, fixed/variable sizing, memory policy, runtime budget, deployment hardware/runtime, production optimization algorithm, and MATLAB CI/license topology.
