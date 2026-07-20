---
description: Muat ulang konteks project secara ringkas untuk melanjutkan kerja setelah /clear atau di sesi baru. Baca file vibe, sajikan briefing tipis — bukan dump isi file.
disable-model-invocation: true
---

# /vibe:context — Prime konteks sesi (hemat token)

Kebalikan dari `/vibe:handoff`. Tujuan: **muat konteks secukupnya** untuk lanjut kerja tanpa membaca ulang seluruh riwayat atau menempel isi file panjang ke context.

Langkah:
1. Cek keberadaan file berikut di project (jangan error kalau tidak ada, cukup lewati):
   - `.vibe/HANDOFF.md`   — status & langkah berikutnya sesi sebelumnya (**prioritas utama**)
   - `.vibe/PROGRESS.md`  — checklist state pekerjaan
   - `.vibe/DECISIONS.md` — keputusan arsitektur yang sudah diambil
   - `CLAUDE.md`          — konvensi & perintah di root (biasanya sudah ikut context, cukup rujuk)
2. Baca file yang ada, lalu susun **briefing ringkas** (target < 20 baris):
   - **Tugas berjalan** — 1-2 kalimat dari HANDOFF.
   - **Langkah berikutnya** — item konkret paling atas.
   - **Blocker / catatan** — hal yang tak terlihat dari kode.
   - **File relevan** — sebut `path:line`, jangan tempel isinya.
3. Kalau `$ARGUMENTS` berisi topik/fokus, saring briefing ke topik itu saja.
4. Kalau folder `.vibe/` / file vibe tak ada sama sekali, beri tahu user dan sarankan `/vibe:init` dulu.

Jangan menyalin isi file mentah-mentah ke jawaban — rangkum. Setelah briefing, tunggu instruksi user; jangan langsung mengeksekusi pekerjaan.
