# Preflight: is this project actually indexed?

Not every Ruby codebase Claude works in has been opened/indexed by RubyMine, and RubyMine's MCP
server may be running with a *different* project open (or none at all). Do this check once per
session, before the first use of any tool in this index:

```bash
mcp rubymine get_repositories '{"projectPath": "<project_root>"}'
```

- Normal result (`"isError"` absent or `false`) → this project is open and indexed right now.
  Use the tools in this index freely for the rest of the session.
- `"isError": true` with a message like `doesn't correspond to any open project` → RubyMine does
  NOT have this project open right now. The error lists currently open projects for confirmation.
  **Stop trying these tools and fall back to grep/Read/Bash for the rest of the session.** Don't
  retry per-call; this is a one-time gate.
- Any other error (connection refused, server not found in config, etc.) → read [setup.md](setup.md).
