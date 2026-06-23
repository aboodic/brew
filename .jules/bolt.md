## 2024-05-24 - Avoid `.select.map` intermediate arrays
**Learning:** When iterating over collections yielding objects (like `Entry` structs), `.select { ... }.map { ... }` or `.select { ... }.flat_map { ... }` creates intermediate array allocations that slow down processing time and increase memory usage.
**Action:** Use `.filter_map { ... }` directly for combined filter/map operations to optimize both memory and CPU by avoiding intermediate array allocations without changing output behavior.

## 2024-05-24 - Avoid `.keys.map.include?` Hash key checks
**Learning:** Checking Hash key inclusions by mapping keys into a new array (e.g., `hash.keys.map { |l| l.split("/").last }.include?(name)`) allocates multiple intermediate arrays, performs expensive string splitting for all keys regardless of a match, and prevents short-circuit evaluation.
**Action:** Use `hash.each_key.any? { |l| l == name || l.end_with?("/#{name}") }` instead. This provides immediate short-circuiting on the first match and entirely avoids allocating intermediate arrays and strings, leveraging Ruby's fast `String#end_with?` logic.
