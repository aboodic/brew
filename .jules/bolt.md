## 2024-05-24 - Avoid `.select.map` intermediate arrays
**Learning:** When iterating over collections yielding objects (like `Entry` structs), `.select { ... }.map { ... }` or `.select { ... }.flat_map { ... }` creates intermediate array allocations that slow down processing time and increase memory usage.
**Action:** Use `.filter_map { ... }` directly for combined filter/map operations to optimize both memory and CPU by avoiding intermediate array allocations without changing output behavior.

## 2024-05-23 - Avoid .map.include? chaining in Ruby enumerables
**Learning:** Intermediate array allocations from chaining `.map` and `.include?` cause overhead, especially in loops. Short-circuit evaluations via `.any?` short-circuit array allocations and perform significantly faster.
**Action:** Replace `.map(&:method).include?(val)` or `.map { |x| x.method }.include?(val)` with `.any? { |x| x.method == val }`.
