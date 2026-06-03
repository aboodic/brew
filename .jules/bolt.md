## 2024-05-24 - Avoid `.select.map` intermediate arrays
**Learning:** When iterating over collections yielding objects (like `Entry` structs), `.select { ... }.map { ... }` or `.select { ... }.flat_map { ... }` creates intermediate array allocations that slow down processing time and increase memory usage.
**Action:** Use `.filter_map { ... }` directly for combined filter/map operations to optimize both memory and CPU by avoiding intermediate array allocations without changing output behavior.

## 2026-06-03 - Avoid string splitting and `.map.include?` for suffix matches
**Learning:** When checking string suffix matches inside enumerables, `keys.map { |l| l.split("/").last }.include?(name)` creates significant overhead through intermediate array allocations (`.keys`, `.map`) and object allocations from `.split`.
**Action:** Use `.each_key.any? { |l| l == name || l.end_with?("/#{name}") }` instead. `.end_with?` is highly optimized in Ruby and performs ~4x faster than string splitting and array iteration in this codebase context.
