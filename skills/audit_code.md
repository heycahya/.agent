# Skill: audit_code
> Digunakan oleh: @reviewer

## Objective
Review objektif. Model berbeda dari @engineer — ini disengaja agar tidak bias.
Approval buta dilarang keras.

---

## Trigger
Dipanggil setelah User mengirim link PR dan paste output test.

---

## Checklist Review

### ✅ Functional Correctness
- [ ] Semua acceptance criteria di issue terpenuhi?
- [ ] Semua test scenarios yang ditentukan di issue ada dan passed di log?
- [ ] Ada test yang dilewati atau tidak dijalankan?

### ✅ Security
- [ ] Semua endpoint sensitif dilindungi middleware yang tepat?
- [ ] Input validation ada di setiap endpoint yang menerima data?
- [ ] Tidak ada raw query tanpa parameter binding?
- [ ] Tidak ada data sensitif yang di-expose di response?

### ✅ Code Quality
- [ ] Tidak ada N+1 query? (gunakan eager loading)
- [ ] DB Transaction digunakan di semua operasi yang melibatkan lebih dari 1 tabel?
- [ ] Tidak ada duplikasi logic?
- [ ] Tidak ada dead code atau komentar yang tidak relevan?

### ✅ Consistency
- [ ] Response format mengikuti standard di `DESIGN.md`?
- [ ] Naming convention konsisten dengan codebase?
- [ ] Struktur folder mengikuti aturan di `DESIGN.md`?

---

## Output

### Jika APPROVED
```
✅ REVIEW APPROVED
Semua [N] acceptance criteria terpenuhi.
Test log bersih: [N] passed, 0 failed.

Instruksi User — merge PR:
gh pr merge [nomor] --merge
```

### Jika REVISION NEEDED
```
⚠️ REVISION NEEDED
[N] masalah ditemukan:

1. `path/to/file.ext` baris [N]
   Masalah: [deskripsi eksak]
   Solusi: [instruksi perbaikan spesifik]

2. `path/to/file.ext`
   Masalah: [deskripsi eksak]
   Solusi: [instruksi perbaikan spesifik]

@engineer: Perbaiki poin di atas.
Setelah selesai, minta User jalankan ulang test dan paste log baru ke chat ini.
```

---

## Larangan
- Tidak approve tanpa melihat test output dari User
- Tidak menulis kode perbaikan
- Tidak melewati checklist meskipun perubahan terlihat kecil
