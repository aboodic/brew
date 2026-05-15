## 2026-05-15 - Array Concatenation Optimization
**Learning:** Using `+=` to build an array creates multiple intermediate arrays, causing unnecessary memory allocation and performance overhead in Ruby. This can be significantly slower than modifying the array directly.
**Action:** Use `.push` or `.concat` to add elements to an array dynamically without creating intermediate object allocations. Using `.each` with `.push` for mapping directly avoids allocating array outputs like `flat_map` does when appending to a parent array.
