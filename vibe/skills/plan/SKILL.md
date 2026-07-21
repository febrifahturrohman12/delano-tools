---
description: Mulai tugas dengan plan-gate di awal + pecah jadi todo terurut sebelum eksekusi. Jalankan di AWAL sesi/tugas, sebelum menulis kode.
disable-model-invocation: true
---

# /vibe:plan — Plan-first + decompose (sebelum eksekusi)

Tujuan: menegakkan **rencana dulu, eksekusi kemudian**, dan memecah kerja jadi sub-tugas terurut yang statusnya benar-benar berubah. Ini praktik inti vibe-coding — bukan ritual; rencana harus **membentuk** langkah eksekusi berikutnya.

**Kapan:** di awal sesi/tugas, SEBELUM ada perubahan kode. Kalau kerja sudah terlanjur jalan, tetap berguna tapi dampaknya berkurang — plan-gate paling kuat kalau di depan.

**Wajib ada deskripsi tugas.** Idealnya dipanggil `/vibe:plan <tugas + konteks konkret>` sekali jalan. Kalau `$ARGUMENTS` **kosong**, JANGAN membuka putaran plan kosong (boros token) — minta user memberikan tujuan + file/constraint terkait dalam satu pesan dulu, baru lanjut ke langkah di bawah. Jangan panggil ulang skill ini tanpa argumen.

Langkah:
1. **Pahami dulu, jangan langsung ngoding.** Baca konteks seperlunya (`CLAUDE.md`, file yang relevan, `.vibe/HANDOFF.md`). Rujuk temuan dengan `path:line`.
2. **Susun rencana ringkas** yang konkret:
   - Tujuan (1–2 kalimat).
   - Pendekatan + file/komponen yang akan disentuh (sebut path konkret).
   - Trade-off / risiko bila ada.
3. **Plan-gate (dialog interaktif)**: sajikan rencana, lalu minta keputusan lewat **AskUserQuestion** dengan opsi:
   - **"Setujui — lanjut delegasi & eksekusi"**
   - **"Revisi rencana"** (user beri koreksi → perbarui rencana → tanya lagi)
   - **"Batal"**
   (Kalau lingkungan mendukung plan mode, `ExitPlanMode` juga sah sebagai gerbang.) Jangan menyentuh kode sampai user memilih **Setujui**.
   **Begitu user memilih Setujui, LANGSUNG lanjut ke langkah 4–5 dalam giliran yang sama** — jangan menunggu, jangan minta user mengetik ulang spec/instruksi eksekusi. Spec sudah ada di rencana; mengulangnya = putaran mubazir (boros token).
4. **Decompose jadi todo terurut (WAJIB untuk tugas berlangkah)**: begitu disetujui, langsung buat **TodoWrite/TaskCreate** berisi sub-tugas nyata & terurut. Aturan pakai: tandai **satu** item `in_progress` sebelum mengerjakannya, lalu `completed` tepat setelah selesai — perbarui **real-time**, bukan sekaligus di akhir. Todo yang statusnya tak pernah berubah = ritual kosong (nol nilai). **Kecuali** tugas benar-benar satu langkah sepele → lewati todo; jangan mengarang sub-tugas palsu (itu gaming, penilai melihatnya).
5. Eksekusi (mengalir langsung dari langkah 4, tanpa giliran user tambahan). **Default: delegasikan penulisan/perubahan kode ke `goblin` via Agent tool, pencarian read-only lintas file ke `gremlin`** — jangan tulis kode sendiri kecuali edit satu-baris sepele. Beri subagent spesifikasi konkret (file, requirement, batasan) **dari rencana yang sudah disetujui** (jangan minta user mengetiknya ulang), tunggu laporannya, lalu verifikasi & integrasikan. Delegasi yang benar-benar terjadi (bukan sekadar niat) = dimensi Delegasi terpenuhi.

Prinsip: rencana yang di-approve di depan + todo yang benar-benar dipakai = fondasi sesi yang rapi. Jangan over-plan tugas sepele satu langkah.
