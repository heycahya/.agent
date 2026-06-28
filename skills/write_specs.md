# Skill: write_specs
> Digunakan oleh: @arsitek

## Objective
Ubah instruksi dari Orchestrator menjadi blueprint teknis yang bisa langsung dieksekusi @engineer.
Output harus cukup detail sehingga @engineer tidak perlu bertanya balik.

---

## Steps

### 1. Baca Input
- Baca instruksi yang di-paste user
- Baca `.agent/DESIGN.md` untuk stack dan conventions
- Baca handoff terbaru di `.agent/handoffs/` untuk konteks progress

### 2. Tentukan Nomor Issue
- Cek nomor tertinggi yang sudah ada di `.agent/artifacts/issues/`
- Gunakan nomor berikutnya (01 → 02 → 03 ...)
- Jika folder masih kosong, mulai dari 01

### 3. Tulis Issue Spec
Simpan ke `.agent/artifacts/issues/[N]-[slug].md`:

```markdown
# Issue [N]: [Nama Fitur]

## Tujuan
[Apa yang ingin dicapai dengan fitur ini — 2-3 kalimat]

## Tech Stack
[Framework, library, dan versi eksak yang digunakan untuk fitur ini]

## File Tree
File yang akan dibuat atau dimodifikasi:
- `path/to/file.ts` — [dibuat | dimodifikasi] — keterangan singkat

## Skema Database (jika ada)
Tabel baru atau perubahan kolom:
- Tabel `nama`: kolom (tipe, constraint), kolom (tipe, constraint)
Migration: [instruksi eksak jika ada]

## API Endpoints
| Method | URI             | Middleware | Request Body       | Response           |
|--------|-----------------|------------|--------------------|--------------------| 
| POST   | /api/[resource] | auth       | { field: type }    | { success, data }  |

## Logic Notes
- [Hal penting untuk implementasi]
- [Edge case yang harus ditangani]
- [Pattern wajib: DB Transaction, eager loading, dll]
- [Dependency dengan fitur lain]

## Test Scenarios
Semua skenario ini harus ada dan passed:
- [ ] Happy path — [deskripsi] → HTTP [kode]
- [ ] Validasi gagal — [field apa] invalid → HTTP 422
- [ ] Unauthorized — tanpa token → HTTP 401
- [ ] Forbidden — role salah → HTTP 403
- [ ] Edge case — [deskripsi spesifik]

## Acceptance Criteria
- [ ] Semua endpoint berjalan sesuai spesifikasi di atas
- [ ] Semua test scenarios di atas passed 100%
- [ ] Tidak ada regresi pada test yang sudah ada
- [ ] Handoff ditulis sebelum PR dibuat
```

### 4. Antigravity Eksekusi Langsung
Jalankan perintah berikut:
```bash
# Submit ke GitHub Issues:
gh issue create --title "feat: [nama fitur]" --body-file .agent/artifacts/issues/[N]-[slug].md

# Buat branch setelah issue terbuat:
git checkout -b feature/[nama-fitur]
```

Kemudian sampaikan ke user:
```
✅ Issue [N] siap: [URL GitHub Issue]
Branch: feature/[nama-fitur]

Lanjut ke @engineer dan kirim:
"kerjakan github issue [URL issue]"
```

---

## Larangan
- Tidak menulis kode aplikasi
- Tidak skip bagian Test Scenarios dan Acceptance Criteria
- Nomor harus sequential, tidak boleh duplikat atau loncat
- Tidak modifikasi `handoffs/`
