# Decision 0001: Toolchain Baseline

Status: Accepted
Date: 2026-08-21

## Context

The project needs a stable MATLAB and code-generation baseline before production interfaces or algorithms are implemented.

## Decision

Use MATLAB R2022b and MATLAB Coder R2022b. MATLAB is the production algorithm source of truth. C++ is generated through MATLAB Coder. The current target is portable C++ and no deployment hardware is selected.

## Consequences

Production MATLAB must not require APIs introduced after R2022b. Generated C/C++ is derived and is not manually maintained as a parallel implementation. Hardware-specific optimization requires a later accepted decision.
