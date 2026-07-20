# vibe — token-hygiene toolkit untuk Claude Code

Plugin untuk memaksimalkan "vibe coding" dengan Claude Code sambil **menghemat token**. Dipasang sekali, dipakai di project mana pun.

Idenya: token termahal adalah context yang dibaca ulang tiap giliran. Plugin ini menyediakan arsitektur file + workflow untuk menjaga context tetap tipis.

## Isi

**Skills (command)**
| Command | Fungsi |
| --- | --- |
| `/vibe:init` | Scaffold `CLAUDE.md`, `PROGRESS.md`, `HANDOFF.md`, `DECISIONS.md` ke project (tanpa menimpa yang sudah ada) |
| `/vibe:handoff` | Ringkas sesi ke `HANDOFF.md` sebelum `/clear` — offload+reset, paling hemat token |
| `/vibe:progress` | Update `PROGRESS.md` (checklist state) |
| `/vibe:slim` | Audit `CLAUDE.md` dan usulkan pemangkasan (dibaca tiap pesan, wajib ramping) |

**Agents**
- `coder` (sonnet) — menulis/mengubah kode; delegasikan penulisan kode ke sini.
- `explorer` (haiku) — pencarian read-only lintas file; kembalikan kesimpulan, bukan dump file.

**Hooks**
- `SessionStart` — mengingatkan membaca `HANDOFF.md` bila ada.

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
3. Delegasikan pencarian ke `explorer` dan penulisan kode ke `coder` (context mereka terpisah = firewall context).
4. Saat context mulai penuh / ganti topik: `/vibe:handoff` → `/clear` → sesi baru baca `HANDOFF.md`.
5. Rujuk file dengan `path:line`, jangan tempel isi file panjang.

## Catatan

- Model `coder`/`explorer` bisa diubah di `agents/*.md` sesuai kebutuhan tiap akun/plan.
- Definisi agent di project (`.claude/agents/`) dengan nama sama akan menimpa versi plugin.
