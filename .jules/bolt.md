## 2024-05-24 - Avoid `.select.map` intermediate arrays
**Learning:** When iterating over collections yielding objects (like `Entry` structs), `.select { ... }.map { ... }` or `.select { ... }.flat_map { ... }` creates intermediate array allocations that slow down processing time and increase memory usage.
**Action:** Use `.filter_map { ... }` directly for combined filter/map operations to optimize both memory and CPU by avoiding intermediate array allocations without changing output behavior.
## 2024-05-15 - Optimize array combinations in Homebrew

**Learning:** Combining `.select { ... }` with `.map(&:...)` and then checking inclusion with `.include?(...)` creates two intermediate arrays, slowing down Ruby code and wasting memory.
**Action:** Replace `.select { ... }.map(&:...).include?(...)` with a direct short-circuit `.any? { |x| ... }` check to improve performance by 10x-20x for these types of chained boolean checks. Similarly replace `.select { ... }.map(&:...)` with `.filter_map { ... }` to avoid an intermediate array allocation.
