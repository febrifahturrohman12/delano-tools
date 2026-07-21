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
| `/vibe:plan` | Plan-gate **dialog interaktif** (Setujui/Revisi/Batal); begitu disetujui, langsung mengalir ke todo + delegasi goblin + verifikasi dalam giliran sama (Planning + Decomposition) |
| `/vibe:verify` | **Auto-deteksi** perintah verify dari `CLAUDE.md` "Perintah"/manifest project (npm/composer/cargo/go/make), jalankan yang relevan, tolak perintah destruktif (reset DB). Cukup ketik tanpa argumen (Verifikasi) |
| `/vibe:handoff` | Ringkas sesi ke `HANDOFF.md` sebelum `/clear` — offload+reset, paling hemat token |
| `/vibe:progress` | Update `PROGRESS.md` (checklist state) |
| `/vibe:decide` | Catat satu keputusan arsitektur ke `DECISIONS.md` (ADR ringkas) biar tak diperdebatkan ulang |
| `/vibe:check` | Self-audit jujur sesi terhadap 7 dimensi vibe-coding (praktik, bukan menyiasati penilai) |
| `/vibe:slim` | Audit `CLAUDE.md` dan usulkan pemangkasan (dibaca tiap pesan, wajib ramping) |
| `/vibe:models` | Dialog interaktif: pilih metode akun (**Default** ikut login, atau **CC** proxy dengan input base URL + token) lalu set model leader + subagent goblin/gremlin per-project |

**Agents** (nama sengaja unik biar tak bentrok dengan agent tim lain)
- `goblin` (sonnet) — peran *coder*: menulis/mengubah kode; delegasikan penulisan kode ke sini.
- `gremlin` (haiku) — peran *explorer*: pencarian read-only lintas file; kembalikan kesimpulan, bukan dump file.

Model default ini global (dari plugin). Untuk mengunci model **per-project** (leader + subagent), jalankan `/vibe:models` — menulis ke `.claude/settings.json` dan `.claude/agents/`.

**Hooks**
- `SessionStart` — menyarankan `/vibe:context` bila `HANDOFF.md` ada.
- `PreCompact` — sebelum context di-compact, ingatkan `/vibe:handoff` dulu (offload sadar, bukan ringkasan otomatis).

## Install (via marketplace privat `delano-tools`)

Plugin ini hidup di dalam marketplace **`delano-tools`** (repo privat `febrifahturrohman12/delano-tools`, plugin di subfolder `vibe/`).

1. Di Claude Code:
   ```
   /plugin marketplace add https://github.com/febrifahturrohman12/delano-tools
   /plugin install vibe@delano-tools
   ```
2. Di project mana pun:
   ```
   /vibe:init
   ```

Update plugin: push perubahan ke repo, lalu `/plugin marketplace update delano-tools` + `/plugin update vibe@delano-tools`.

### Test lokal tanpa install
```bash
claude --plugin-dir /path/ke/delano-tools/vibe
```
Setelah ubah file, jalankan `/reload-plugins`.

## Cara pakai (langkah demi langkah)

Baru pertama coba? Ikuti urutan ini. Ada dua fase: **sekali per project** (setup) lalu **tiap sesi kerja** (siklus).

### 1. Sekali per project (setup)

Jalankan **di root project yang mau digarap** (bukan folder home):

```
/vibe:init      # scaffold CLAUDE.md + folder .vibe/ (HANDOFF/PROGRESS/DECISIONS), auto-ignore
/vibe:models    # opsional: kunci model leader + goblin/gremlin per-project
```

### 2. Tiap sesi kerja (siklus)

Urutannya sengaja — tiap langkah menutup satu dimensi vibe-coding:

| # | Langkah | Command / aksi | Kapan |
|---|---|---|---|
| 1 | Pemanasan | `/vibe:context` | Awal sesi (mis. setelah `/clear`) |
| 2 | Rencana → eksekusi | `/vibe:plan <tugas + konteks>` → dialog **"Setujui"** → **otomatis** lanjut ke todo + delegasi `goblin`/`gremlin` + verifikasi (tanpa ketik ulang spec) | **Sebelum** ngoding; approval memicu eksekusi |
| 3 | Buktikan | `/vibe:verify` (auto-deteksi perintah project) | Kalau belum ke-cover langkah 2 |
| 4 | Catat | `/vibe:decide` / `/vibe:progress` | Ada keputusan / kemajuan |
| 5 | Audit | `/vibe:check` | **Sebelum** tutup / sebelum grading |
| 6 | Tutup | `/vibe:handoff` → `/clear` | Context penuh / ganti topik |

Sesi berikutnya balik ke langkah 1 (`/vibe:context`) untuk pemanasan dari `HANDOFF.md`.

> **v0.4.0:** plan-gate kini dialog interaktif yang langsung mengalir ke eksekusi — tak perlu mengirim ulang spec sebagai pesan terpisah (menghemat token).

### 3. Kebiasaan biar efeknya nyata

1. Jaga `CLAUDE.md` **ramping** (< 100 baris); cek berkala dengan `/vibe:slim`.
2. **Delegasi beneran** — jangan tulis kode di leader; lempar ke `goblin`. Butuh cari file? lempar ke `gremlin`. Context mereka terpisah = firewall context = hemat token.
3. Rujuk file dengan `path:line`, **jangan tempel isi file panjang** ke prompt.
4. Offload sadar: `/vibe:handoff` **sebelum** `/clear`, bukan mengandalkan ringkasan otomatis.

> Prinsip (lihat [`RUBRIC.md`](RUBRIC.md)): **perbaiki praktiknya, skor mengikuti sendiri.** Vibe tidak pernah menyiasati penilai.

## Selaras 7 dimensi vibe-coding

Vibe bukan cuma soal token (itu 1 dari 7 dimensi). Command-nya dipetakan ke praktik vibe-coding berkualitas: **Planning** (`/vibe:plan`), **Context** (`/vibe:context`), **Decomposition** (`/vibe:plan`), **Delegasi** (`goblin`/`gremlin`), **Verifikasi** (`/vibe:verify`), **Efisiensi Token** (`/vibe:handoff`+`/clear`, `/vibe:slim`), **Dokumentasi** (`/vibe:decide`, `/vibe:handoff`). Peta lengkap + catatan integritas ada di [`RUBRIC.md`](RUBRIC.md). Prinsip: **perbaiki praktiknya, skor mengikuti** — vibe tak pernah menyiasati penilai.

## Catatan

- Model `goblin`/`gremlin` bisa diubah di `agents/*.md` sesuai kebutuhan tiap akun/plan (atau per-project via `/vibe:models`).
- Definisi agent di project (`.claude/agents/`) dengan nama sama akan menimpa versi plugin.
