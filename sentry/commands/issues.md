---
description: List Sentry issues (mendukung natural language & filter level/waktu/limit).
allowed-tools: mcp__plugin_sentry_sentry__list_issues
---

**Parse $ARGUMENTS:**
- Number → limit (default: 5)
- "error/warning/fatal" → `level:X`
- Time ("1 hour" → `lastSeen:-1h`, "24h/today" → `lastSeen:-24h`, "week" → `lastSeen:-7d`)
- Sentry query format → use directly
- Empty → query: `is:unresolved`, limit: 5

Call `list_issues` with `organizationSlug`: "${user_config.sentry_org}", `projectSlugOrId`: "${user_config.sentry_project}", `regionUrl`: "https://${user_config.sentry_host}" + `query`, `sort`: "date", `limit`.

**Output**: compact table — Issue ID, Title, Level, Events, Last Seen. Then offer detail or fix.
