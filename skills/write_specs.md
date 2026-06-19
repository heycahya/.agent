# Skill: write_specs
> Digunakan oleh: @arsitek

## Objective
Ubah prompt dari @orchestrator menjadi blueprint teknis yang bisa langsung dieksekusi @engineer.

---

## Steps

### 1. Baca Input
- Baca prompt yang di-paste User
- Baca `DESIGN.md` untuk stack dan conventions
- Baca handoff terbaru di `handoffs/` untuk konteks

### 2. Tentukan Nomor
Gunakan nomor yang sama dengan prompt yang diterima.
(prompt-99 → issue-99, prompt-98 → issue-98)

### 3. Tulis Issue Spec
Simpan ke `artifacts/issues/[N]-[slug].md`:

```markdown
# Issue [N]: [Nama Fitur]

## Tech Stack
Framework dan versi eksak yang digunakan.

## File Tree
File yang akan dibuat atau dimodifikasi:
- `path/to/file.ext` — [dibuat | dimodifikasi] — keterangan singkat

## Data Schema
Tabel baru atau perubahan kolom (jika ada):
- Tabel `nama`: kolom1 (tipe), kolom2 (tipe)

## API Endpoints
| Method | URI | Middleware | Deskripsi |
|--------|-----|------------|-----------|

## Logic Notes
- Hal penting untuk implementasi
- Edge case yang harus ditangani
- Pattern yang wajib diikuti (DB Transaction, lockForUpdate, dll)

## Test Scenarios
Skenario yang harus ditulis dan diverifikasi:
- [ ] Happy path — HTTP 200/201
- [ ] Validasi gagal — HTTP 422
- [ ] Akses ditolak role salah — HTTP 403
- [ ] Edge case spesifik

## Acceptance Criteria
- [ ] Semua endpoint berjalan sesuai spesifikasi di atas
- [ ] Semua test scenarios passed 100%
- [ ] Tidak ada regresi pada test yang sudah ada
```

### 4. Berikan Perintah ke User

```
✅ Issue spec siap di: .agents/artifacts/issues/[N]-[slug].md

Jalankan perintah berikut:

# 1. Submit ke GitHub:
gh issue create --title "feat: [nama fitur]" --body-file .agents/artifacts/issues/[N]-[slug].md

# 2. Setelah issue terbuat, buat branch:
git checkout -b feature/[nama-fitur]

# 3. Pindah ke chat @engineer dan kirim:
#    "kerjakan github issue [URL issue]"
```

---

## Larangan
- Tidak menulis kode aplikasi
- Nomor harus sama dengan nomor prompt yang diterima
- Tidak modifikasi `handoffs/` atau `prompts/`
