## 2024-05-24 - Avoid `.select.map` intermediate arrays
**Learning:** When iterating over collections yielding objects (like `Entry` structs), `.select { ... }.map { ... }` or `.select { ... }.flat_map { ... }` creates intermediate array allocations that slow down processing time and increase memory usage.
**Action:** Use `.filter_map { ... }` directly for combined filter/map operations to optimize both memory and CPU by avoiding intermediate array allocations without changing output behavior.

## 2024-06-14 - Optimize Hash Key String Matching
**Learning:** When checking conditions on hash keys that require mapping or string manipulation (like `.keys.map { |k| k.split("/").last }.include?(...)`), it creates expensive intermediate arrays and performs unnecessary string allocations.
**Action:** Use `.each_key.any? { |k| k == name || k.end_with?("/#{name}") }` to utilize short-circuit evaluation and highly optimized string methods (`end_with?`), which avoids intermediate arrays and is significantly faster.
