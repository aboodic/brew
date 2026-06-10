## 2024-05-24 - Avoid `.select.map` intermediate arrays
**Learning:** When iterating over collections yielding objects (like `Entry` structs), `.select { ... }.map { ... }` or `.select { ... }.flat_map { ... }` creates intermediate array allocations that slow down processing time and increase memory usage.
**Action:** Use `.filter_map { ... }` directly for combined filter/map operations to optimize both memory and CPU by avoiding intermediate array allocations without changing output behavior.

## 2024-05-25 - Avoid multi-line blocks in heredoc string interpolations
**Learning:** When refactoring string interpolations inside heredocs in the Homebrew repository, using multi-line `{ ... }` blocks causes RuboCop's `Style/BlockDelimiters` auto-correct (`bin/brew style --fix`) to format them into invalid `do ... end` blocks containing comments (e.g., `# {' '}`), which can break compilation.
**Action:** Keep block interpolations within heredocs on a single line (e.g., `#{collection.filter_map { |x| x if condition }.join("\n")}`), or refactor the logic outside the heredoc string altogether.
