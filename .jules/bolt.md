## 2024-05-24 - Avoid `.select.map` intermediate arrays
**Learning:** When iterating over collections yielding objects (like `Entry` structs), `.select { ... }.map { ... }` or `.select { ... }.flat_map { ... }` creates intermediate array allocations that slow down processing time and increase memory usage.
**Action:** Use `.filter_map { ... }` directly for combined filter/map operations to optimize both memory and CPU by avoiding intermediate array allocations without changing output behavior.

## 2024-05-24 - Avoid `.map { ... }.include?` with string manipulation
**Learning:** When checking string suffix matches inside enumerables, `collection.map { |s| s.split("/").last }.include?(value)` is very slow due to intermediate array allocations and string splitting.
**Action:** Use `.any? { |s| s.end_with?(value) && (s == value || s.end_with?("/#{value}")) }` instead. `end_with?` is highly optimized in Ruby and avoiding `.map` saves intermediate array allocations.
