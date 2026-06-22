## 2024-05-24 - Avoid `.select.map` intermediate arrays
**Learning:** When iterating over collections yielding objects (like `Entry` structs), `.select { ... }.map { ... }` or `.select { ... }.flat_map { ... }` creates intermediate array allocations that slow down processing time and increase memory usage.
**Action:** Use `.filter_map { ... }` directly for combined filter/map operations to optimize both memory and CPU by avoiding intermediate array allocations without changing output behavior.
## 2024-05-24 - Array allocation avoidance in Enumerable methods
**Learning:** Chaining `.map` and `.include?` (e.g. `collection.map(&:property).include?(value)`) or mapping over keys and `.include?` allocates an intermediate array, which degrades performance unnecessarily.
**Action:** Use `.any? { |item| item.property == value }` instead to short-circuit iteration and completely avoid the intermediate array allocation.
