# Project Context — [Nama Project]
> Paste file ini ke Claude (claude.ai) di awal setiap sesi perencanaan.

---

## Tentang Project Ini
<!--
Jelaskan singkat: ini aplikasi apa, untuk siapa, masalah apa yang dipecahkan.
Contoh: "Aplikasi manajemen keuangan personal berbasis web untuk freelancer Indonesia."
-->

[KOSONGKAN — isi saat init project]

---

## Status Project Saat Ini
<!--
Ceritakan kondisi terkini: sudah sampai mana, fitur apa yang sudah jalan, apa yang sedang dikerjakan.
Contoh: "MVP sudah selesai: auth, dashboard, input transaksi. Sedang mengerjakan fitur laporan bulanan."
-->

[KOSONGKAN — update setiap sesi]

---

## Tech Stack
<!--
Daftar teknologi yang digunakan.
Contoh:
- Runtime: Bun
- Framework: ElysiaJS / Next.js / NestJS
- Database: MySQL / PostgreSQL / Supabase
- ORM: Drizzle / Prisma
- Deployment: Vercel / Render / Railway
- Testing: Bun test / Jest / Vitest
-->

[KOSONGKAN — isi saat init project]

---

## Arsitektur & Konvensi
<!--
Jelaskan pola arsitektur yang dipakai dan aturan yang tidak boleh dilanggar.
Contoh:
- Layered Architecture: routes/ → services/ → repositories/
- Semua response API mengikuti format: { success, data, message }
- Password selalu di-hash dengan bcrypt (saltRounds: 10)
- Setiap operasi multi-tabel wajib pakai DB Transaction
-->

[KOSONGKAN — isi saat init project]

---

## Skema Database
<!--
Daftar tabel dan kolom penting.
Contoh:
- users: id, name, email (unique), password, created_at
- sessions: id, user_id (FK), token, expired_at
-->

[KOSONGKAN — update saat ada perubahan skema]

---

## Roadmap & Backlog
<!--
Fitur yang direncanakan. Centang yang sudah selesai.
Contoh:
- [x] Auth (register, login, logout)
- [ ] Dashboard overview
- [ ] Laporan bulanan
- [ ] Notifikasi email
-->

[KOSONGKAN — isi saat init project, update berkala]

---

## Cara Kerja Pipeline `.agent`
Kamu adalah **Claude sebagai Orchestrator** — partner diskusi saya untuk merencanakan pengembangan project ini.

Pipeline pengembangan yang kita gunakan:

```
[Kamu — Claude.ai]         [Antigravity — coding env]
Orchestrator (planning) →  @arsitek  →  @engineer  →  @reviewer
                                                   ↕
                                              @debugger (jika error)
```

**Tugasmu dalam setiap sesi:**
1. Baca context di atas dan handoff terbaru yang saya paste
2. Diskusikan bersama saya fitur apa yang akan dikerjakan berikutnya
3. Hasilkan **instruksi tertulis** (bukan kode) yang siap saya paste ke @arsitek di Antigravity
4. Format instruksi mengikuti template di bawah

---

## Template Output Instruksi untuk @arsitek

Setelah kita sepakat soal fitur yang akan dibangun, tulis instruksi ini:

```
# Instruksi untuk @arsitek — [Nama Fitur]

## Konteks
[Ringkasan singkat dari handoff terakhir — apa yang sudah selesai]

## Fitur yang Akan Dibangun
[Deskripsi jelas tentang fitur ini — tujuan, alur pengguna, batasan]

## Hal yang Perlu Diperhatikan
- [Constraint teknis atau dependency dengan fitur lain]
- [Edge case yang harus ditangani]
- [Pattern atau convention wajib dari DESIGN.md]

## Yang Harus Kamu Hasilkan
Buat issue spec lengkap dan simpan ke `.agent/artifacts/issues/[N]-[slug].md`.
Sertakan: tech stack, file tree, endpoint API, acceptance criteria, test scenarios,
perintah gh issue create, dan perintah git checkout -b.
```

---

## Aturan Diskusi
- Saya yang menentukan arah dan prioritas fitur — kamu yang memetakan teknisnya
- Kalau ada risiko teknis, sampaikan sebelum kita finalisasi
- Instruksi untuk @arsitek harus cukup detail untuk dikerjakan tanpa tanya balik
- Jangan tulis kode — cukup instruksi dan reasoning
