# `+pphl` Production Boundary

This package is reserved for MATLAB R2022b production/codegen candidates. No production algorithm is implemented by the bootstrap.

Planned responsibility areas are `model`, `geometry`, `assignment`, `constraints`, and `solver`. Create a package area only when a real component has an accepted responsibility and test surface.

Rules:

- remain compatible with MATLAB R2022b;
- use explicit interfaces and data-shape contracts;
- do not depend on research-only toolbox conveniences unless separately accepted as production dependencies and codegen-compatible;
- write behavior tests before new production behavior;
- treat generated C/C++ as derived output;
- do not invent unresolved numeric, sizing, memory, timing, or hardware contracts.
