## 2024-05-24 - Avoid `.select.map` intermediate arrays
**Learning:** When iterating over collections yielding objects (like `Entry` structs), `.select { ... }.map { ... }` or `.select { ... }.flat_map { ... }` creates intermediate array allocations that slow down processing time and increase memory usage.
**Action:** Use `.filter_map { ... }` directly for combined filter/map operations to optimize both memory and CPU by avoiding intermediate array allocations without changing output behavior.
## 2024-05-23 - Optimize Array allocations on inclusions
**Learning:** Chaining `.map(&:property).include?(value)` creates an intermediate array allocation. Using `.any? { |obj| obj.property == value }` is significantly faster as it avoids the allocation and short-circuits.
**Action:** Replace `.map(&:...).include?` patterns with `.any? { ... }` blocks when checking for presence based on object properties.
