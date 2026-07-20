# vibe — token-hygiene toolkit untuk Claude Code

Plugin untuk memaksimalkan "vibe coding" dengan Claude Code sambil **menghemat token**. Dipasang sekali, dipakai di project mana pun.

Idenya: token termahal adalah context yang dibaca ulang tiap giliran. Plugin ini menyediakan arsitektur file + workflow untuk menjaga context tetap tipis.

## Layout file per-project

`/vibe:init` menaruh `CLAUDE.md` di root (dibaca otomatis tiap pesan) dan file kerja di folder `.vibe/`:

```
project/
├── CLAUDE.md            # committed, kebaca otomatis, jaga ramping
└── .vibe/               # gitignore + dockerignore otomatis
    ├── HANDOFF.md       # status sesi (personal)
    ├── PROGRESS.md      # checklist kerja (personal)
    └── DECISIONS.md     # ADR ringkas (un-ignore kalau mau di-share)
```

`/vibe:init` otomatis menambah `.vibe/` ke **`.gitignore`** (tak ke-push) dan `.vibe/` + `CLAUDE.md` ke **`.dockerignore`** (tak ke-bake ke image). Mau membagikan keputusan? Tambah `!.vibe/DECISIONS.md` di `.gitignore` — tapi jangan isi kredensial/IP/detail keamanan.

## Isi

**Skills (command)**
| Command | Fungsi |
| --- | --- |
| `/vibe:init` | Scaffold `CLAUDE.md`, `PROGRESS.md`, `HANDOFF.md`, `DECISIONS.md` ke project (tanpa menimpa yang sudah ada) |
| `/vibe:context` | Muat ulang konteks (`HANDOFF`/`PROGRESS`/`DECISIONS`) jadi briefing tipis — pemanasan sesi baru setelah `/clear` |
| `/vibe:plan` | Plan-gate di awal + pecah jadi todo terurut sebelum eksekusi (Planning + Decomposition) |
| `/vibe:verify` | Jalankan test/build/run, periksa hasil, tindak lanjuti kegagalan (Verifikasi) |
| `/vibe:handoff` | Ringkas sesi ke `HANDOFF.md` sebelum `/clear` — offload+reset, paling hemat token |
| `/vibe:progress` | Update `PROGRESS.md` (checklist state) |
| `/vibe:decide` | Catat satu keputusan arsitektur ke `DECISIONS.md` (ADR ringkas) biar tak diperdebatkan ulang |
| `/vibe:check` | Self-audit jujur sesi terhadap 7 dimensi vibe-coding (praktik, bukan menyiasati penilai) |
| `/vibe:slim` | Audit `CLAUDE.md` dan usulkan pemangkasan (dibaca tiap pesan, wajib ramping) |
| `/vibe:models` | Set model per-project: leader (`.claude/settings.json`) + subagent goblin/gremlin (`.claude/agents/`) |

**Agents** (nama sengaja unik biar tak bentrok dengan agent tim lain)
- `goblin` (sonnet) — peran *coder*: menulis/mengubah kode; delegasikan penulisan kode ke sini.
- `gremlin` (haiku) — peran *explorer*: pencarian read-only lintas file; kembalikan kesimpulan, bukan dump file.

Model default ini global (dari plugin). Untuk mengunci model **per-project** (leader + subagent), jalankan `/vibe:models` — menulis ke `.claude/settings.json` dan `.claude/agents/`.

**Hooks**
- `SessionStart` — menyarankan `/vibe:context` bila `HANDOFF.md` ada.
- `PreCompact` — sebelum context di-compact, ingatkan `/vibe:handoff` dulu (offload sadar, bukan ringkasan otomatis).

## Install (via marketplace privat)

1. Push folder ini ke git repo **privat** kamu:
   ```bash
   git remote add origin <url-repo-privat>
   git push -u origin main
   ```
2. Di Claude Code:
   ```
   /plugin marketplace add <url-repo-privat>
   /plugin install vibe@vibe-marketplace
   ```
3. Di project mana pun:
   ```
   /vibe:init
   ```

Update plugin: push perubahan ke repo, lalu `/plugin marketplace update` di Claude Code.

### Test lokal tanpa install
```bash
claude --plugin-dir /path/ke/vibe-plugin
```
Setelah ubah file, jalankan `/reload-plugins`.

## Workflow hemat token (ringkas)

1. `/vibe:init` sekali per project → arsitektur file terpasang.
2. Jaga `CLAUDE.md` ramping (< 100 baris); cek berkala dengan `/vibe:slim`.
3. Delegasikan pencarian ke `gremlin` dan penulisan kode ke `goblin` (context mereka terpisah = firewall context).
4. Saat context mulai penuh / ganti topik: `/vibe:handoff` → `/clear` → sesi baru `/vibe:context` untuk pemanasan.
5. Rujuk file dengan `path:line`, jangan tempel isi file panjang.

## Selaras 7 dimensi vibe-coding

Vibe bukan cuma soal token (itu 1 dari 7 dimensi). Command-nya dipetakan ke praktik vibe-coding berkualitas: **Planning** (`/vibe:plan`), **Context** (`/vibe:context`), **Decomposition** (`/vibe:plan`), **Delegasi** (`goblin`/`gremlin`), **Verifikasi** (`/vibe:verify`), **Efisiensi Token** (`/vibe:handoff`+`/clear`, `/vibe:slim`), **Dokumentasi** (`/vibe:decide`, `/vibe:handoff`). Peta lengkap + catatan integritas ada di [`RUBRIC.md`](RUBRIC.md). Prinsip: **perbaiki praktiknya, skor mengikuti** — vibe tak pernah menyiasati penilai.

## Catatan

- Model `goblin`/`gremlin` bisa diubah di `agents/*.md` sesuai kebutuhan tiap akun/plan (atau per-project via `/vibe:models`).
- Definisi agent di project (`.claude/agents/`) dengan nama sama akan menimpa versi plugin.
