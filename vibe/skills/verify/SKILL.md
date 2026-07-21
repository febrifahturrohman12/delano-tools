---
description: Verifikasi perubahan dengan menjalankan test/build/run yang relevan dan menindaklanjuti kegagalan. Jalankan setelah membuat perubahan, sebelum menganggap selesai.
disable-model-invocation: true
---

# /vibe:verify — Buktikan perubahan benar-benar jalan

Tujuan: menutup tugas dengan **bukti**, bukan asumsi. Cukup diketik `/vibe:verify` **tanpa argumen** — skill ini menentukan sendiri cara verify project ini, menjalankannya, memeriksa hasil, dan menindaklanjuti bila gagal.

> Kalau project punya skill `/verify` bawaan yang lebih lengkap (menggerakkan flow end-to-end), pakai itu. Skill ini checklist ringan + auto-deteksi perintah, supaya user tak perlu mengetik prompt verify tiap kali.

## 1. Tentukan perintah verify SENDIRI (jangan tanya user dulu)
Cari sumber perintah, urut prioritas — berhenti di yang pertama ketemu:

1. **`CLAUDE.md` bagian "Perintah"** (Test/Build/Lint/Run) — sumber utama. `/vibe:init` mengisinya; ini "memori" perintah project agar tak diketik ulang.
2. **File manifest project** bila CLAUDE.md kosong/tak ada — deteksi dari stack:

   | Stack (file penanda) | Test | Build/Compile | Lint/Format |
   |---|---|---|---|
   | Node (`package.json`) | baca `scripts.test` → `npm test` | `scripts.build` → `npm run build` | `scripts.lint` |
   | PHP (`composer.json`) | `scripts.test` atau `vendor/bin/phpunit` | — | `vendor/bin/php-cs-fixer fix --dry-run` |
   | Python (`pyproject.toml`/`pytest.ini`) | `pytest` / `python -m pytest` | — | `ruff check` / `flake8`, `mypy` |
   | Rust (`Cargo.toml`) | `cargo test` | `cargo build` | `cargo clippy` |
   | Go (`go.mod`) | `go test ./...` | `go build ./...` | `go vet ./...` |
   | Make (`Makefile`) | `make test` | `make build` | `make lint` |

3. **Baru tanya user** (sekali) kalau tetap tak terdeteksi — lalu sarankan menambahkannya ke `CLAUDE.md` "Perintah" agar lain kali otomatis.

## 2. Pilih yang RELEVAN, bukan jalankan semua
- Pilih verifikasi yang menyentuh apa yang berubah: test unit/feature terkait, atau build, atau jalankan app & latih alur yang berubah.
- Perubahan yang cuma dok/komentar tak perlu di-drive.
- Untuk endpoint/handler tanpa test: **smoke-test runtime** sah (mis. jalankan server lokal + `curl`).

## 3. Lapisan AMAN — jangan rusak apa pun
- **Jangan jalankan perintah destruktif** tanpa konfirmasi: yang me-reset/drop/seed database, `migrate:fresh`, hapus data, atau memanggil layanan berbayar/produksi.
- Kalau suite test tampak menyentuh **DB sungguhan tanpa isolasi** (mis. ada `ResetDatabase`, tak ada config DB test terpisah), **jangan jalankan** — pilih verifikasi lebih aman (lint + build + run bertarget) atau tanya user apakah ada DB test terisolasi. Catat jebakan ini ke `CLAUDE.md` "Gotcha".

## 4. Periksa & tindak lanjuti
- **Baca `tool_result`-nya** — jangan anggap lulus tanpa membaca output. Sebutkan hasil apa adanya (lulus/gagal + angka).
- **Kalau gagal → perbaiki, lalu ulang** sampai hijau atau blocker jelas. Kegagalan dibiarkan = verifikasi setengah.
- Laporkan ringkas: perintah apa dijalankan, hasilnya, tindakan bila ada.

Jujur soal hasil: kalau test gagal, katakan gagal dengan output-nya; kalau ada langkah dilewati, sebutkan. Jangan klaim "selesai" tanpa bukti.
