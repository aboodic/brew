## 2024-05-14 - Optimize Hash creation

**Learning:** When building a Hash from an Enumerable with an index, the `.each_with_index.flat_map { ... }.to_h` pattern creates large intermediate arrays, causing significant garbage collection overhead and slower execution times. Using `.each_with_index.with_object({})` to build the Hash directly avoids this overhead.

**Action:** Replace `flat_map { ... }.to_h` with `with_object({})` where appropriate to optimize memory usage and speed when constructing Hashes, especially on frequently accessed code paths.
