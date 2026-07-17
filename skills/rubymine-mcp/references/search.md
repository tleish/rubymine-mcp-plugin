# Text/regex search



```bash
mcp rubymine search_text '{"q": "authorize_api_request!", "projectPath": "<project_root>"}'
mcp rubymine search_regex '{"q": "def\\s+authorize_\\w+", "projectPath": "<project_root>"}'
```
Fast IntelliJ-indexed search with match coordinates. Prefer these two as the default search tools.

`search_in_files_by_text` / `search_in_files_by_regex` are the older equivalents (`searchText`/`regexPattern` instead of `q`, plus `directoryToSearch`/`fileMask` filters, results wrapped in `||markers||` instead of coordinates) — use them only if you need the directory/file-mask filtering.
