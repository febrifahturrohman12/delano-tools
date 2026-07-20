---
description: "Bantuan: daftar semua command /sentry:* dan cara pakai natural language."
allowed-tools: Read
---

Read `${CLAUDE_PLUGIN_ROOT}/reference.md` for config, then show:

## Sentry MCP Commands

| Command | Description |
|---------|-------------|
| `/sentry:issues [query]` | List issues (supports natural language) |
| `/sentry:detail <ID>` | Issue detail + stacktrace |
| `/sentry:fix [ID]` | Full workflow: detect → fix → resolve |
| `/sentry:resolve <ID> [action]` | Resolve, ignore, reopen |
| `/sentry:events [query]` | Search events/logs |
| `/sentry:releases [version]` | List releases |
| `/sentry:help` | This help |

You can also ask in natural language, e.g.: "show recent errors", "fix error in login", "detail issue PROJECT-123".
