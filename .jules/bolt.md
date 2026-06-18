## 2024-05-24 - Avoid `.select.map` intermediate arrays
**Learning:** When iterating over collections yielding objects (like `Entry` structs), `.select { ... }.map { ... }` or `.select { ... }.flat_map { ... }` creates intermediate array allocations that slow down processing time and increase memory usage.
**Action:** Use `.filter_map { ... }` directly for combined filter/map operations to optimize both memory and CPU by avoiding intermediate array allocations without changing output behavior.
## 2024-05-24 - Avoid `.map.include?` intermediate array allocations
**Learning:** When checking if a property of any element in a collection matches a value, `.map(&:property).include?(value)` creates an intermediate array containing all mapped properties, which increases processing time and memory usage.
**Action:** Use `.any? { |item| item.property == value }` to avoid intermediate array allocations and gain processing speed from short-circuiting once a match is found.
