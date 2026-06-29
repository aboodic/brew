## 2024-05-24 - Avoid `.select.map` intermediate arrays
**Learning:** When iterating over collections yielding objects (like `Entry` structs), `.select { ... }.map { ... }` or `.select { ... }.flat_map { ... }` creates intermediate array allocations that slow down processing time and increase memory usage.
**Action:** Use `.filter_map { ... }` directly for combined filter/map operations to optimize both memory and CPU by avoiding intermediate array allocations without changing output behavior.

## 2024-06-29 - Optimize array inclusion checks with string suffix matches
**Learning:** When checking string suffix matches inside enumerables, mapping with `.split('/')` and checking `.include?` creates intermediate array allocations.
**Action:** Use `.each_key.any?` with `.end_with?` to avoid intermediate array allocations and improve processing speed.
