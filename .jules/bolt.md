## 2024-05-18 - Avoid chaining .flat_map.compact.flat_map
**Learning:** Chaining `.flat_map` followed by `.compact.flat_map` creates temporary arrays and adds overhead.
**Action:** Replace this pattern with `.each_with_object([])` combined with manual validation (e.g., safe navigation and nil checks) to build the result array incrementally, reducing overhead and improving CPU execution time, especially when evaluating multiple dependency chains like `casks.each_with_object([]) do |cask, formulae| ... end`.

## 2024-05-18 - Replacing Array += with .concat() avoids memory overhead
**Learning:** Using `array += [items]` creates temporary arrays and duplicates existing ones, significantly impacting CPU usage and memory when executing inside a large loop context like `formulae.each`.
**Action:** Use `.concat()` instead of `+=` to push arrays and mutate the existing accumulator array in-place, offering a significant and measurable performance boost without sacrificing readability.
