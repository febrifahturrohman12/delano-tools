---
description: Pasang arsitektur token-hygiene (CLAUDE.md di root + .vibe/ untuk file kerja) ke project saat ini. Jalankan sekali per project.
disable-model-invocation: true
---

# /vibe:init — Scaffold arsitektur vibe

Pasang file berikut ke project saat ini, **tanpa menimpa** yang sudah ada.
Layout: `CLAUDE.md` di **root** (dibaca otomatis tiap pesan), sisanya di folder **`.vibe/`** (file kerja/keputusan).
Template ada di `${CLAUDE_PLUGIN_ROOT}/templates/`.

Langkah:
1. **Deteksi layout lama & migrasi.** Cek apakah ada `HANDOFF.md`, `PROGRESS.md`, atau `DECISIONS.md` **di root** (sisa layout vibe lama). Untuk tiap yang ketemu:
   - Kalau versi `.vibe/<file>` **belum ada** → **pindahkan** ke `.vibe/`. Pakai `git mv <file> .vibe/` bila ini repo git (agar history terjaga), selain itu `mv`.
   - Kalau `.vibe/<file>` **sudah ada** → jangan timpa; laporkan bentrok dan biarkan file root apa adanya untuk user putuskan.
   Laporkan file mana yang dimigrasi.
2. Buat folder `.vibe/` bila belum ada.
4. Untuk tiap target berikut, cek apakah sudah ada. Kalau **belum ada**, salin dari template. Kalau **sudah ada**, LEWATI dan laporkan (jangan timpa):
   - `CLAUDE.md`            ← `templates/CLAUDE.md.tmpl`   (root)
   - `.vibe/PROGRESS.md`    ← `templates/PROGRESS.md.tmpl`
   - `.vibe/HANDOFF.md`     ← `templates/HANDOFF.md.tmpl`
   - `.vibe/DECISIONS.md`   ← `templates/DECISIONS.md.tmpl`
5. Kalau `$ARGUMENTS` berisi nama project, isikan ke judul `CLAUDE.md`. Kalau kosong, tebak dari nama folder. (Hanya berlaku kalau `CLAUDE.md` baru dibuat — jangan sentuh `CLAUDE.md` yang sudah ada.)
6. Isi bagian Stack/Perintah `CLAUDE.md` sebisanya dengan mendeteksi project (`package.json`, `composer.json`, `go.mod`, `pyproject.toml`, dll). **Jangan mengarang**; kosongkan kalau tidak yakin. (Lewati kalau `CLAUDE.md` sudah ada.)
7. **Amankan dua jalur** (agar file kerja tak ke-push ke git & tak ke-bake ke Docker image):
   - `.gitignore` — pastikan ada baris `.vibe/`. Buat file bila belum ada; append bila ada; jangan duplikat.
   - `.dockerignore` — pastikan ada baris `.vibe/` **dan** `CLAUDE.md` (keduanya tak perlu masuk image). Buat/append seperti di atas; jangan duplikat.
   Gunakan blok bertanda, mis:
     ```
     # vibe (token-hygiene)
     .vibe/
     ```
8. **Cek ukuran `CLAUDE.md`.** Kalau `CLAUDE.md` sudah ada dan > ~100 baris (umum di project existing), sarankan user menjalankan `/vibe:slim` untuk merampingkannya — jangan rampingkan otomatis di sini.
9. Tampilkan ringkasan: file mana dimigrasi, dibuat, dilewati, ignore mana ditambahkan, dan apakah `/vibe:slim` disarankan.

Catatan untuk user:
- `.vibe/` di-gitignore secara default (aman: `HANDOFF`/`PROGRESS` personal, `DECISIONS` tak sengaja bocor). Kalau mau **membagikan** `DECISIONS.md` ke repo, tambahkan `!.vibe/DECISIONS.md` di `.gitignore`. Jangan tulis kredensial/IP/detail keamanan di dalamnya.
- Jaga `CLAUDE.md` tetap ramping (< 100 baris). Gunakan `/vibe:slim` untuk audit.
