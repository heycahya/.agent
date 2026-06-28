---
description: Setup project baru dari nol
---

# 🚀 Init Project

Ikuti langkah ini secara berurutan saat memulai project baru.

---

## Step 1 — Buat Folder & Repo

Antigravity menjalankan:
```bash
mkdir [project-name]
cd [project-name]
git init
gh repo create [project-name] --public --source=. --remote=origin
```

---

## Step 2 — Copy `.agent`

Salin seluruh folder `.agent` dari template ini ke root project baru.

Tambahkan ke `.gitignore`:
```
.agent/
```

---

## Step 3 — Isi `project-context.md`

Buat file `project-context.md` di root project.
Gunakan template dari draft ini.

Isi bagian yang kosong:
- Tentang project
- Tech stack
- Arsitektur & konvensi
- Skema database awal
- Roadmap awal

---

## Step 4 — Isi `.agent/DESIGN.md`

Buka `.agent/DESIGN.md` dan lengkapi:
- Tech stack & versi
- Pola arsitektur dan struktur folder
- Code conventions
- Response format API
- Aturan wajib (security, transaction, dll)

---

## Step 5 — Scaffolding Project (jika dari nol)

Buka Antigravity, arahkan ke @arsitek, kirim:

> "Buat scaffolding project baru. Stack: [sebutkan stack]. 
> Buat struktur folder sesuai `DESIGN.md`. 
> Buat file konfigurasi dasar (package.json / bun.lockb / drizzle.config.ts / .env.example).
> Setelah selesai, jalankan project dan pastikan bisa start tanpa error."

---

## Step 6 — First Commit

Antigravity menjalankan:
```bash
git add .
git commit -m "chore: init project"
git push -u origin main
```

---

## Step 7 — Mulai Development

Buka Claude.ai di browser.
Paste isi `project-context.md`.
Mulai diskusi fitur pertama.

Pipeline siap berjalan. Lanjut ke `workflows/startcycle.md`.
