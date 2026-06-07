## 2024-05-24 - Avoid `.select.map` intermediate arrays
**Learning:** When iterating over collections yielding objects (like `Entry` structs), `.select { ... }.map { ... }` or `.select { ... }.flat_map { ... }` creates intermediate array allocations that slow down processing time and increase memory usage.
**Action:** Use `.filter_map { ... }` directly for combined filter/map operations to optimize both memory and CPU by avoiding intermediate array allocations without changing output behavior.
## 2024-06-07 - Avoid `.keys.map.include?` for string matching on hash keys
**Learning:** When checking conditions on hash keys that require mapping or string manipulation (e.g., `hash.keys.map { ... }.include?(...)`), it creates intermediate array allocations (`.keys` array and the mapped array) that slow down processing time.
**Action:** Use `hash.each_key.any? { ... }` with direct string comparison operations like `==` or `.end_with?` to avoid intermediate array allocations and improve execution speed significantly.
