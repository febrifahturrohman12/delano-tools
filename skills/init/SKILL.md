---
description: Pasang arsitektur token-hygiene (CLAUDE.md, PROGRESS.md, HANDOFF.md, DECISIONS.md) ke project saat ini. Jalankan sekali per project.
disable-model-invocation: true
---

# /vibe:init — Scaffold arsitektur vibe

Pasang file-file berikut ke root project saat ini, **tanpa menimpa** yang sudah ada.
Template ada di `${CLAUDE_PLUGIN_ROOT}/templates/`.

Langkah:
1. Untuk tiap target berikut, cek apakah sudah ada di project. Kalau **belum ada**, salin dari template. Kalau **sudah ada**, LEWATI dan laporkan (jangan timpa):
   - `CLAUDE.md`     ← `templates/CLAUDE.md.tmpl`
   - `PROGRESS.md`   ← `templates/PROGRESS.md.tmpl`
   - `HANDOFF.md`    ← `templates/HANDOFF.md.tmpl`
   - `DECISIONS.md`  ← `templates/DECISIONS.md.tmpl`
2. Kalau `$ARGUMENTS` berisi nama project, isikan ke judul `CLAUDE.md`. Kalau kosong, tebak dari nama folder.
3. Isi bagian Stack/Perintah `CLAUDE.md` sebisanya dengan mendeteksi project (`package.json`, `composer.json`, `go.mod`, `pyproject.toml`, dll). **Jangan mengarang**; kosongkan kalau tidak yakin.
4. Tampilkan ringkasan: file mana yang dibuat, mana yang dilewati.

Ingatkan user: `CLAUDE.md` harus tetap ramping (< 100 baris). Gunakan `/vibe:slim` untuk audit.
