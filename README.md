# .agent — AI Development Pipeline Template

Template pipeline pengembangan berbasis AI untuk solo developer.
Clone repo ini ke setiap project baru sebagai sistem manajemen agen.

---

## Cara Pakai

1. Clone repo ini ke folder project baru:
   ```bash
   cp -r .agent/ /path/to/project-baru/.agent/
   ```

2. Tambahkan ke `.gitignore` project:
   ```
   .agent/
   ```

3. Buat `project-context.md` di root project menggunakan template di `.agent/project-context.md`

4. Isi `.agent/DESIGN.md` sesuai stack project

5. Ikuti `workflows/initproject.md` untuk setup lengkap

---

## Struktur Folder

```
.agent/
├── AGENTS.md              # definisi peran dan model setiap agen
├── DESIGN.md              # tech stack, arsitektur, conventions (diisi per project)
├── project-context.md     # system prompt untuk Claude.ai (Orchestrator)
├── artifacts/
│   └── issues/            # output @arsitek — issue spec per fitur
├── bugs/                  # output @debugger — bug ticket + RCA
├── handoffs/              # output @engineer — memory antar siklus
├── skills/                # instruksi behavior per agen
│   ├── write_specs.md
│   ├── generate_code.md
│   ├── audit_code.md
│   └── debug_issue.md
└── workflows/
    ├── initproject.md     # setup project baru dari nol
    └── startcycle.md      # golden loop — siklus pengembangan satu fitur
```

---

## Pipeline

```
[Claude.ai — Orchestrator]
Diskusi fitur → instruksi untuk @arsitek
        ↓
[@arsitek — Antigravity]
Issue spec → gh issue create → git checkout -b
        ↓
[@engineer — Antigravity]
Implementasi → test 100% → handoff → PR
        ↓
[@reviewer — Antigravity]
APPROVED → merge PR → siklus berikutnya
```

Interrupt: error merah → @debugger → RCA → bug ticket → kembali ke @engineer

---

## Agen & Model

| Agen | Model | Peran |
|------|-------|-------|
| Orchestrator | Claude.ai (browser) | Diskusi perencanaan fitur |
| @arsitek | gemini-2.5-pro | Issue spec & planning |
| @engineer | gemini-2.5-flash | Implementasi kode |
| @reviewer | claude-sonnet-4-6 | Code review gate |
| @debugger | Model pro (beda dari engineer) | Root cause analysis |

---

## Catatan

- `.agent/` masuk `.gitignore` — tidak ikut ke repository project
- `project-context.md` diletakkan di root project (ikut repo, bisa di-commit)
- Setiap siklus punya satu nomor yang mengikat: `issue-N → handoff-N → bug-N` (jika ada)
- Numbering sequential ascending: 01 → 02 → 03 ...
