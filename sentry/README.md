# sentry — Sentry error-tracking via MCP (plugin Claude Code)

Slash commands + natural language untuk berinteraksi langsung dengan Sentry (self-hosted maupun cloud) dari dalam Claude Code. Menggunakan MCP server `@sentry/mcp-server` yang di-bundle plugin.

## Fitur
- 🗣️ **Natural language** — "apa saja error 1 jam terakhir?"
- 🔧 **Full fix workflow** — detect → analyze stacktrace → fix code → resolve
- 💰 **Token efficient** — output ringkas, default limit rendah
- 🏠 **Self-hosted & cloud**

## Prasyarat
- **Node.js ≥ 20** (untuk `npx @sentry/mcp-server`) — cek: `node -v`
- **Sentry access token** dengan scope: `project:read`, `event:read`, `issue:read`, `issue:write`, `org:read`, `team:read`

## Install
```
/plugin marketplace add https://github.com/febrifahturrohman12/delano-tools
/plugin install sentry@delano-tools
```
Saat plugin di-enable, Claude Code **menanyakan** 4 nilai (via `userConfig`): Sentry Host, Organization Slug, Project Slug, Access Token (token disimpan aman di keychain). MCP server otomatis start dengan konfigurasi itu — **tidak perlu edit `.mcp.json` manual**.

Ganti konfigurasi belakangan: `/plugin` → pilih `sentry` → edit config (atau non-sensitive di `settings.json` → `pluginConfigs`).

## Commands
| Command | Fungsi |
|---|---|
| `/sentry:issues [query]` | List issues (natural language) |
| `/sentry:detail <ID>` | Detail issue + stacktrace |
| `/sentry:fix [ID]` | Workflow: detect → fix → resolve |
| `/sentry:resolve <ID> [action]` | resolve / ignore / reopen |
| `/sentry:events [query]` | Cari events/logs |
| `/sentry:releases [version]` | List releases |
| `/sentry:docs` | Pointer dokumentasi (self-hosted) |
| `/sentry:help` | Bantuan |

## Catatan teknis
- Nama tool MCP ter-scope plugin: `mcp__plugin_sentry_sentry__<tool>` (mis. `list_issues`, `get_issue_details`, `list_events`, `update_issue`, `find_releases`).
- `organizationSlug`/`projectSlugOrId`/`regionUrl` diisi otomatis dari `userConfig` (`${user_config.*}`) di tiap command — tak perlu inject ke `CLAUDE.md`.
- Query reference: `reference.md`.

Dikonversi dari installer npx `febrifahturrohman12/sentry-mcp` ke format plugin marketplace.
