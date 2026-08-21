# MATLAB Learning Harness Design

Date: 2026-08-21
Status: Approved design baseline

## 1. Purpose

This repository is a long-lived learning, research, and implementation workspace for a neutral constrained multi-resource assignment problem. The repository must preserve authoritative problem definitions, decisions, plans, MATLAB source, tests, code-generation evidence, and benchmark evidence so that future AI-assisted work can resume from repository truth instead of chat history.

The harness is optimized for two goals at once:

1. help the learner build real understanding through prediction, counterexamples, tests, debugging, and explain-back; and
2. produce MATLAB implementations that can be verified and, where appropriate, converted to portable C++ with MATLAB Coder.

The harness must not treat generated code, chat history, model self-reports, or toolbox defaults as product authority.

## 2. Toolchain Baseline

The authoritative toolchain baseline is:

- MATLAB R2022b.
- MATLAB Coder R2022b.
- MATLAB is the source language.
- C++ is generated through MATLAB Coder rather than maintained as an independent handwritten implementation.
- The current generated-code target is portable C++.
- No hardware-specific optimization is authorized until a target platform is selected and recorded as a repository decision.

Production MATLAB must not rely on syntax or APIs introduced after R2022b.

Generated C/C++ is a derived artifact. Algorithmic defects must be fixed in the owning MATLAB source, interface contract, coder configuration, or generation pipeline and then regenerated. Generated C/C++ must not be manually patched as the source of truth.

## 3. Repository Authority Model

The repository is the system of record. Authority is divided by responsibility rather than by one global file order.

### Product and domain intent

`docs/product/` owns current problem definitions, externally observable semantics, constraints, objectives, assumptions, and declared non-goals.

### Lasting choices

`docs/decisions/` owns accepted decisions that future work must inherit, including toolchain, numeric policy, code-generation boundaries, and architecture choices.

### Architecture

Architecture documents describe accepted component boundaries and data flow. They may explain an accepted rule but do not create product policy that is absent from product authority or a human-approved decision.

### Durable work memory

`docs/plans/active/` owns one durable plan for work that spans sessions, has meaningful dependencies, needs recovery context, or cannot be safely resumed from the diff alone. Validated work moves to `docs/plans/completed/`.

### Executable truth

MATLAB source, tests, generated-code checks, benchmark results, runtime signals, and Git history show what currently exists and what has been observed. They do not silently create new product policy.

### Chat

Chat is not durable authority. Any lasting decision reached in chat must be promoted into the appropriate repository document before future work relies on it.

If a required semantic choice is materially ambiguous, mutation stops and the smallest missing human decision is requested.

## 4. Research and Production Boundary

The repository intentionally separates research freedom from production constraints.

### Research MATLAB

`matlab/research/` may use MATLAB toolboxes, visualization, scripts, exploratory code, brute-force search, slow reference implementations, and non-codegen constructs.

Its purposes include:

- learning and derivation;
- building small exact or trusted reference implementations;
- generating counterexamples;
- validating hypotheses;
- visual analysis;
- comparing algorithm candidates; and
- producing oracle results for small instances.

Research code is not production merely because it returns correct outputs on observed cases.

### Production MATLAB

`matlab/+pphl/` is the production and code-generation candidate boundary.

Production code must be:

- compatible with MATLAB R2022b;
- compatible with MATLAB Coder R2022b for codegen-owned entry points;
- deterministic for a fixed input unless repository authority explicitly permits nondeterminism;
- explicit about public interfaces and data shapes;
- portable with respect to the currently unspecified deployment hardware; and
- covered by behavior-appropriate tests.

Research toolbox APIs may be used to create an oracle without becoming a production dependency.

## 5. Reference and Production Implementations

For algorithmically nontrivial components, the preferred verification pattern is:

1. create a small, understandable reference implementation in `matlab/research/reference/` when feasible;
2. restrict the reference implementation to instance sizes for which its correctness can be trusted and its cost is acceptable;
3. implement the production candidate separately under `matlab/+pphl/`; and
4. compare the two on reproducible small instances.

A reference implementation may be slow, brute-force, or toolbox-assisted. Its job is to provide a trusted comparison surface, not production performance.

Any discrepancy between reference and production output must be treated as a debugging event: reproduce it, minimize the counterexample, form a single hypothesis, test the hypothesis, fix the owning cause, and retain a regression test when the failure is meaningful.

## 6. Learning Harness

New concepts start in Learn Mode by default.

### Modes

#### Learn Mode

The learner owns the first reasoning attempt. The AI acts primarily as tutor, adversarial reviewer, and debugging guide.

For a new concept, the preferred sequence is:

1. state the problem;
2. learner proposes a model or hypothesis;
3. learner predicts behavior on a small example;
4. learner proposes a test or counterexample;
5. AI challenges the reasoning without revealing the full solution prematurely;
6. a failing test demonstrates the missing behavior when implementation work begins;
7. learner attempts the first implementation;
8. AI reviews and guides root-cause debugging;
9. fresh verification is run; and
10. learner explains the governing invariant and failure modes back in their own words.

The default hint level is H1.

Hint levels are:

- H0: no hint;
- H1: one directional question;
- H2: identify the region of the misconception or defect;
- H3: provide a counterexample;
- H4: provide an algorithm idea or structural skeleton;
- H5: explain the full solution;
- H6: provide a complete example implementation.

Unless the learner explicitly requests a higher level, the AI must not provide the first complete production implementation for a new concept before the learner has attempted one.

#### Pair Mode

After the learner has demonstrated adequate understanding of a concept, the AI and learner may jointly design tests, architecture, refactors, and production code.

#### Execute Mode

The AI may take the lead on low-learning-value mechanical work such as repetitive file updates, routine documentation maintenance, deterministic data generation, and other work explicitly delegated by the learner.

### Prediction Gate

Before observing an answer or execution result in Learn Mode, the learner should predict the expected behavior when practical. The workflow is:

`predict -> observe -> explain discrepancy`.

### Counterexample Gate

Understanding requires more than reproducing the successful case. For important concepts, the learner must be able to identify at least one plausible naive approach and a case where that approach fails.

### Explain-Back Gate

Passing code does not imply that the learner understands the concept. A concept may be implemented or verified while the learner remains in `LEARNING` status.

The strongest learning status, `UNDERSTOOD`, requires the learner to explain the governing idea, work a representative example, describe a failure case or counterexample, and transfer the concept to a slightly different example.

### AI Overreach

The following are harness failures in Learn Mode unless explicitly requested:

- revealing the complete solution before a learner attempt;
- silently choosing an unresolved product assumption;
- writing the first complete production implementation for a new concept;
- patching a bug before root-cause investigation; or
- declaring understanding solely because tests pass.

Reusable AI friction should be recorded and may later justify improving repository instructions.

## 7. Knowledge and Mistake Records

`docs/research/knowledge-map.md` tracks concept status using:

- `UNSEEN`;
- `LEARNING`;
- `IMPLEMENTED`;
- `VERIFIED`; and
- `UNDERSTOOD`.

These labels describe learning progress and must not be conflated with software release status.

`docs/research/mistake-log.md` records mistakes that reveal a meaningful gap in the learner's mental model. A useful mistake record includes:

- the prior belief;
- evidence that contradicted it;
- the smallest counterexample;
- the root cause or missing concept;
- the new rule or invariant learned; and
- the regression test or future check, when applicable.

Ordinary typographical mistakes need not be recorded.

`docs/research/open-questions.md` records unresolved semantics or engineering choices. An unresolved item is not permission for an AI agent to invent a default.

## 8. Proposed Repository Structure

The initial repository skeleton is expected to converge toward:

```text
AGENTS.md
README.md
docs/
  WORKFLOW.md
  product/
    problem-model.md
    codegen-contract.md
  decisions/
  research/
    knowledge-map.md
    mistake-log.md
    open-questions.md
    reading-notes/
  plans/
    active/
    completed/
  templates/
  superpowers/
    specs/
    plans/
matlab/
  +pphl/
    +model/
    +geometry/
    +assignment/
    +constraints/
    +solver/
  research/
    reference/
    experiments/
    visualization/
tests/
  unit/
  integration/
  differential/
  adversarial/
  codegen/
benchmarks/
datasets/
  synthetic/
codegen/
  config/
  generated/
```

This structure is a boundary map, not a requirement to create empty directories that have no immediate owner. The first implementation plan may use placeholder-preserving files only where Git requires them and where the path materially improves navigation.

## 9. Initial Product Model Document

`docs/product/problem-model.md` must distinguish at least:

- purpose;
- entities;
- inputs;
- outputs;
- decision variables;
- constraints;
- objectives;
- assumptions;
- unresolved semantics;
- intended scale; and
- non-goals.

The first learning exercise is to build this model before implementing a solver.

Unresolved semantics must be explicitly labeled as unresolved and must not be converted into implementation assumptions by an AI agent.

## 10. Code-Generation Contract

`docs/product/codegen-contract.md` owns the production code-generation contract.

The initial accepted facts are:

- MATLAB R2022b is the baseline;
- MATLAB Coder R2022b is the generator;
- MATLAB production source is authoritative;
- generated C++ is derived;
- the current target is portable C++;
- hardware is not yet selected;
- research MATLAB may use toolbox and non-codegen constructs; and
- production codegen-owned MATLAB must be codegen compatible.

The following are intentionally not yet product requirements and must not be invented by an agent:

- maximum production array dimensions;
- fixed-size versus variable-size policy for each public interface;
- numeric precision and tolerance policy;
- dynamic-memory policy;
- execution deadline;
- target processor or operating system; and
- hardware-specific optimization strategy.

Each of these requires future evidence or an explicit human decision before becoming an invariant.

## 11. Validation Strategy

Correctness evidence precedes performance claims.

### Unit tests

Unit tests verify one focused behavior of a component.

### Integration tests

Integration tests verify that multiple owned components satisfy an end-to-end repository behavior on a controlled instance.

### Differential tests

Differential tests compare a production implementation with a trusted reference implementation or oracle on reproducible small instances.

When a differential discrepancy is found, the smallest useful counterexample should be retained as a regression test.

### Adversarial tests

Adversarial tests target known difficult structures rather than relying only on random data. Examples for neutral geometry and combinatorial optimization may include degenerate geometric configurations, symmetry-heavy instances, infeasible instances, exactly-one-solution instances, and high-conflict or low-conflict cases.

### Test-first development

Production behavior changes follow Red-Green-Refactor:

1. write a focused test that fails for the missing behavior;
2. run it and confirm that it fails for the expected reason;
3. implement the smallest coherent production change;
4. rerun the focused test and relevant neighboring tests;
5. refactor only while tests remain green.

Learn Mode adds prediction before RED and explain-back after GREEN.

## 12. Codegen Verification

A MATLAB test passing does not by itself prove a codegen-owned production component is ready.

For codegen-owned entry points, verification should include, when the component reaches that lifecycle stage:

1. MATLAB behavior tests;
2. successful MATLAB Coder generation under R2022b;
3. a generated-code execution or equivalent supported verification route; and
4. comparison between MATLAB and generated-code behavior under the accepted numeric contract.

The numeric equivalence policy is not yet defined. An agent must not invent a floating-point tolerance such as `1e-6` without authority.

MATLAB Coder entry points should be explicit and finite rather than treating the entire package as an implicit public code-generation interface.

## 13. Generated Artifacts Policy

The repository should commit codegen configuration, public entry-point definitions, interface documentation, and verification scripts when they become real artifacts.

Large generated C/C++ trees, build output, caches, and temporary MATLAB Coder artifacts are not committed by default.

If downstream integration later requires version-controlled generated source, that change requires an explicit repository decision.

## 14. Benchmark Strategy

Benchmarks answer scaling and performance questions; tests answer correctness questions. They are separate evidence surfaces.

A reproducible benchmark must record enough information to rerun the workload, including:

- generator or dataset version;
- random seed when randomness is used;
- problem configuration;
- instance size; and
- algorithm or implementation revision.

Useful metrics may include candidate count, conflict count, constraint count, feasibility, objective value, runtime, memory when measurable, and whether reference comparison and codegen verification were performed.

Algorithm-specific metrics such as search nodes, iterations, optimality gap, preprocessing time, or solver time may be added when an algorithm actually exposes them.

There is currently no authorized execution-time budget because no deployment hardware or system deadline has been selected. Until such authority exists, benchmark evidence records observed scaling and bottlenecks rather than declaring an arbitrary pass/fail latency threshold.

## 15. Software and Learning Status

Software status and learner status are separate.

Useful software evidence labels are:

- `IMPLEMENTED`: code exists;
- `VERIFIED`: correctness evidence exists for the accepted scope;
- `CODEGEN_VERIFIED`: generated behavior has been verified for the accepted codegen contract; and
- `BENCHMARKED`: reproducible scale/performance evidence exists for a defined workload.

A learner may still be `LEARNING` even when software is `CODEGEN_VERIFIED`.

## 16. Initial CI Policy

The first repository iteration uses local validation rather than introducing CI infrastructure prematurely.

GitHub Actions, self-hosted MATLAB runners, or other MATLAB CI infrastructure are not selected in this design because license, runner, environment, and operational constraints are not yet established.

When real automated behaviors exist, CI may be proposed using evidence from the repository's local validation path and actual environment constraints.

## 17. First Commit Boundary

The first implementation commit after this approved design spec should establish repository protocol and skeleton only. It should not contain a real optimization solver or domain algorithm.

Expected initial artifacts include:

- `AGENTS.md` as a compact routing and authority entry point;
- `README.md` with the project and toolchain baseline;
- `docs/WORKFLOW.md` based on repository-harness principles plus Learn/Pair/Execute routing;
- initial product contract documents;
- accepted decision records for the toolchain, research/production boundary, and learning policy;
- research tracking files;
- durable plan structure;
- MATLAB package/research skeleton;
- test and benchmark skeletons where they improve navigation; and
- `.gitignore` rules for MATLAB/Coder generated and transient artifacts.

The first domain exercise after the skeleton is to formulate the neutral problem model without implementing a solver.

## 18. Non-Goals of This Design

This design does not select:

- a deployment processor;
- an operating system;
- an execution deadline;
- numeric tolerances;
- production problem size limits;
- a specific optimization algorithm;
- a specific toolbox solver as production architecture;
- a CI provider or MATLAB license strategy; or
- a handwritten C++ implementation maintained in parallel with MATLAB.

These choices remain future decisions that must be justified by product need, learning goals, or measured evidence.

## 19. Completion Standard

A repository change is complete only when the requested outcome exists or its blocker is explicit, repository authority remains current, behavior-appropriate proof has been freshly run or its absence is disclosed, and any durable active plan accurately records progress and remaining risks.

Descriptions, plans, generated source, benchmark speed, and AI claims do not substitute for observed behavior-level evidence.
