---
description: Mulai tugas dengan plan-gate di awal + pecah jadi todo terurut sebelum eksekusi. Jalankan di AWAL sesi/tugas, sebelum menulis kode.
disable-model-invocation: true
---

# /vibe:plan — Plan-first + decompose (sebelum eksekusi)

Tujuan: menegakkan **rencana dulu, eksekusi kemudian**, dan memecah kerja jadi sub-tugas terurut yang statusnya benar-benar berubah. Ini praktik inti vibe-coding — bukan ritual; rencana harus **membentuk** langkah eksekusi berikutnya.

**Kapan:** di awal sesi/tugas, SEBELUM ada perubahan kode. Kalau kerja sudah terlanjur jalan, tetap berguna tapi dampaknya berkurang — plan-gate paling kuat kalau di depan.

Langkah:
1. **Pahami dulu, jangan langsung ngoding.** Baca konteks seperlunya (`CLAUDE.md`, file yang relevan, `.vibe/HANDOFF.md`). Rujuk temuan dengan `path:line`.
2. **Susun rencana ringkas** yang konkret:
   - Tujuan (1–2 kalimat).
   - Pendekatan + file/komponen yang akan disentuh (sebut path konkret).
   - Trade-off / risiko bila ada.
3. **Plan-gate**: sajikan rencana ke user dan **minta persetujuan sebelum mengeksekusi**. Kalau lingkungan mendukung plan mode, gunakan `ExitPlanMode` agar plan benar-benar jadi gerbang. Jangan menyentuh kode sampai user setuju.
4. **Decompose jadi todo terurut**: setelah disetujui, buat daftar tugas dengan **TodoWrite/TaskCreate** — tiap item = sub-tugas nyata. Selama eksekusi, **ubah statusnya** (in_progress → completed). Todo yang tak pernah berubah status = ritual kosong, hindari.
5. Baru eksekusi (delegasikan penulisan ke `goblin`, pencarian ke `gremlin` bila cocok).

Prinsip: rencana yang di-approve di depan + todo yang benar-benar dipakai = fondasi sesi yang rapi. Jangan over-plan tugas sepele satu langkah.
