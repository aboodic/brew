## 2024-05-24 - Avoid `.select.map` intermediate arrays
**Learning:** When iterating over collections yielding objects (like `Entry` structs), `.select { ... }.map { ... }` or `.select { ... }.flat_map { ... }` creates intermediate array allocations that slow down processing time and increase memory usage.
**Action:** Use `.filter_map { ... }` directly for combined filter/map operations to optimize both memory and CPU by avoiding intermediate array allocations without changing output behavior.

## 2024-05-24 - String match optimization over collections
**Learning:** When checking string suffix matches inside enumerables, using `.map { |s| s.split("/").last }.include?(...)` creates intermediate arrays and string objects, slowing down execution time.
**Action:** Use `.any? { |s| s == name || s.end_with?("/#{name}") }` instead. `end_with?` is highly optimized in Ruby and performs significantly faster than string splitting or regex matching, while `.any?` short-circuits.
