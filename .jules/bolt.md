## 2024-05-24 - Avoid `.select.map` intermediate arrays
**Learning:** When iterating over collections yielding objects (like `Entry` structs), `.select { ... }.map { ... }` or `.select { ... }.flat_map { ... }` creates intermediate array allocations that slow down processing time and increase memory usage.
**Action:** Use `.filter_map { ... }` directly for combined filter/map operations to optimize both memory and CPU by avoiding intermediate array allocations without changing output behavior.
## 2024-05-24 - Optimize string matching and avoid intermediate array allocations
**Learning:** When checking conditions on hash keys that require mapping or string manipulation (e.g., `hash.keys.map { |k| k.split("/").last }.include?(value)`), chaining `.map` and `.include?` creates multiple intermediate array allocations. Furthermore, string operations like `.split('/')` are significantly slower than optimized Ruby methods like `end_with?`.
**Action:** Use `.each_key.any?` for short-circuit evaluation to avoid intermediate array allocations, and replace `.split` or `.match?` with optimized methods like `.end_with?` when checking string suffix matches.
