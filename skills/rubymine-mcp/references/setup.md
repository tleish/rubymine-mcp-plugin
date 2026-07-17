# Setup / troubleshooting

Read this only if the [preflight check](preflight.md) fails with something other than the
"no open project" message, or a `mcp rubymine ...` call otherwise fails.

## `mcp` resolves to the wrong binary

Some machines also have an unrelated Python "MCP SDK" package installed as `mcp`. Symptom:
`Error: typer is required. Install with 'pip install mcp[cli]'`. Fix: run `which -a mcp`, find
the entry that isn't under an asdf/pyenv/rbenv/mise shim dir, and invoke that one directly (or
fix PATH ordering).

## RubyMine server not registered

Run `mcp --list` to check. If missing:
1. Find the port RubyMine is listening on (IDE's MCP/AI settings, or ask the user).
2. `mcp add --url http://127.0.0.1:<port>/stream rubymine` — use `/stream` (Streamable HTTP),
   not `/sse` (legacy SSE transport, unsupported by this CLI).

## Slow calls / chrondb warnings

The audit-log backend can fail to download/init, adding delay without breaking functionality.
Disable it once: add to the CLI config (path from `mcp config path`):
```json
{ "audit": { "enabled": false } }
```

## `<rails_project_root>` (used in `rails.md`)

Only applies if this project has a paired Rails app in a separate repo. Check the project's
CLAUDE.md/CLAUDE.local.md for the documented sibling-repo path; don't guess a relative path. No
paired Rails app → skip `rails.md`.
