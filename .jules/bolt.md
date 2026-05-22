## 2025-02-12 - Ruby Array allocations in map/select chains
**Learning:** Using `.select { ... }.map(&:...)` or chaining `+=` with `.filter_map(...).map(...)` creates intermediate array allocations that slow down processing time in Ruby.
**Action:** Use `.filter_map { ... }` directly for select-map operations and append using `.each { |x| target << x }` instead of `+=` with mapped collections to avoid intermediate arrays and improve CPU time.
