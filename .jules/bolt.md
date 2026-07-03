## 2024-05-24 - Avoid `.select.map` intermediate arrays
**Learning:** When iterating over collections yielding objects (like `Entry` structs), `.select { ... }.map { ... }` or `.select { ... }.flat_map { ... }` creates intermediate array allocations that slow down processing time and increase memory usage.
**Action:** Use `.filter_map { ... }` directly for combined filter/map operations to optimize both memory and CPU by avoiding intermediate array allocations without changing output behavior.
## 2024-05-24 - Optimized Linkage Checker Dylib Lookup
**Learning:** Chaining `.keys.map { ... }.include?(...)` with `.split("/")` on a large hash allocates multiple intermediate arrays and performs expensive string splits on every element.
**Action:** Use `.each_key.any? { ... }` with `end_with?` to avoid allocations and short-circuit the evaluation.
