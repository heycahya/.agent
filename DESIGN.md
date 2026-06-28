# Design Document
> Dibaca oleh @arsitek dan @engineer di setiap siklus.
> Wajib diisi saat init project. Update setiap ada perubahan arsitektur.

---

## Tech Stack

### Runtime & Framework
<!--
Contoh: Bun + ElysiaJS / Node.js + NestJS / Next.js (fullstack)
-->

[KOSONGKAN — isi saat init project]

### Database & ORM
<!--
Contoh: MySQL + Drizzle / PostgreSQL + Prisma / Supabase
-->

[KOSONGKAN]

### Testing
<!--
Contoh: bun test / vitest / jest
Aturan state-clean: setiap test suite wajib truncate data sebelum dijalankan
-->

[KOSONGKAN]

### Deployment
<!--
Contoh: Vercel (frontend) + Railway (backend) / Render / Supabase
-->

[KOSONGKAN]

---

## Arsitektur

### Pola Arsitektur
<!--
Contoh: Layered Architecture
- src/routes/     → routing & request handling
- src/services/   → business logic
- src/repositories/ → database queries (jika dipisah)
- src/middlewares/ → auth guard, error handler
-->

[KOSONGKAN]

### Struktur Folder
<!--
Tempel struktur folder project di sini.
Contoh:
src/
├── routes/
│   ├── user.route.ts
│   └── auth.route.ts
├── services/
│   └── user.service.ts
└── middlewares/
    └── auth.middleware.ts
-->

[KOSONGKAN]

---

## Code Conventions

### Response Format API
<!--
Tentukan format standard response JSON.
Contoh:
Success: { success: true, data: {...}, message: "OK" }
Error:   { success: false, data: null, message: "Pesan error" }
-->

[KOSONGKAN]

### Naming Convention
<!--
Contoh:
- File: kebab-case (user.service.ts)
- Variable/Function: camelCase
- Class: PascalCase
- Database kolom: snake_case
-->

[KOSONGKAN]

### Aturan Wajib
<!--
Aturan yang tidak boleh dilanggar:
Contoh:
- Password selalu di-hash dengan bcrypt (saltRounds: 10)
- Semua operasi multi-tabel wajib pakai DB Transaction
- Tidak ada raw query tanpa parameter binding
- Semua endpoint butuh validasi input
- Eager loading untuk menghindari N+1 query
-->

[KOSONGKAN]

---

## Environment Variables
<!--
Daftar env var yang digunakan (tanpa value-nya).
Contoh:
- DATABASE_URL
- JWT_SECRET
- BCRYPT_SALT_ROUNDS
-->

[KOSONGKAN]
