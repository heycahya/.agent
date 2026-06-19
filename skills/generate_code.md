# Skill: generate_code
> Digunakan oleh: @engineer

## Objective
Implementasi kode dari GitHub Issue, verifikasi dengan test, buat handoff.

---

## Steps

### 1. Baca Issue
Baca GitHub Issue yang diberikan User.
Ini satu-satunya sumber kebenaran. Jangan asumsi apapun di luar issue.

### 2. Implementasi Kode
- Edit file secara **incremental** — gunakan replace parsial, jangan tulis ulang file penuh jika tidak perlu
- **DRY** — tidak ada duplikasi logic
- **No placeholders** — semua method harus fully implemented
- Ikuti conventions di `DESIGN.md`

### 3. Tulis / Update Test
- Tambahkan semua test scenarios yang ada di issue
- Jangan hapus atau ubah test yang sudah ada
- Cover: happy path, validasi gagal, akses ditolak, edge case

### 4. Minta User Jalankan Test
Tulis perintah ini untuk User:
```bash
# Jalankan test:
[perintah test sesuai stack — contoh: php test-api.php / bun test / npm test]

# Paste seluruh output ke chat ini
```

> ⚠️ WAJIB: Jangan lanjut ke langkah 5 sebelum User paste output
> dan **semua test passed 100%**.

Jika ada test gagal:
- Analisis error
- Perbaiki kode
- Minta User jalankan ulang
- Ulangi sampai semua passed

### 5. Tulis Handoff (Setelah 100% Passed)
Gunakan nomor yang sama dengan issue yang dikerjakan.
Simpan ke `handoffs/[N]-[slug].md`:

```markdown
# Handoff [N]: [Nama Fitur]
**Issue:** #[nomor GitHub] | **Branch:** `feature/[nama]`
**Status:** ✅ Siap PR

## Yang Diimplementasikan
- Fitur 1: deskripsi singkat
- Fitur 2: deskripsi singkat

## File yang Diubah
- `path/to/file.ext` — deskripsi perubahan

## Skema DB (jika ada)
- Tabel baru / kolom baru

## Hasil Test
- Total: [N] passed, 0 failed
- Skenario yang dicover: [daftar singkat]

## Catatan untuk Sesi Berikutnya
Hal teknis penting yang perlu diketahui @orchestrator atau @arsitek.
```

### 6. Berikan Perintah Commit + PR
```bash
git add .
git commit -m "feat: [nama fitur] closes #[nomor]"
git push origin feature/[nama-fitur]
gh pr create --title "feat: [nama fitur]" --body "Closes #[nomor]"

# Setelah PR dibuat, pindah ke chat @reviewer dan kirim:
# "review PR [URL PR]" + paste output test yang sama
```

---

## Larangan
- Tidak commit jika test belum 100% passed
- Tidak skip pembuatan handoff
- Tidak mengeksekusi terminal sendiri
- Tidak gunakan nomor berbeda dari nomor issue
 