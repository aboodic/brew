## 2024-05-24 - Avoid `.select.map` intermediate arrays
**Learning:** When iterating over collections yielding objects (like `Entry` structs), `.select { ... }.map { ... }` or `.select { ... }.flat_map { ... }` creates intermediate array allocations that slow down processing time and increase memory usage.
**Action:** Use `.filter_map { ... }` directly for combined filter/map operations to optimize both memory and CPU by avoiding intermediate array allocations without changing output behavior.
## 2025-02-14 - Optimize intermediate array allocations for boolean checks
**Learning:** Using `.keys.map { ... }.include?(...)` creates intermediate array allocations that slow down processing time and increase memory usage, particularly inside loop conditions.
**Action:** Use `.each_key.any? { ... }` combined with `.end_with?` check instead to avoid the extra memory allocation overhead and gain significant processing speed improvements (measured at ~2.8x faster for `.any?` compared to `.keys.map.include?` based on testing).
