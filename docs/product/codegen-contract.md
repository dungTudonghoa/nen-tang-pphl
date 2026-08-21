# MATLAB Coder Contract

## Accepted Baseline

- MATLAB: R2022b.
- MATLAB Coder: R2022b.
- Production source of truth: MATLAB.
- Production/codegen candidate boundary: `matlab/+pphl/`.
- Generated target: portable C++.
- Generated C/C++ is derived and must not be manually patched as algorithm authority.
- `matlab/research/` may use toolboxes and non-codegen constructs and is not automatically codegen-owned.

## Codegen Ownership

Codegen entry points must be explicit and finite. If generated behavior is wrong, investigate the owning MATLAB source, public interface/type contract, coder configuration, or generation pipeline and regenerate.

## Verification Expectation

When a component becomes codegen-owned, evidence should include MATLAB behavior tests, successful generation on the R2022b baseline, execution through an accepted generated-code verification route, and comparison with MATLAB behavior under the accepted numeric contract.

## Intentionally Unresolved Contracts

The following are not authorized defaults:

- maximum input or array dimensions;
- fixed-size versus variable-size policy for public interfaces;
- floating-point precision or equivalence tolerance;
- dynamic-memory policy;
- execution deadline;
- target processor, operating system, or runtime;
- hardware-specific optimization strategy.

A future human decision or accepted product requirement must establish each before it becomes an invariant.
