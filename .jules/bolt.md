## 2024-05-24 - Avoid `.select.map` intermediate arrays
**Learning:** When iterating over collections yielding objects (like `Entry` structs), `.select { ... }.map { ... }` or `.select { ... }.flat_map { ... }` creates intermediate array allocations that slow down processing time and increase memory usage.
**Action:** Use `.filter_map { ... }` directly for combined filter/map operations to optimize both memory and CPU by avoiding intermediate array allocations without changing output behavior.
## 2025-02-18 - Avoid map array allocation inside hash iteration loops
**Learning:** Checking string suffix presence on hash keys using `.keys.map { |k| k.split("/").last }.include?(name)` allocates multiple intermediate arrays on every check.
**Action:** Use `.each_key.any? { |k| k == name || k.end_with?("/#{name}") }` to avoid object allocation and short-circuit evaluation.
