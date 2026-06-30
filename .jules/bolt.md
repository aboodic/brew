## 2024-05-24 - Avoid `.select.map` intermediate arrays
**Learning:** When iterating over collections yielding objects (like `Entry` structs), `.select { ... }.map { ... }` or `.select { ... }.flat_map { ... }` creates intermediate array allocations that slow down processing time and increase memory usage.
**Action:** Use `.filter_map { ... }` directly for combined filter/map operations to optimize both memory and CPU by avoiding intermediate array allocations without changing output behavior.

## 2024-05-25 - Avoid intermediate array allocations and string allocations with `.include?`
**Learning:** When checking if any transformed element in a collection matches a value (e.g., `hash.keys.map { |x| x.split("/").last }.include?(val)`), chaining `.map` and string operations like `.split` creates unnecessary intermediate arrays and string objects. It also prevents short-circuiting, forcing iteration over the entire collection even if a match is found early.
**Action:** Use `.any?` combined with efficient string matchers like `.end_with?` (e.g., `hash.each_key.any? { |x| x.end_with?("/#{val}") || x == val }`). This avoids intermediate array and string allocations, and short-circuits execution for significant processing speed improvements (measured at ~80% faster in Homebrew's linkage checker).
