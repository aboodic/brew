## 2024-05-24 - Avoid `.select.map` intermediate arrays
**Learning:** When iterating over collections yielding objects (like `Entry` structs), `.select { ... }.map { ... }` or `.select { ... }.flat_map { ... }` creates intermediate array allocations that slow down processing time and increase memory usage.
**Action:** Use `.filter_map { ... }` directly for combined filter/map operations to optimize both memory and CPU by avoiding intermediate array allocations without changing output behavior.
## 2024-03-22 - Optimizing Hash Key Matching

**Learning:** When checking conditions on hash keys that require mapping or string manipulation (like splitting to find a filename match), using \`hash.keys.map { ... }.include?(...)\` causes intermediate array allocations. Combined with string splitting, this drastically slows down performance.

**Action:** Use \`hash.each_key.any? { |key| key.end_with?("/#{name}") || key == name }\` to avoid intermediate array allocations and avoid string splitting entirely for a significant (~7x) performance boost.
