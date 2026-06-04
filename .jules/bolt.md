## 2024-05-24 - Avoid `.select.map` intermediate arrays
**Learning:** When iterating over collections yielding objects (like `Entry` structs), `.select { ... }.map { ... }` or `.select { ... }.flat_map { ... }` creates intermediate array allocations that slow down processing time and increase memory usage.
**Action:** Use `.filter_map { ... }` directly for combined filter/map operations to optimize both memory and CPU by avoiding intermediate array allocations without changing output behavior.

## 2024-06-04 - Optimize String Matching on Hash Keys
**Learning:** When checking for string suffix matches on hash keys (e.g., `hash.keys.map { |k| k.split('/').last }.include?(name)`), using `keys.map` allocates an intermediate array of keys, then another array from `split`, and iterates fully before `include?`. This is extremely slow compared to short-circuiting with `each_key.any?` and using highly optimized string methods like `end_with?`.
**Action:** When searching for a matching string in keys or arrays, avoid `map` followed by `include?`. Use `any?` and check for exact matches or `end_with?` instead of splitting strings.
