---
description: Set akun & model per-project (leader + subagent goblin/gremlin) lewat dialog interaktif. Jalankan sekali per project saat ingin mengunci akun/model.
disable-model-invocation: true
---

# /vibe:models — Set akun & model per-project (dialog interaktif)

Mengunci **metode akun** + **model** untuk project saat ini di folder `.claude/`, terpisah dari plugin global. Berguna karena tiap akun/plan/proxy punya kuota & penamaan model berbeda.

Jalankan **interaktif**: tanya via AskUserQuestion lalu tulis file. Kalau `$ARGUMENTS` berisi override eksplisit (`peran=model`, lihat alias di bawah), pakai itu dan **lewati dialog** (mode cepat untuk power-user).

## Alur dialog

### 1. Tanya metode akun
Pakai AskUserQuestion (header "Metode akun", satu pilihan):
- **Default** — ikut akun yang sedang login (mis. OAuth/personal). Model pakai nama polos.
- **CC** — akun proxy: input Base URL + Auth token, model pakai prefix `cc/`.

### 2. Kalau Default
- Model tetap (otomatis, tanpa nanya lagi):
  - leader → `claude-opus-4-8`
  - goblin (coder) → `claude-sonnet-5`
  - gremlin (explorer) → `claude-haiku-4-5-20251001`
- **Leader**: set `"model"` di `.claude/settings.json` (buat bila belum ada; kalau ada, ubah **hanya** key `model`, pertahankan key lain seperti `enabledPlugins` — jangan timpa seluruh file).
- **JANGAN** tulis `env`/token — biar ikut akun yang login.
- Lanjut ke langkah 4 (tulis agent).

### 3. Kalau CC
a. **Minta Base URL + Auth token** — minta user mengetikkannya (token bersifat rahasia). Kalau user tak memberikan keduanya, hentikan dan jelaskan bahwa mode CC butuh keduanya.
b. **Tanya varian model leader** via AskUserQuestion (header "Model leader"):
   - `cc/claude-opus-4-8[1m]` — context 1M (Recommended)
   - `cc/claude-opus-4-8` — tanpa 1M
c. goblin/gremlin otomatis (tanpa nanya): goblin → `cc/claude-sonnet-5`, gremlin → `cc/claude-haiku-4-5-20251001`.
d. Tulis ke **`.claude/settings.local.json`** (pertahankan key lain yang sudah ada seperti `enabledPlugins`, `enabledMcpjsonServers`; ubah/isi hanya `env` + `model`):
   ```json
   {
     "env": {
       "ANTHROPIC_BASE_URL": "<base url dari user>",
       "ANTHROPIC_AUTH_TOKEN": "<token dari user>",
       "ANTHROPIC_DEFAULT_OPUS_MODEL": "cc/claude-opus-4-8",
       "ANTHROPIC_DEFAULT_SONNET_MODEL": "cc/claude-sonnet-5",
       "ANTHROPIC_DEFAULT_HAIKU_MODEL": "cc/claude-haiku-4-5-20251001",
       "ANTHROPIC_DEFAULT_SUBAGENT_MODEL": "cc/claude-sonnet-5",
       "CLAUDE_CODE_SUBAGENT_MODEL": "cc/claude-sonnet-5"
     },
     "model": "<varian leader pilihan user>"
   }
   ```
   Lima env `*_MODEL` itu me-remap alias `opus/sonnet/haiku` → model `cc/…`, jadi subagent yang pakai alias polos pun ikut benar.
e. **Wajib gitignore**: `.claude/settings.local.json` berisi token. Kalau project adalah git repo dan file itu belum di-ignore, tambahkan baris `.claude/settings.local.json` ke `.gitignore`. Jangan pernah biarkan token ke-commit.

### 4. Tulis agent goblin & gremlin (kedua metode)
Buat override per-project dengan **menyalin** definisi dari plugin lalu mengganti baris `model:`:
- Salin `${CLAUDE_PLUGIN_ROOT}/agents/goblin.md` → `.claude/agents/goblin.md`, ganti frontmatter `model:` jadi model goblin (Default: `claude-sonnet-5`; CC: `cc/claude-sonnet-5`).
- Salin `${CLAUDE_PLUGIN_ROOT}/agents/gremlin.md` → `.claude/agents/gremlin.md`, ganti `model:` jadi model gremlin (Default: `claude-haiku-4-5-20251001`; CC: `cc/claude-haiku-4-5-20251001`).
- Ini menyalin isi terbaru dari plugin (DRY) — hanya model yang berbeda.

### 5. Ringkasan
Tampilkan: metode akun terpilih, model tiap peran, dan path tiap file yang ditulis. Ingatkan user:
- Perubahan model **leader** & **env** butuh **restart sesi** di project itu agar berlaku (env & model leader dibaca saat startup). Model subagent langsung berlaku pada delegasi berikutnya.
- Kalau `.claude/` masuk `.gitignore` project, setting ini **personal/lokal** — tak ikut ke repo/tim.

## Mode cepat via `$ARGUMENTS` (opsional, lewati dialog)
Format `peran=model`, contoh: `/vibe:models leader=sonnet goblin=opus gremlin=haiku`.
Alias yang dikenali (petakan ke ID lengkap):
- `opus` → `claude-opus-4-8`
- `sonnet` → `claude-sonnet-5`
- `haiku` → `claude-haiku-4-5-20251001`
- `fable` → `claude-fable-5`
- `inherit` → `inherit` (ikut default global, tak dikunci — untuk leader berarti hapus key `model`)
- ID lengkap (mis. `cc/claude-sonnet-5`, `claude-opus-4-8`) diterima apa adanya.
- Alias peran `coder`/`explorer` diterima (coder→goblin, explorer→gremlin).

Mode cepat tidak menyentuh `env`/token — hanya model. Untuk setup akun CC (base URL + token) gunakan dialog.
