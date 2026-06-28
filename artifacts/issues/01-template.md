# Issue 01: [Nama Fitur]

## Tujuan
[Apa yang ingin dicapai — 2-3 kalimat]

## Tech Stack
[Framework dan versi eksak]

## File Tree
- `src/routes/[nama].route.ts` — dibuat — routing endpoint
- `src/services/[nama].service.ts` — dibuat — business logic

## Skema Database (jika ada)
- Tabel `[nama]`: id (int, PK, auto increment), [kolom] ([tipe], [constraint])

## API Endpoints
| Method | URI | Middleware | Request Body | Response |
|--------|-----|------------|--------------|----------|
| POST | /api/[resource] | - | { field: string } | { success, data } |

## Logic Notes
- [Hal penting]
- [Edge case]

## Test Scenarios
- [ ] Happy path → HTTP 201
- [ ] Validasi gagal (field kosong) → HTTP 422
- [ ] [edge case spesifik] → HTTP [kode]

## Acceptance Criteria
- [ ] Semua endpoint berjalan sesuai spesifikasi
- [ ] Semua test scenarios passed 100%
- [ ] Tidak ada regresi
- [ ] Handoff ditulis sebelum PR dibuat
