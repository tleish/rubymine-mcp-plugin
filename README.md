# rubymine-mcp

A Claude Code plugin that teaches Claude to use RubyMine's (or another JetBrains IDE's) MCP
server via the [avelino/mcp](https://github.com/avelino/mcp) CLI — index-based search, real
diagnostics, safe refactors, Rails-aware introspection — instead of grep/Bash/Read, and without
loading RubyMine's ~43 raw MCP tool schemas (~28k tokens) into every prompt.

The CLI queries the live server on demand — Claude reads only the one reference file it needs
for the task at hand, and pays no schema cost until it actually calls a tool.

## Structure

```
.claude-plugin/plugin.json          — plugin manifest
skills/rubymine-mcp/
  SKILL.md                          — always-active index (paths: ["**/*"]); routes to references/
  references/                       — read on demand only, per topic
    preflight.md                    — first-use-this-session check (read this first)
    setup.md                        — troubleshooting (wrong binary, server not registered, etc.)
    symbol-lookup.md, rename.md, search.md, diagnostics.md,
    navigation.md, orientation.md, rails.md
```

## Prerequisites (one-time, per machine)

```bash
brew tap avelino/mcp https://github.com/avelino/mcp.git
brew install avelino/mcp/mcp
```

Enable RubyMine's built-in MCP server — see [JetBrains: Model Context Protocol (MCP)
server](https://www.jetbrains.com/help/idea/mcp-server.html). Then register it with the CLI
(find the port shown in that IDE settings page — it's not fixed across machines/installs):

```bash
mcp add --url http://127.0.0.1:<port>/stream rubymine
```

Use `/stream` (Streamable HTTP transport) — this CLI does not support the legacy `/sse` (HTTP+SSE)
transport that some JetBrains versions also expose.

The CLI's audit-log backend (`chrondb`) may fail to download/initialize, adding a warning and
delay to every call without breaking functionality. If so, disable it once in the CLI's config
(path from `mcp config path`):
```json
{ "audit": { "enabled": false } }
```

## Installing this plugin

From a Claude Code session:

```
/plugin marketplace add tleish/rubymine-mcp-plugin
/plugin install rubymine-mcp@rubymine-mcp
```

For local/dev use instead, without going through the marketplace:

```bash
claude --plugin-dir /path/to/rubymine-mcp-plugin
```

## Full tool accounting (43 tools)

Every tool RubyMine's MCP server exposes, triaged. Nothing here is silently dropped — a tool is
either documented in `references/`, or listed here as deliberately excluded/niche.

### Documented (20)

Covered in the reference files — index-based or semantic capabilities Claude can't get from
Bash/grep/native tools.

### Excluded — redundant with Claude's own tools, or with another documented tool (13)

| Tool | Use instead |
|---|---|
| `read_file`, `get_file_text_by_path` | Read |
| `replace_text_in_file`, `apply_patch` | Edit |
| `create_new_file` | Write |
| `execute_terminal_command` | Bash |
| `find_files_by_glob` | `search_file` — same glob matching, plus multi-pattern `paths` filters with `!`-excludes. `find_files_by_glob` adds subdirectory-scoping and a timeout param, but that's not worth documenting a second tool for. |
| `build_project`, `execute_run_configuration`, `get_run_configurations` | Run the project's own build/test commands directly (e.g. `bundle exec rspec`/`rubocop`) |
| `reformat_file`, `open_file_in_editor` | UI-facing; no-op for an agent |
| `get_all_open_file_paths` | Reflects human IDE editor-tab state; not useful to an autonomous agent |

### Niche / not documented — database tools (10)

`cancel_sql_query`, `execute_sql_query`, `get_database_object_description`,
`list_database_connections`, `list_database_schemas`, `list_recent_sql_queries`,
`list_schema_object_kinds`, `list_schema_objects`, `preview_table_data`,
`test_database_connection`

Only useful when actively debugging live DB state via RubyMine's configured DB connections — not
a general navigation/search need, so not given a reference file. Call these directly with
`mcp rubymine <tool> '<json>'` if that specific need comes up; check `mcp rubymine --info` for
schemas.