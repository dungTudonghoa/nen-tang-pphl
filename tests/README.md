# Test and Verification Surfaces

Tests prove defined behavior; benchmarks measure scale/performance. Keep those roles separate.

Planned evidence categories:

- **Unit:** one focused local behavior.
- **Integration:** behavior across owned component boundaries.
- **Differential:** production result compared with a trusted reference/oracle on controlled small instances.
- **Adversarial:** deliberately difficult, degenerate, symmetric, infeasible, or boundary cases.
- **Codegen:** MATLAB Coder generation and generated-behavior evidence for explicit codegen-owned entry points.

For new production behavior use test-first development: observe RED for the expected missing behavior, implement the smallest coherent change, then observe GREEN. In Learn Mode the preferred loop is `predict -> RED -> learner attempt -> GREEN -> explain`.

When a meaningful discrepancy is found, minimize it and retain it as regression evidence.
