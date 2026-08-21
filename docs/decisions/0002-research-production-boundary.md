# Decision 0002: Research and Production Boundary

Status: Accepted
Date: 2026-08-21

## Context

Research needs flexible tools while production candidates need a stable codegen-compatible ownership boundary.

## Decision

`matlab/research/` may use toolboxes, visualization, scripts, brute force, reference implementations, and non-codegen constructs. `matlab/+pphl/` is the production/codegen-candidate boundary and must follow the R2022b production contract.

## Consequences

Research/reference implementations may serve as trusted oracles for controlled instances without becoming production dependencies. Moving an idea into production requires explicit tests and codegen-appropriate design rather than a file move alone.
