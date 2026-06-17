## 2024-05-24 - Avoid `.select.map` intermediate arrays
**Learning:** When iterating over collections yielding objects (like `Entry` structs), `.select { ... }.map { ... }` or `.select { ... }.flat_map { ... }` creates intermediate array allocations that slow down processing time and increase memory usage.
**Action:** Use `.filter_map { ... }` directly for combined filter/map operations to optimize both memory and CPU by avoiding intermediate array allocations without changing output behavior.
## 2024-05-24 - Avoid `.map.include?` intermediate arrays
**Learning:** Chaining `.map(&:property).include?(value)` creates intermediate array allocations that slow down processing time.
**Action:** Use `.any? { |item| item.property == value }` short-circuit evaluations to optimize CPU usage by avoiding intermediate array allocations.
