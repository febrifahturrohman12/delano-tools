---
description: Audit CLAUDE.md dan usulkan pemangkasan. CLAUDE.md dibaca tiap pesan, jadi wajib ramping.
disable-model-invocation: true
---

# /vibe:slim — Rampingkan CLAUDE.md

`CLAUDE.md` ikut context di **SETIAP** pesan sepanjang sesi. Baris berlebih = pajak token terus-menerus.

Langkah:
1. Baca `CLAUDE.md` project. Hitung jumlah baris & perkiraan kasar token (≈ jumlah kata × 1.3).
2. Tandai bagian yang sebaiknya **DIBUANG** karena bisa ditemukan lagi saat perlu:
   - Struktur / pohon folder
   - Penjelasan cara kerja kode
   - Sejarah / changelog
   - Daftar file yang panjang
   - Info yang sudah jelas dari kode
3. **Pertahankan hanya**: konvensi wajib, perintah build/test/run, dan gotcha yang tak terlihat dari kode.
4. Tampilkan versi ramping usulan (target < 100 baris) dan **tanyakan** apakah mau diterapkan sebelum menimpa.
