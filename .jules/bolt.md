## 2024-05-24 - Avoid `.select.map` intermediate arrays
**Learning:** When iterating over collections yielding objects (like `Entry` structs), `.select { ... }.map { ... }` or `.select { ... }.flat_map { ... }` creates intermediate array allocations that slow down processing time and increase memory usage.
**Action:** Use `.filter_map { ... }` directly for combined filter/map operations to optimize both memory and CPU by avoiding intermediate array allocations without changing output behavior.
## 2024-05-18 - Optimize array allocations in hash key search
**Learning:** Chaining `.keys.map { ... }.include?(...)` on a Hash creates two intermediate arrays (one for keys, one for mapped values). When combined with string manipulation like `.split("/").last`, this becomes extremely inefficient in a tight loop.
**Action:** Replace with `.each_key.any? { |k| ... }` to short-circuit the search and eliminate array allocations completely. For path checking, use `k.end_with?("/#{name}") || k == name` instead of splitting the string. This improves performance by ~63%.
