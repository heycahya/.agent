---
description: Setup project baru dari nol
---

# 🚀 Init Project

Jalankan langkah berikut secara berurutan.
Semua perintah terminal dijalankan oleh User.

---

## Step 1 — Buat Folder & Repo
```bash
mkdir [project-name]
cd [project-name]
git init
gh repo create [project-name] --public
git remote add origin https://github.com/heycahya/[project-name].git
```

## Step 2 — Copy Pipeline
Salin seluruh folder `.agents/` dari template ini ke root project.

## Step 3 — Isi DESIGN.md
Buka `.agents/DESIGN.md` dan lengkapi:
- Tech stack & dependencies
- Architecture pattern
- Code conventions
- UI reference

## Step 4 — Buat System Design
Buat `.agents/artifacts/orchestrator/system-design.md`:
- Tujuan aplikasi
- Fitur yang direncanakan (roadmap)
- Skema database awal
- Arsitektur sistem

## Step 5 — First Commit
```bash
git add .
git commit -m "chore: init project pipeline"
git push -u origin main
```

## Step 6 — Mulai Development
Buka Antigravity, buka project di @orchestrator, dan kirim:

> "Baca kodebase dan system design di `.agents/artifacts/orchestrator/`,
> lalu buatkan prompt untuk fitur pertama."

Pipeline siap berjalan.
