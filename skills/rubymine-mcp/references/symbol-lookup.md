# Symbol lookup



```bash
mcp rubymine search_symbol '{"q": "AccessTokenGenerator", "projectPath": "<project_root>"}'
```
Semantic lookup by class/method/field name fragment — not a text match. Add `"paths": ["providers/**"]` to scope, `"limit": N` to cap results, `"include_external": true` to include gems/SDK symbols.

```bash
mcp rubymine get_symbol_info '{"filePath": "gems/ship_key/lib/ship_key/client.rb", "line": 8, "column": 3, "projectPath": "<project_root>"}'
```
Quick-docs / resolved definition for the symbol at a specific 1-based `line`/`column`. `filePath` is relative to `<project_root>` — substitute a real file path, the one above is just an example.
