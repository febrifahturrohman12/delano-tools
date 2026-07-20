---
description: List Sentry releases + info deployment (opsional filter versi).
allowed-tools: mcp__plugin_sentry_sentry__find_releases
---

Call `find_releases` with `organizationSlug`: "${user_config.sentry_org}", `projectSlug`: "${user_config.sentry_project}", `regionUrl`: "https://${user_config.sentry_host}" + `query`: "$ARGUMENTS" (if provided).

Show releases with version, date, and deployment info.

If no releases found, inform user that release tracking is not configured. Suggest adding `release` option to Sentry SDK init. Docs: https://docs.sentry.io/product/releases/
