---
description: Catat satu keputusan arsitektur ke DECISIONS.md sebagai ADR ringkas, agar tak diperdebatkan ulang tiap sesi. Jalankan begitu sebuah keputusan diambil.
disable-model-invocation: true
---

# /vibe:decide — Catat keputusan (ADR ringkas)

Keputusan yang tercatat = tidak perlu dijelaskan ulang tiap sesi, dan bisa ditarik `/vibe:context`. Ini menghemat token sekaligus mencegah bolak-balik memperdebatkan hal yang sudah diputus.

Langkah:
1. Kalau `.vibe/DECISIONS.md` belum ada, buat dari `${CLAUDE_PLUGIN_ROOT}/templates/DECISIONS.md.tmpl` (buat folder `.vibe/` bila perlu).
2. Tentukan isi keputusan:
   - Kalau `$ARGUMENTS` berisi teks, jadikan itu inti keputusan.
   - Kalau kosong, ambil dari keputusan yang baru saja disepakati di sesi berjalan. Kalau belum jelas, **tanya** singkat ke user sebelum menulis.
3. Tambahkan **entri baru di atas** (paling baru dulu), format ADR ringkas:
   ```
   ## <tanggal hari ini> — <judul keputusan>
   - **Konteks:** kenapa ini muncul (1 kalimat)
   - **Keputusan:** apa yang dipilih
   - **Alasan:** kenapa
   - **Alternatif ditolak:** apa + kenapa tidak (kalau ada)
   ```
4. Jaga ringkas — maksimal beberapa baris per bagian. Ini catatan keputusan, bukan esai.
5. **Jangan timpa** entri lama; hanya menambah. Laporkan judul entri yang ditambahkan.

Keamanan: `DECISIONS.md` bisa ikut ke repo/registry. Tulis **keputusan & alasan** saja — jangan kredensial, IP/hostname, atau detail keamanan yang eksploitabel. Perlakukan seperti komentar kode yang di-push.
