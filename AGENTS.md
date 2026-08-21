# Agent Instructions

## Repository Harness

Start from the requested outcome and treat this repository as the system of record. Read `docs/WORKFLOW.md` and only the product, decision, plan, source, test, codegen, and benchmark material needed for the task.

- MATLAB R2022b and MATLAB Coder R2022b are the authoritative toolchain baseline.
- MATLAB production source is authoritative over generated C/C++. Do not manually repair algorithmic behavior in generated files; fix the owning MATLAB source, interface contract, coder configuration, or generation pipeline and regenerate.
- `matlab/+pphl/` is the production/codegen-candidate boundary. `matlab/research/` may use toolboxes and non-codegen constructs for learning, reference implementations, experiments, and visualization.
- New concepts start in Learn Mode. Default hint level is H1. Do not provide the first complete production implementation for a new concept before the learner attempts one unless the learner explicitly requests a higher hint level or full solution.
- Product semantics and externally observable rules require authority in `docs/product/` or an accepted human decision in `docs/decisions/`. Code patterns, tests, toolbox defaults, and AI preferences do not create product policy.
- If a material semantic choice is unresolved, stop before mutation and request the smallest missing human decision.
- Use one file in `docs/plans/active/` when work spans sessions, has meaningful dependencies, needs recovery context, or cannot be safely resumed from the diff alone. Move it to `docs/plans/completed/` only after validation.
- For production behavior changes, follow test-first development: observe the focused test fail for the intended reason, implement the smallest coherent change, rerun relevant proof, and refactor only while tests stay green.
- For bugs and unexpected behavior, investigate root cause before proposing a fix. Preserve meaningful counterexamples as regression evidence.
- A MATLAB test passing does not by itself prove a codegen-owned component is ready. Codegen-owned entry points require appropriate generation and MATLAB/generated-behavior evidence under the accepted codegen contract.
- Do not invent numeric tolerances, maximum production dimensions, memory policy, execution deadlines, hardware targets, CI infrastructure, or a production optimization algorithm when repository authority has not selected them.
- Claim completion only with fresh executable or observable evidence, or disclose the exact proof that could not be run.

Chat is not durable authority. Promote lasting decisions, unresolved questions, learning evidence, and reusable mistakes into the repository.
