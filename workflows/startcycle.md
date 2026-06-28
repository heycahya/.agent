---
description: The Golden Loop — Siklus pengembangan satu fitur
---

# 🔄 The Golden Loop

Satu siklus = satu fitur.
Satu nomor mengikat satu siklus penuh: issue → handoff → (bug jika ada).
Nomor naik secara sequential: 01 → 02 → 03 ...

---

## LANGKAH 0 — ORCHESTRATOR (Claude.ai)
**Platform:** Claude.ai (browser, bukan Antigravity)

**Trigger:** Awal siklus baru, setelah PR sebelumnya merged.

1. Buka Claude.ai
2. Paste isi `project-context.md`
3. Paste isi handoff terbaru dari `.agent/handoffs/`
4. Diskusikan fitur berikutnya
5. Minta Claude tulis instruksi untuk @arsitek

**Output dari Claude:**
```
# Instruksi untuk @arsitek — [Nama Fitur]
[instruksi lengkap...]
```

6. Copy instruksi tersebut
7. Lanjut ke Langkah 1

---

## LANGKAH 1 — ARSITEK
**Agen:** @arsitek | **Env:** Antigravity

**Trigger:** Paste instruksi dari Orchestrator ke chat @arsitek.

**Yang dilakukan @arsitek:**
1. Baca instruksi
2. Baca `.agent/DESIGN.md`
3. Baca handoff terbaru di `.agent/handoffs/`
4. Jalankan skill `write_specs`
5. Tulis issue spec ke `.agent/artifacts/issues/[N]-[slug].md`

**Output @arsitek (Antigravity eksekusi langsung):**
```bash
# Submit ke GitHub Issues:
gh issue create --title "feat: [nama]" --body-file .agent/artifacts/issues/[N]-[slug].md

# Buat branch:
git checkout -b feature/[nama-fitur]
```

Lanjut ke Langkah 2 setelah issue terbuat dan branch siap.

---

## LANGKAH 2 — ENGINEER
**Agen:** @engineer | **Env:** Antigravity

**Trigger:** Kirim ke @engineer: "kerjakan github issue [URL issue]"

**Yang dilakukan @engineer:**
1. Baca GitHub Issue
2. Baca `.agent/DESIGN.md`
3. Implementasi kode secara incremental
4. Tulis / update test sesuai issue
5. Antigravity jalankan test secara mandiri
6. Loop sampai semua test 100% passed
7. Tulis handoff ke `.agent/handoffs/[N]-[slug].md`

**Output @engineer (Antigravity eksekusi langsung):**
```bash
git add .
git commit -m "feat: [nama] closes #[nomor]"
git push origin feature/[nama-fitur]
gh pr create --title "feat: [nama]" --body "Closes #[nomor]"
```

Lanjut ke Langkah 3 setelah PR terbuat.

---

## LANGKAH 3 — REVIEWER
**Agen:** @reviewer | **Env:** Antigravity

**Trigger:** Kirim ke @reviewer: "review PR [URL PR]"

**Yang dilakukan @reviewer:**
1. Baca kode PR
2. Baca test log (Antigravity jalankan ulang test)
3. Jalankan skill `audit_code`

**Jika REVISION NEEDED:**
```
Kembali ke @engineer dengan daftar revision
→ iterasi Langkah 2 sampai semua poin selesai
→ @reviewer review ulang
```

**Jika APPROVED (Antigravity eksekusi):**
```bash
gh pr merge [nomor] --merge
```

→ Update `project-context.md` bagian Status dan Roadmap
→ Kembali ke **Langkah 0** untuk siklus berikutnya

---

## INTERRUPT — ERROR MERAH
*Bisa terjadi di Langkah 2 atau 3*

```
1. STOP — @engineer berhenti, tidak modifikasi kode apapun
2. Pindah ke chat @debugger
3. Paste error log lengkap
4. @debugger jalankan skill debug_issue
5. Setelah bug ticket + fix plan siap di bugs/bug-[N]-[slug].md
6. Kembali ke @engineer dengan bug ticket tersebut
```

---

## RINGKASAN FLOW

```
[Claude.ai]
Orchestrator diskusi fitur
        ↓ (paste instruksi)
[@arsitek — Antigravity]
Tulis issue spec → gh issue create → git checkout -b
        ↓ (kerjakan github issue [URL])
[@engineer — Antigravity]
Implementasi → Test 100% → Handoff → PR
        ↓ (review PR [URL])
[@reviewer — Antigravity]
APPROVED → merge PR
        ↓
Siklus baru: kembali ke Orchestrator
```
