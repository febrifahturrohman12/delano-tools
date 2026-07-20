# Sentry MCP — Query Reference

**Dashboard**: https://${user_config.sentry_host}/organizations/${user_config.sentry_org}/issues/?project=${user_config.sentry_project}

## Config (dipakai di setiap tool call)
- `organizationSlug`: `${user_config.sentry_org}`
- `projectSlugOrId`: `${user_config.sentry_project}`
- `regionUrl`: `https://${user_config.sentry_host}`

**NEVER use `search_issues`** — selalu pakai `list_issues`.

## Query Syntax

Terjemahkan natural language ke Sentry query:
- "latest errors" → query: `is:unresolved level:error`, sort: `date`
- "warnings today" → query: `is:unresolved level:warning lastSeen:-24h`
- "5 recent issues" → query: `is:unresolved`, sort: `date`, limit: `5`

**Time**: "1 hour" → `-1h`, "24 hours/today" → `-24h`, "1 week" → `-7d`, "1 month" → `-30d`
**Level**: "error" → `level:error`, "warning" → `level:warning`, "fatal/crash" → `level:fatal`

## Tool Params

| Tool | Key Params |
|---|---|
| `list_issues` | query, limit, sort |
| `get_issue_details` | issueId or issueUrl |
| `list_events` | query, dataset, statsPeriod |
| `update_issue` | issueId, status |
| `find_releases` | query |

## Response Language

Selalu balas dalam bahasa yang dipakai user.
