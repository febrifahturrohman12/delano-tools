---
description: Set model per-project untuk leader (sesi) dan subagent coder/explorer. Jalankan sekali per project saat ingin mengunci model.
disable-model-invocation: true
---

# /vibe:models — Set model per-project (leader + subagent)

Mengunci model untuk project saat ini di folder `.claude/`, terpisah dari plugin global. Berguna karena tiap akun/plan punya kuota berbeda.

Default (kalau `$ARGUMENTS` kosong):
- **leader** → `claude-opus-4-8`
- **coder** → `claude-sonnet-5`
- **explorer** → `claude-haiku-4-5-20251001`

Override via `$ARGUMENTS`, format `peran=model`, contoh:
`/vibe:models leader=sonnet coder=opus explorer=haiku`

Alias yang dikenali (petakan ke ID lengkap):
- `opus` → `claude-opus-4-8`
- `sonnet` → `claude-sonnet-5`
- `haiku` → `claude-haiku-4-5-20251001`
- `fable` → `claude-fable-5`
- `inherit` → `inherit` (ikut default global, tak dikunci)
- ID lengkap (mis. `claude-opus-4-8`) diterima apa adanya.

Langkah:
1. Buat folder `.claude/` (dan `.claude/agents/`) bila belum ada.
2. **Leader** — set model di `.claude/settings.json`:
   - Kalau file belum ada → buat `{ "model": "<leader>" }`.
   - Kalau sudah ada → tamb/ubah **hanya** key `"model"`, **pertahankan** key lain (mis. `enabledPlugins`). Jangan menimpa seluruh file.
   - Kalau leader = `inherit` → jangan tulis key `model` (atau hapus bila ada), biar ikut global.
3. **coder & explorer** — buat override per-project dengan **menyalin** definisi dari plugin lalu mengganti baris `model:`:
   - Salin `${CLAUDE_PLUGIN_ROOT}/agents/coder.md` → `.claude/agents/coder.md`, ganti frontmatter `model:` jadi `<coder>`.
   - Salin `${CLAUDE_PLUGIN_ROOT}/agents/explorer.md` → `.claude/agents/explorer.md`, ganti `model:` jadi `<explorer>`.
   - Ini menyalin isi terbaru dari plugin (DRY) — hanya model yang berbeda. Kalau peran = `inherit`, set `model: inherit`.
4. Tampilkan ringkasan: model tiap peran + path file yang ditulis.

Ingatkan user:
- Perubahan model **leader** butuh **restart sesi** di project itu agar berlaku (atau ganti manual via `/model`). Model subagent langsung berlaku pada delegasi berikutnya.
- Kalau `.claude/` masuk `.gitignore` project (umum), setting ini **personal/lokal** — tak ikut ke repo/tim.
