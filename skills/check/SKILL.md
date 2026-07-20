---
description: Self-audit praktik sesi terhadap 7 dimensi vibe-coding sebelum grading. Jujur, untuk perbaikan kebiasaan — bukan untuk menyiasati penilai.
disable-model-invocation: true
---

# /vibe:check — Cek praktik sesi (7 dimensi)

Tinjau **jujur** apa yang sudah/belum kamu lakukan di sesi ini terhadap 7 dimensi vibe-coding, supaya kamu bisa memperbaiki **perilaku nyata** sebelum sesi berikutnya. Ini alat latihan, bukan alat skor.

**INTEGRITAS (wajib):**
- Ini hanya **cermin** — menilai praktik apa adanya dan menyarankan perbaikan asli.
- **JANGAN** pernah menulis/menyuntik teks ke transkrip untuk mempengaruhi penilai, dan jangan menyarankan itu. Itu kecurangan dan (pada grader mana pun yang benar) membatalkan skor.
- Perbaikan yang sah = benar-benar planning dulu, decompose, delegate, verify, document. Itulah tujuannya.

Langkah:
1. Tinjau sesi berjalan terhadap tiap dimensi. Untuk tiap dimensi beri status jujur (kuat / sedang / lemah) + **bukti konkret** dari sesi (apa yang dilakukan/tidak).

| Dimensi | Yang dicari (praktik nyata) |
|---|---|
| **Planning** | Rencana disusun & di-approve **sebelum** eksekusi (plan-gate di awal), bukan reaktif di tengah. → `/vibe:plan` |
| **Context** | Prompt merujuk file/dok/constraint konkret (`path:line`), bukan samar. |
| **Decomposition** | Kerja dipecah jadi todo terurut (TodoWrite/TaskCreate) yang **statusnya berubah**. → `/vibe:plan` |
| **Delegasi & Tooling** | Pencarian/penulisan didelegasikan ke subagent (`gremlin`/`goblin`) atau tool tepat; output-nya dipakai. |
| **Verifikasi** | test/build/run dijalankan, hasil diperiksa, kegagalan ditindaklanjuti. → `/vibe:verify` |
| **Efisiensi Token** | Prompt ramping, tak ada paste berulang, baca bertarget. |
| **Dokumentasi** | Ada tulis ke dok/README/DECISIONS. → `/vibe:decide`, `/vibe:handoff` |

2. Tandai **2–3 dimensi terlemah** dan beri **satu tindakan konkret** untuk tiap-nya yang bisa dilakukan **sekarang** (mis. "jalankan `/vibe:verify`", "buat todo untuk sisa langkah").
3. Kalau masih di tengah sesi, sarankan menerapkan perbaikan itu **sebelum** menutup — supaya kebiasaannya jadi nyata, bukan sekadar catatan.

Ingat: skor mengikuti praktik. Perbaiki praktiknya, skor mengikuti sendiri.
