## 2024-05-24 - Optimize Hash Construction with with_object

**Learning:** Using `flat_map { ... }.to_h` allocates significant intermediate arrays, degrading memory efficiency and speed. Microbenchmarks show that building the hash directly using `with_object({})` avoids temporary array creation and is about 20% faster.

**Action:** Avoid `flat_map { ... }.to_h` when constructing hashes. Always prefer `each_with_index.with_object({})` or `with_object({})` to build hashes directly.
