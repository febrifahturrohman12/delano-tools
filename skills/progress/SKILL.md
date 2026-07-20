---
description: Update PROGRESS.md (checklist state pekerjaan) tanpa mengotori context.
disable-model-invocation: true
---

# /vibe:progress — Update state pekerjaan

1. Kalau `PROGRESS.md` belum ada, buat dari `${CLAUDE_PLUGIN_ROOT}/templates/PROGRESS.md.tmpl`.
2. Perbarui checklist berdasarkan yang sudah/belum dikerjakan di sesi ini: pindahkan item selesai ke **Selesai**, tambah item baru ke **Sedang dikerjakan** / **Backlog**, catat **Blocker**.
3. Kalau `$ARGUMENTS` berisi teks, jadikan item baru di **Sedang dikerjakan**.
4. Jaga tetap ringkas — ini state, bukan jurnal.
