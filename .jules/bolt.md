## 2024-05-24 - Avoid `.select.map` intermediate arrays
**Learning:** When iterating over collections yielding objects (like `Entry` structs), `.select { ... }.map { ... }` or `.select { ... }.flat_map { ... }` creates intermediate array allocations that slow down processing time and increase memory usage.
**Action:** Use `.filter_map { ... }` directly for combined filter/map operations to optimize both memory and CPU by avoiding intermediate array allocations without changing output behavior.
## 2024-05-25 - Avoid `.keys.map.include?` with string manipulation
**Learning:** Checking string conditions inside Hash keys using `.keys.map { ... }.include?` creates multiple intermediate allocations (an array of keys, and a mapped array of modified strings) which degrades performance. String manipulation via `split("/")` inside loops further adds overhead.
**Action:** Use `.each_key.any? { ... }` combined with `.end_with?` to short-circuit matching without allocating temporary arrays or splitting strings, providing a significant 4.5x speedup.
