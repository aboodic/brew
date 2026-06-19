## 2024-05-24 - Avoid `.select.map` intermediate arrays
**Learning:** When iterating over collections yielding objects (like `Entry` structs), `.select { ... }.map { ... }` or `.select { ... }.flat_map { ... }` creates intermediate array allocations that slow down processing time and increase memory usage.
**Action:** Use `.filter_map { ... }` directly for combined filter/map operations to optimize both memory and CPU by avoiding intermediate array allocations without changing output behavior.
## 2024-05-24 - Avoid `.map.include?` combined with string splits in tight loops
**Learning:** Using `.map` with string manipulations like `.split` followed by `.include?` creates intermediate arrays and allocates strings repeatedly.
**Action:** Use `.any?` combined with string suffix matching like `.end_with?` to avoid allocations and fast-path the search.
