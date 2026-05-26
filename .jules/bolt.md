## 2024-05-24 - Avoid `.select.map` intermediate arrays
**Learning:** When iterating over collections yielding objects (like `Entry` structs), `.select { ... }.map { ... }` or `.select { ... }.flat_map { ... }` creates intermediate array allocations that slow down processing time and increase memory usage.
**Action:** Use `.filter_map { ... }` directly for combined filter/map operations to optimize both memory and CPU by avoiding intermediate array allocations without changing output behavior.

## 2024-05-26 - Avoid intermediate array allocations for inclusions checks
**Learning:** Using `.map(&:property).include?(value)` or `.flat_map(&:property).include?(value)` creates intermediate array allocations and processes the entire collection unnecessarily before checking for inclusion.
**Action:** Replace these with `.any? { |item| item.property == value }` (or `.any? { |item| item.property.include?(value) }` for flattened lists) for significant processing speed improvements via short-circuit evaluation.
