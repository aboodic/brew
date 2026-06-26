## 2024-05-24 - Avoid `.select.map` intermediate arrays
**Learning:** When iterating over collections yielding objects (like `Entry` structs), `.select { ... }.map { ... }` or `.select { ... }.flat_map { ... }` creates intermediate array allocations that slow down processing time and increase memory usage.
**Action:** Use `.filter_map { ... }` directly for combined filter/map operations to optimize both memory and CPU by avoiding intermediate array allocations without changing output behavior.

## 2024-06-26 - String matching optimization in collections
**Learning:** When checking string suffix matches inside enumerables, extracting keys with `.keys`, creating intermediate arrays with `.map`, and using `.split("/")` before `.include?` is significantly slower than direct string matching.
**Action:** Use `.each_key.any? { |l| l == name || l.end_with?("/#{name}") }` instead. `end_with?` is highly optimized in Ruby and avoids allocating intermediate arrays, performing significantly faster than string splitting or mapping.
