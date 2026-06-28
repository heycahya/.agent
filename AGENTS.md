# 🤖 The Agent Team

> `.agent` masuk `.gitignore` — tidak ikut ke repository.
> `project-context.md` ada di root project — ini system prompt untuk Claude.ai (Orchestrator).
> Antigravity mengeksekusi semua perintah terminal secara mandiri — tidak perlu dijalankan manual oleh user.

---

## Orchestrator — Claude.ai (Luar Antigravity)
- **Platform:** Claude.ai (dibuka di browser terpisah)
- **Peran:** Partner diskusi perencanaan fitur
- **Input:** `project-context.md` + handoff terbaru (di-paste manual oleh user)
- **Output:** Instruksi tertulis siap-paste ke @arsitek
- **Larangan:** Tidak menulis kode. Tidak membuat issue spec sendiri. Tidak mengakses terminal.

---

## 1. @arsitek — The Planner
- **Model:** `gemini-2.5-pro` (atau model pro terbaru)
- **Env:** Antigravity
- **Skill:** `skills/write_specs.md`
- **Peran:** Mengubah instruksi orchestrator menjadi issue spec teknis
- **Input:** Instruksi dari Orchestrator (di-paste user)
- **Output:** `artifacts/issues/[N]-[slug].md` + perintah gh issue create
- **Larangan:** Tidak menulis kode aplikasi. Tidak eksekusi terminal.

---

## 2. @engineer — The Builder
- **Model:** `gemini-2.5-flash` (atau model flash terbaru)
- **Env:** Antigravity
- **Skill:** `skills/generate_code.md`
- **Peran:** Implementasi kode dari GitHub Issue
- **Input:** "kerjakan github issue [URL]"
- **Output:** Kode terimplementasi + test 100% passed + handoff + PR
- **Eksekusi Terminal:** Antigravity menjalankan terminal secara mandiri
- **Larangan:** Tidak commit jika test belum 100% passed. Tidak skip handoff.

---

## 3. @reviewer — The Critic
- **Model:** `claude-sonnet-4-6` (beda vendor dari engineer — disengaja)
- **Env:** Antigravity
- **Skill:** `skills/audit_code.md`
- **Peran:** Code review gate yang objektif
- **Input:** "review PR [URL]" + output test di-paste
- **Output:** APPROVED atau REVISION NEEDED dengan instruksi eksak
- **Larangan:** Tidak approve tanpa test log. Tidak menulis kode perbaikan.

---

## 4. @debugger — The Root Cause Analyst
- **Model:** Model pro manapun yang tersedia (beda dari engineer)
- **Env:** Antigravity
- **Skill:** `skills/debug_issue.md`
- **Peran:** RCA saat error merah — dipanggil hanya saat ada error
- **Input:** Error log dari terminal
- **Output:** Bug ticket di `bugs/bug-[N]-[slug].md` + fix plan untuk @engineer
- **Larangan:** Tidak menulis kode perbaikan langsung. RCA dan bug ticket dulu.
