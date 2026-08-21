# Code Generation Configuration

This directory owns durable MATLAB Coder entry-point and configuration material when real codegen-owned components exist.

The baseline is MATLAB Coder R2022b targeting portable C++. Entry points must be explicit and finite. Configuration and verification scripts may be committed; generated source trees, caches, and build output are derived and excluded by default.

Numeric tolerance, interface sizing, memory policy, runtime deadline, and deployment hardware remain unresolved until explicitly accepted.
