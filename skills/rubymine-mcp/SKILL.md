---
name: rubymine-mcp
description: MANDATORY first check before using grep, Bash search, or Read-based exploration to find/search/rename code in a Ruby or Rails codebase. Do not grep for a class/method definition or run a text search across the repo without checking this skill first — RubyMine's MCP server (via the avelino/mcp CLI) does semantic symbol lookup and indexed search, which is faster and more accurate than text matching.
when_to_use: Trigger on requests like "find where X is defined", "where is X located", "search the codebase for X", "rename X to Y", "find files matching X", "check this file for errors", or any question about Rails routes/controllers/models/views/helpers/mailers.
---

RubyMine's IDE intelligence (index-based search, diagnostics, safe refactors) is available via
`mcp rubymine <tool> '<json>'` ([avelino/mcp](https://github.com/avelino/mcp)). Read only the
file below matching your current need.


Commands take `projectPath: <project_root>` (resolve via `git rev-parse --show-toplevel`) unless
noted otherwise.

## Which file to read

| Need | Read |
|---|---|
| Find where a class/method/field is defined, or get docs for a symbol at a location | [references/symbol-lookup.md](references/symbol-lookup.md) |
| Safely rename a class/method/variable project-wide | [references/rename.md](references/rename.md) |
| Find text or regex matches across the repo | [references/search.md](references/search.md) |
| Check a file for real IDE errors/warnings (beyond linters) | [references/diagnostics.md](references/diagnostics.md) |
| Find files by name/glob, or explore a directory structure | [references/navigation.md](references/navigation.md) |
| Get oriented in an unfamiliar area (deps, modules, repos) | [references/orientation.md](references/orientation.md) |
| Inspect a paired Rails app — routes, controllers, models, views, helpers, mailers | [references/rails.md](references/rails.md) |
| First use this session (do this first) | [references/preflight.md](references/preflight.md) |
| Something failing, or server not registered | [references/setup.md](references/setup.md) |
