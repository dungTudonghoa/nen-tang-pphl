# Benchmarks

Benchmarks record observed scaling and bottlenecks; they do not prove correctness and currently have no arbitrary pass/fail latency budget.

Every reproducible benchmark should record:

- generator or dataset version;
- random seed when randomness is used;
- problem configuration;
- instance size;
- algorithm/implementation revision;
- relevant structural counts such as candidates, conflicts, or constraints when available;
- feasibility/objective information when defined;
- runtime and memory when measurable; and
- whether reference comparison and codegen verification were performed.

Add algorithm-specific metrics only when the selected algorithm exposes meaningful measurements.
