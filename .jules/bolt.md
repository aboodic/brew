## 2026-05-17 - Avoid temporary arrays in string collection
**Learning:** Using `array += [item]` creates an intermediate array object and copies elements, which is less performant in Ruby compared to using `array << item` or `array.push(items...)`.
**Action:** Use `<<` for single items or `push` for multiple items instead of `+= [...]` when appending elements to an existing array.
