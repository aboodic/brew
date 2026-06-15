## 2024-05-24 - Avoid `.select.map` intermediate arrays
**Learning:** When iterating over collections yielding objects (like `Entry` structs), `.select { ... }.map { ... }` or `.select { ... }.flat_map { ... }` creates intermediate array allocations that slow down processing time and increase memory usage.
**Action:** Use `.filter_map { ... }` directly for combined filter/map operations to optimize both memory and CPU by avoiding intermediate array allocations without changing output behavior.
## 2024-06-15 - Optimize Hash Key Matching
**Learning:** When checking conditions on hash keys that require mapping or string manipulation (e.g., `hash.keys.map { |k| transform(k) }.include?(value)`), use `hash.each_key.any? { |k| test(k) }` to avoid allocating an intermediate array of keys and the subsequent mapped array.
**Action:** Replace `hash.keys.map { |k| transform(k) }.include?(value)` with `hash.each_key.any? { |k| test(k) }` for performance improvements.
