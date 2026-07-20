---
description: Cari Sentry events/logs (dataset errors/spans/logs, filter waktu & query).
allowed-tools: mcp__plugin_sentry_sentry__list_events
---

**Parse $ARGUMENTS:**
- "error/warning/fatal" → query filter, Time → statsPeriod
- `--dataset=spans|logs|errors` → dataset (default: `errors`)
- `--period=1h|24h|7d` → statsPeriod (default: `24h`)
- Remaining text → query

Call `list_events` with `organizationSlug`: "${user_config.sentry_org}", `projectSlug`: "${user_config.sentry_project}", `regionUrl`: "https://${user_config.sentry_host}" + `dataset`, `query`, `statsPeriod`, `limit`: 10.

**Output**: compact table. If empty, show a few example queries.
