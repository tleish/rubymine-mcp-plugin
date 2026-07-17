# Structural navigation

```bash
mcp rubymine search_file '{"q": "**/*_spec.rb", "projectPath": "<project_root>"}'
mcp rubymine find_files_by_name_keyword '{"nameKeyword": "client", "projectPath": "<project_root>"}'
mcp rubymine list_directory_tree '{"directoryPath": "gems/ship_key/lib/ship_key", "projectPath": "<project_root>"}'
```
`find_files_by_name_keyword` matches filenames only (no glob support) but is faster — prefer it when you just know part of a filename. Use `search_file` for glob matching; add `"paths": ["!**/spec/**"]`-style entries to exclude subpaths.

`directoryPath` above is just an example — substitute the real directory relative to `<project_root>`.
