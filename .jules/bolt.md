## 2024-05-24 - Avoid `.select.map` intermediate arrays
**Learning:** When iterating over collections yielding objects (like `Entry` structs), `.select { ... }.map { ... }` or `.select { ... }.flat_map { ... }` creates intermediate array allocations that slow down processing time and increase memory usage.
**Action:** Use `.filter_map { ... }` directly for combined filter/map operations to optimize both memory and CPU by avoiding intermediate array allocations without changing output behavior.

## 2024-06-24 - Avoid mapping hash keys array to search for matching suffixes
**Learning:** When searching for a matching suffix across hash keys, extracting keys into an array (`.keys`), mapping that array with `split` (`.map { |k| k.split("/").last }`), and then calling `.include?` allocates two intermediate arrays and strings per element, slowing execution time significantly.
**Action:** Iterate directly over the hash keys and use block matching with optimized C extension methods (e.g., `.each_key.any? { |k| k == name || k.end_with?("/#{name}") }`) to avoid intermediate allocations and short-circuit early upon a match.
