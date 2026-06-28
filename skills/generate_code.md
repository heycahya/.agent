# Skill: generate_code
> Digunakan oleh: @engineer

## Objective
Implementasi kode dari GitHub Issue secara incremental, verifikasi dengan test, tulis handoff.
Antigravity menjalankan semua perintah terminal secara mandiri.

---

## Steps

### 1. Baca Issue
Baca GitHub Issue yang diberikan.
Ini adalah satu-satunya sumber kebenaran. Jangan asumsi apapun di luar issue.
Baca juga `.agent/DESIGN.md` sebelum mulai menulis kode.

### 2. Implementasi Kode
- Edit file secara **incremental** — replace parsial, bukan tulis ulang file penuh
- **DRY** — tidak ada duplikasi logic
- **No placeholders** — semua fungsi fully implemented
- Ikuti conventions di `DESIGN.md` tanpa pengecualian
- Struktur folder mengikuti arsitektur yang sudah ditetapkan

### 3. Tulis / Update Test
- Tambahkan semua test scenarios yang tercantum di issue
- Jangan hapus atau ubah test yang sudah ada
- Wajib ada state cleanup (truncate / delete) di awal setiap test suite
- Cover: happy path, validasi gagal, unauthorized, forbidden, edge case

### 4. Jalankan Test (Antigravity Eksekusi Mandiri)
```bash
# Sesuaikan dengan stack yang digunakan:
bun test         # Bun
npm test         # Node.js
php artisan test # Laravel
```

**Loop sampai 100% passed:**
- Jika ada yang gagal → analisis error → perbaiki kode → jalankan ulang
- Ulangi sampai semua passed, 0 failed

> ⚠️ WAJIB: Tidak boleh lanjut ke langkah 5 sebelum semua test 100% passed.

### 5. Tulis Handoff (Hanya Setelah 100% Passed)
Gunakan nomor yang sama dengan nomor issue.
Simpan ke `.agent/handoffs/[N]-[slug].md`:

```markdown
# Handoff [N]: [Nama Fitur]
**Issue:** #[nomor GitHub] — [URL]
**Branch:** `feature/[nama]`
**Status:** ✅ Siap PR

## Yang Diimplementasikan
- [Fitur/fungsi 1]: deskripsi singkat
- [Fitur/fungsi 2]: deskripsi singkat

## File yang Diubah
- `path/to/file.ts` — [dibuat | dimodifikasi] — deskripsi perubahan

## Skema DB (jika ada)
- Tabel baru / kolom baru / migration yang dijalankan

## Hasil Test
- Total: [N] passed, 0 failed
- Skenario yang dicover: [daftar singkat]

## Catatan untuk Siklus Berikutnya
[Hal teknis penting yang perlu diketahui Orchestrator, @arsitek, atau @engineer berikutnya]
[Dependency yang dibuat, pola baru yang diperkenalkan, utang teknis jika ada]

## Bug yang Diselesaikan di Siklus Ini
- bug-[N]-[slug]: [judul bug] ← kosongkan jika tidak ada bug
```

### 6. Commit & PR (Antigravity Eksekusi Mandiri)
```bash
git add .
git commit -m "feat: [nama fitur] closes #[nomor]"
git push origin feature/[nama-fitur]
gh pr create --title "feat: [nama fitur]" --body "Closes #[nomor]

## Test Result
[paste ringkasan output test]"
```

Kemudian sampaikan ke user:
```
✅ PR siap: [URL PR]
Test: [N] passed, 0 failed

Lanjut ke @reviewer dan kirim:
"review PR [URL PR]"
```

---

## Larangan
- Tidak commit jika test belum 100% passed
- Tidak skip pembuatan handoff
- Tidak gunakan nomor berbeda dari nomor issue
- Tidak modifikasi test yang sudah ada kecuali ada instruksi eksplisit di issue