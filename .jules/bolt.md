## 2024-05-24 - Avoid `.select.map` intermediate arrays
**Learning:** When iterating over collections yielding objects (like `Entry` structs), `.select { ... }.map { ... }` or `.select { ... }.flat_map { ... }` creates intermediate array allocations that slow down processing time and increase memory usage.
**Action:** Use `.filter_map { ... }` directly for combined filter/map operations to optimize both memory and CPU by avoiding intermediate array allocations without changing output behavior.

## 2024-05-24 - Optimize string suffix matching
**Learning:** When checking string suffix matches inside enumerables, using `.any? { |s| s.end_with?('suffix') }` is significantly faster than mapping with `.split('/')`. `end_with?` is highly optimized in Ruby and avoids allocating intermediate strings and arrays.
**Action:** Replace `collection.map { |s| s.split('/').last }.include?(name)` with `collection.any? { |s| s == name || s.end_with?("/#{name}") }`.
