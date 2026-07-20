---
description: Tampilkan detail satu Sentry issue + stacktrace (app frames) dari ID/URL.
allowed-tools: mcp__plugin_sentry_sentry__get_issue_details, Read
---

**Parse $ARGUMENTS:**
- URL → use as `issueUrl`
- Issue ID (PROJECT-123) → use as `issueId` + `organizationSlug`: "${user_config.sentry_org}"
- Empty → ask user for Issue ID

Call `get_issue_details` with `regionUrl`: "https://${user_config.sentry_host}".

**Output** (compact):
1. **Summary**: title, status, level, events count, first/last seen
2. **Stacktrace**: app code frames only (skip vendor/library), show file:line + snippet
3. **Link**: Sentry dashboard URL

If stacktrace points to a file in this project, offer to open and help fix it.
