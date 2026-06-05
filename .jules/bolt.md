## 2024-05-24 - Avoid `.select.map` intermediate arrays
**Learning:** When iterating over collections yielding objects (like `Entry` structs), `.select { ... }.map { ... }` or `.select { ... }.flat_map { ... }` creates intermediate array allocations that slow down processing time and increase memory usage.
**Action:** Use `.filter_map { ... }` directly for combined filter/map operations to optimize both memory and CPU by avoiding intermediate array allocations without changing output behavior.
## 2024-05-24 - Replace .map.include? with .any? for faster evaluation
**Learning:** Chaining `.map` and `.include?` creates an intermediate array and iterates through the entire collection twice. For arrays, this is slower than using `.any?` which avoids the intermediate array and short-circuits. For hash keys, `.keys.map { ... }.include?(value)` is much slower than `.each_key.any? { ... }`.
**Action:** Use `.any? { |item| item.property == value }` instead of `.map(&:property).include?(value)`, and `.each_key.any? { |key| ... }` instead of `.keys.map { ... }.include?`.
