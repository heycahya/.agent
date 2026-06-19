---
description: The Golden Loop — Siklus pengembangan utama
---

# 🔄 The Golden Loop

Setiap siklus = satu fitur. Urutan ini tidak boleh dibalik.
Satu nomor mengikat satu siklus penuh: prompt → issue → handoff.

---

## LANGKAH 0 — ORCHESTRATOR
**Agen:** @orchestrator | **Model:** gemini 3.1 pro (high) | **Env:** Antigravity

**Trigger:** Awal siklus baru setelah PR sebelumnya merged, atau kick-off project.

1. Baca handoff terbaru di `.agents/handoffs/`
2. Baca kodebase project langsung
3. Baca `.agents/artifacts/orchestrator/system-design.md`
4. Jalankan skill `orchestrate_prompt`
5. Tulis prompt ke `.agents/prompts/[N]-[slug].md`

**Output ke User:**
```
✅ Prompt [N] siap di: .agents/prompts/[N]-[slug].md
Copy isinya dan paste ke chat @arsitek.
```

---

## LANGKAH 1 — ARSITEK
**Agen:** @arsitek | **Model:** gemini 3.1 pro (high)

**Trigger:** User paste isi `prompts/[N]-[slug].md` ke chat @arsitek.

1. Baca `DESIGN.md`
2. Baca handoff terbaru di `.agents/handoffs/`
3. Jalankan skill `write_specs`
4. Tulis issue ke `.agents/artifacts/issues/[N]-[slug].md`

**Output ke User:**
```bash
# Submit ke GitHub Issues:
gh issue create --title "feat: [nama]" --body-file .agents/artifacts/issues/[N]-[slug].md

# Buat branch setelah issue terbuat:
git checkout -b feature/[nama-fitur]

# Lalu pindah ke chat @engineer dan kirim:
# "kerjakan github issue [URL issue]"
```

**HALT** — tunggu konfirmasi User sebelum siklus lanjut.

---

## LANGKAH 2 — ENGINEER
**Agen:** @engineer | **Model:** gemini 3.5 flash (high)

**Trigger:** User kirim "kerjakan github issue [URL]" ke chat @engineer.

1. Baca GitHub Issue
2. Jalankan skill `generate_code`
3. Implementasi kode secara incremental
4. Tulis / update test sesuai issue
5. **Minta User jalankan test dan paste output**

**Loop sampai 100% passed:**
- Jika ada yang gagal → analisis, perbaiki, minta User jalankan ulang

**Setelah 100% passed:**
6. Tulis handoff ke `.agents/handoffs/[N]-[slug].md`

**Output ke User:**
```bash
git add .
git commit -m "feat: [nama] closes #[nomor]"
git push origin feature/[nama-fitur]
gh pr create --title "feat: [nama]" --body "Closes #[nomor]"

# Setelah PR dibuat, pindah ke chat @reviewer dan kirim:
# "review PR [URL PR]" lalu paste output test yang sama
```

---

## LANGKAH 3 — REVIEWER
**Agen:** @reviewer | **Model:** claude sonnet 4.6 (thinking)

**Trigger:** User kirim "review PR [URL]" + paste output test.

1. Baca kode PR
2. Analisis test log
3. Jalankan skill `audit_code`

**Jika REVISION NEEDED:**
```
User kembali ke chat @engineer dengan daftar revision
→ kembali ke Langkah 2 (iterasi)
→ User paste log baru setelah fix
```

**Jika APPROVED:**
```bash
gh pr merge [nomor] --merge
```
→ Kembali ke **Langkah 0** untuk siklus berikutnya.

---

## INTERRUPT — ERROR MERAH
*Bisa terjadi di Langkah 2 atau 3*

```
1. STOP — jangan modifikasi kode apapun
2. Pindah ke chat @debugger
3. Paste error log lengkap
4. @debugger jalankan skill debug_issue
5. Setelah bug ticket + fix plan siap → kembali ke @engineer
```
