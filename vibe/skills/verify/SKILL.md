---
description: Verifikasi perubahan dengan menjalankan test/build/run yang relevan dan menindaklanjuti kegagalan. Jalankan setelah membuat perubahan, sebelum menganggap selesai.
disable-model-invocation: true
---

# /vibe:verify — Buktikan perubahan benar-benar jalan

Tujuan: menutup tugas dengan **bukti**, bukan asumsi. Jalankan perintah test/build/run yang relevan, **periksa hasilnya**, dan **tindak lanjuti** bila gagal — bukan sekadar menjalankan sekali lalu lanjut.

> Kalau project punya skill `/verify` bawaan yang lebih lengkap (menggerakkan flow end-to-end), pakai itu. Skill ini adalah checklist ringan yang selaras untuk memastikan verifikasi benar-benar terjadi.

Langkah:
1. **Identifikasi apa yang berubah** dan permukaan runtime-nya (fungsi/endpoint/UI yang tersentuh). Perubahan yang cuma test/dok tak perlu di-drive.
2. **Jalankan perintah yang tepat** (lihat `CLAUDE.md` untuk perintah build/test/run project):
   - test unit/feature yang relevan, atau
   - build/compile, atau
   - jalankan app & latih alur yang berubah.
3. **Periksa tool_result-nya** — jangan anggap lulus tanpa membaca output. Sebutkan hasil apa adanya (lulus/gagal + angka).
4. **Kalau gagal → perbaiki, lalu ulang** sampai hijau atau blocker jelas. Kegagalan yang dibiarkan tanpa tindak lanjut = verifikasi setengah.
5. Laporkan ringkas: perintah apa dijalankan, hasilnya, tindakan bila ada.

Jujur soal hasil: kalau test gagal, katakan gagal dengan output-nya; kalau ada langkah dilewati, sebutkan. Jangan klaim "selesai" tanpa bukti.
