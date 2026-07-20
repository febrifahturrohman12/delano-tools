# delano-tools — marketplace plugin Claude Code

Marketplace privat berisi plugin Claude Code buatan sendiri. Pasang lewat Claude Code:

```
/plugin marketplace add https://github.com/febrifahturrohman12/delano-tools
/plugin install <plugin>@delano-tools
```

## Plugin

| Plugin | Folder | Fungsi |
| --- | --- | --- |
| **vibe** | [`vibe/`](vibe/) | Token-hygiene + vibe-coding toolkit, selaras 7 dimensi vibe-coding. Baru coba? Lihat [**Cara pakai (langkah demi langkah)**](vibe/README.md#cara-pakai-langkah-demi-langkah). |
| **sentry** | [`sentry/`](sentry/) | Sentry error-tracking via MCP: `/sentry:*` commands + natural language. Lihat [`sentry/README.md`](sentry/README.md). |

## Struktur

```
.claude-plugin/marketplace.json   # katalog marketplace "delano-tools"
vibe/                             # plugin vibe   (punya .claude-plugin/plugin.json sendiri)
sentry/                           # plugin sentry (MCP server + /sentry:* commands)
```

Menambah plugin baru: buat folder plugin baru di root, tambahkan entri di `.claude-plugin/marketplace.json` (`name`, `source`, `description`).

## Update

```
/plugin marketplace update delano-tools
/plugin update <plugin>@delano-tools
```
