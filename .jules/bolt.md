## 2024-05-24 - Avoid `.select.map` intermediate arrays
**Learning:** When iterating over collections yielding objects (like `Entry` structs), `.select { ... }.map { ... }` or `.select { ... }.flat_map { ... }` creates intermediate array allocations that slow down processing time and increase memory usage.
**Action:** Use `.filter_map { ... }` directly for combined filter/map operations to optimize both memory and CPU by avoiding intermediate array allocations without changing output behavior.
## 2024-05-24 - Avoid `.keys.map.include?` string splitting on Hashes
**Learning:** In Ruby, `hash.keys.map { |k| k.split("/").last }.include?(name)` allocates multiple intermediate arrays and performs expensive string splits on every iteration. This is a common bottleneck when checking linkages or paths.
**Action:** Use `.each_key.any?` with direct equality and `.end_with?` to avoid array allocations and string splitting (e.g., `hash.each_key.any? { |k| k == name || k.end_with?("/#{name}") }`). This yields over a 6x speedup.
