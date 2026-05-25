## 2024-06-12 - Avoid map.include? chaining for string processing

**Learning:** Chaining `.map { |str| str.split("/").last }.include?(target)` creates massive intermediate array allocations and splits every string in the collection before evaluating the inclusion. Regex matching (`match?`) is also surprisingly slow for simple suffix matching in this context.
**Action:** Always replace `.map { ... }.include?(...)` chains with `.any? { ... }` to allow short-circuiting. For path component suffix matching, use the highly optimized `end_with?("/suffix")` instead of `split` or `match?`.
