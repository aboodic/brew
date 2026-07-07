## 2024-05-24 - Avoid `.select.map` intermediate arrays
**Learning:** When iterating over collections yielding objects (like `Entry` structs), `.select { ... }.map { ... }` or `.select { ... }.flat_map { ... }` creates intermediate array allocations that slow down processing time and increase memory usage.
**Action:** Use `.filter_map { ... }` directly for combined filter/map operations to optimize both memory and CPU by avoiding intermediate array allocations without changing output behavior.
## 2024-07-07 - Avoid mapping keys of large hashes to check inclusion

**Learning:** When checking conditions on hash keys that require mapping or string manipulation (e.g., `hash.keys.map { ... }.include?(...)`), use `hash.each_key.any? { ... }` instead. The former allocates an intermediate array of keys and maps the entire collection before checking inclusion, whereas `any?` evaluates lazily, avoids array allocations, and short-circuits. Also, `end_with?` is highly optimized in Ruby and performs significantly faster than string splitting.
**Action:** Replace chained `.keys.map.include?` calls with `.each_key.any?` and use `end_with?` for suffix matching to achieve significant memory and CPU processing speed improvements, especially in performance-sensitive logic like dependency/linkage checking.
