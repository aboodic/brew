## 2026-05-21 - Optimize array allocations
**Learning:** Using `array += [items]` or `array += collection.flat_map` allocates new intermediate array objects and copies elements, which is less performant and uses more memory than appending directly.
**Action:** Use `array << item1 << item2` or `collection.each { |item| array << item }` to avoid these unnecessary allocations.
