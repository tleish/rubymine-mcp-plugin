# Safe rename



```bash
mcp rubymine rename_refactoring '{"pathInProject": "gems/ship_key/lib/ship_key/client.rb", "symbolName": "OldName", "newName": "NewName", "projectPath": "<project_root>"}'
```
Project-wide, reference-aware rename — safer than sed/grep-replace since it won't touch unrelated identical strings. `pathInProject` is relative to `<project_root>`; the path/names above are just an example, substitute the real ones.
