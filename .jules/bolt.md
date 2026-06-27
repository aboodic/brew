## 2024-05-24 - Avoid `.select.map` intermediate arrays
**Learning:** When iterating over collections yielding objects (like `Entry` structs), `.select { ... }.map { ... }` or `.select { ... }.flat_map { ... }` creates intermediate array allocations that slow down processing time and increase memory usage.
**Action:** Use `.filter_map { ... }` directly for combined filter/map operations to optimize both memory and CPU by avoiding intermediate array allocations without changing output behavior.

## 2024-05-24 - Ruby Enumerable Short-Circuiting Performance
**Learning:** Chaining `.map` with `.include?` (e.g. `collection.map(&:property).include?(value)`) forces Ruby to iterate the entire collection and allocate a new array before checking for inclusion. Similarly, `.keys.map` allocates two intermediate arrays (one for keys, one for mapped values).
**Action:** Replace `.map(&:property).include?(value)` with `.any? { |item| item.property == value }`. For hashes, use `.each_key.any?` and optimize string checks with `.end_with?` instead of `.split('/')` for >5x performance gains.
