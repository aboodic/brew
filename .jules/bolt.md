## 2024-05-24 - Avoid `.select.map` intermediate arrays
**Learning:** When iterating over collections yielding objects (like `Entry` structs), `.select { ... }.map { ... }` or `.select { ... }.flat_map { ... }` creates intermediate array allocations that slow down processing time and increase memory usage.
**Action:** Use `.filter_map { ... }` directly for combined filter/map operations to optimize both memory and CPU by avoiding intermediate array allocations without changing output behavior.
## 2024-07-01 - Avoid intermediate array allocations in inclusion checks
**Learning:** Chaining `.map` and `.include?` creates unnecessary intermediate array allocations, slowing down performance.
**Action:** Use `.any?` short-circuit evaluations with comparisons or suffix matching (`.end_with?`) to avoid allocating intermediate arrays and speed up inclusion checking.
