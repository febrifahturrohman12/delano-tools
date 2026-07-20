---
description: Tulis ringkasan sesi ke HANDOFF.md agar bisa /clear lalu lanjut dengan context tipis. Jalankan saat context mulai penuh atau ganti topik.
disable-model-invocation: true
---

# /vibe:handoff — Offload konteks sebelum /clear

Tujuan: menyimpan cukup konteks ke `.vibe/HANDOFF.md` supaya sesi berikutnya bisa lanjut TANPA membaca ulang seluruh riwayat. Ini teknik hemat token paling berdampak.

Langkah:
1. Kalau `.vibe/HANDOFF.md` belum ada, buat dari `${CLAUDE_PLUGIN_ROOT}/templates/HANDOFF.md.tmpl` (buat folder `.vibe/` bila perlu). Kalau `.vibe/` belum ada sama sekali, sarankan `/vibe:init` dulu.
2. Isi/timpa isinya berdasarkan sesi berjalan:
   - **Tujuan tugas** — 1-2 kalimat.
   - **Sudah dikerjakan** — poin-poin ringkas.
   - **File tersentuh** — `path` + alasan singkat.
   - **Langkah berikutnya** — urutan konkret.
   - **Catatan penting / jebakan** — apa yang tak terlihat dari kode.
   - Tanggal update.
3. Ringkas — jangan salin dialog. Rujuk file dengan `path:line`, jangan tempel isi file.
4. Kalau `$ARGUMENTS` mengandung `progress`, update juga `.vibe/PROGRESS.md`.
5. Setelah menulis, sarankan user menjalankan `/clear` lalu memulai sesi baru dengan `/vibe:context`.
