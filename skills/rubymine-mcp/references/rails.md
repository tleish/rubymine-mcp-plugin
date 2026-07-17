# Rails introspection (paired Rails repo)

Skip this file entirely if the current project has no paired Rails app.

These tools require pagination (`page`, `page_size`) and give runtime-aware answers (e.g. the
actual resolved routing table), which beats grepping `routes.rb`/`app/controllers` by hand.
Point `projectPath` at the Rails repo root, not the current (non-Rails) project:

```bash
mcp rubymine get_rails_routes '{"page": 1, "page_size": 50, "projectPath": "<rails_project_root>"}'
mcp rubymine get_rails_controllers '{"page": 1, "page_size": 50, "projectPath": "<rails_project_root>"}'
mcp rubymine get_rails_models '{"page": 1, "page_size": 50, "projectPath": "<rails_project_root>"}'
mcp rubymine get_rails_views '{"page": 1, "page_size": 50, "projectPath": "<rails_project_root>"}'
mcp rubymine get_rails_helpers '{"page": 1, "page_size": 50, "projectPath": "<rails_project_root>"}'
mcp rubymine get_rails_mailers '{"page": 1, "page_size": 50, "projectPath": "<rails_project_root>"}'
```
Each also takes `included_fqn_filters`/`excluded_fqn_filters` (regex-ish name filters) and similar directory/view/method filters — see `mcp rubymine --info` for the full schema per tool.
