# File problems (real diagnostics)



```bash
mcp rubymine get_file_problems '{"filePath": "gems/ship_key/lib/ship_key/client.rb", "projectPath": "<project_root>"}'
```
Runs IntelliJ's actual inspections on a file — catches things a linter/Bash won't. Add `"errorsOnly": true` to filter warnings out. `filePath` is relative to `<project_root>`; substitute the real file.
