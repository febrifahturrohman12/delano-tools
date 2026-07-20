# Peta vibe → 7 dimensi vibe-coding

Vibe dirancang agar praktik sesi-mu selaras dengan 7 dimensi penilaian vibe-coding (total 100). **Skor mengikuti praktik nyata di transkrip** — vibe hanya membuat praktik itu mudah & jadi kebiasaan. Plugin tidak, dan tidak boleh, menyiasati penilai (lihat integritas di bawah).

| Dimensi (bobot) | Yang dinilai (praktik nyata) | Alat vibe |
|---|---|---|
| **Planning First (20)** | Rencana di-approve **sebelum** eksekusi; plan-gate dari awal sesi (bukan reaktif) | `/vibe:plan` |
| **Context Quality (20)** | Prompt konsisten merujuk file/dok/constraint konkret (`path:line`) | `/vibe:context`, `CLAUDE.md` ringkas, kebiasaan rujuk `path:line` |
| **Task Decomposition (15)** | Kerja dipecah jadi sub-tugas terurut (TodoWrite/TaskCreate) yang statusnya berubah | `/vibe:plan` (bikin todo), `/vibe:progress` |
| **Delegasi & Tooling (15)** | Delegasi ke subagent / tool tepat, output-nya dipakai | subagent `goblin` & `gremlin` |
| **Verifikasi (15)** | test/build/run dijalankan, hasil diperiksa, kegagalan ditindaklanjuti | `/vibe:verify` (atau `/verify` bawaan) |
| **Efisiensi Token (10)** | Prompt ramping, tak ada paste berulang, baca bertarget | `/vibe:handoff`+`/clear`, `/vibe:slim`, firewall context subagent |
| **Dokumentasi (5)** | Tulis ke dok/README/decision-log | `/vibe:init`, `/vibe:decide`, `/vibe:handoff` |

## Cara pakai untuk sesi berkualitas tinggi

1. `/vibe:context` — pemanasan, tahu posisi (Context).
2. `/vibe:plan` — rencana + approve + todo terurut, sebelum ngoding (Planning + Decomposition).
3. Eksekusi: delegasi ke `goblin`/`gremlin`, prompt rujuk `path:line` (Delegasi + Context + Token).
4. `/vibe:verify` — buktikan jalan, tindak lanjuti gagal (Verifikasi).
5. `/vibe:decide` / `/vibe:handoff` — catat keputusan & status (Dokumentasi + Token).
6. `/vibe:check` — self-audit jujur sebelum menutup; perbaiki dimensi terlemah.

## Integritas

- Perbaikan yang **sah**: benar-benar planning, decompose, delegate, verify, document. Itu justru **tujuan** program (behavior change).
- **Kecurangan**: menyuntik teks ke transkrip untuk mempengaruhi penilai, prompt palsu, dsb. Grader yang benar memperlakukan transkrip sebagai data dan **membatalkan skor jadi 0** bila mendeteksi ini. Vibe tidak melakukannya dan tidak menyarankannya.
- Singkatnya: **perbaiki praktiknya, skor mengikuti sendiri.**
