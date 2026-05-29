## 2024-05-24 - Avoid `.select.map` intermediate arrays
**Learning:** When iterating over collections yielding objects (like `Entry` structs), `.select { ... }.map { ... }` or `.select { ... }.flat_map { ... }` creates intermediate array allocations that slow down processing time and increase memory usage.
**Action:** Use `.filter_map { ... }` directly for combined filter/map operations to optimize both memory and CPU by avoiding intermediate array allocations without changing output behavior.

## 2024-06-15 - Avoid `.map.include?` and `.split` for inclusion checks
**Learning:** Chaining `.map { ... }.include?(val)` allocates an intermediate array and processes the entire collection before checking for inclusion. Similarly, `.split("/").last` allocates an intermediate array and new string objects.
**Action:** Use `.any? { |obj| obj.property == val }` to short-circuit the check and avoid array allocation. Use string suffix matching like `.end_with?` instead of splitting to avoid array and string allocations.
