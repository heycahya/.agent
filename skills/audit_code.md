# Skill: audit_code
> Digunakan oleh: @reviewer

## Objective
Review objektif dan menyeluruh.
@reviewer menggunakan model beda vendor dari @engineer — ini disengaja untuk menghilangkan bias.
Approval tanpa dasar dilarang keras.

---

## Trigger
Dipanggil saat user mengirim: "review PR [URL]"
Antigravity menjalankan test secara mandiri untuk mendapatkan log terbaru.

---

## Checklist Review

### ✅ Functional Correctness
- [ ] Semua acceptance criteria di issue terpenuhi?
- [ ] Semua test scenarios yang tercantum di issue ada di test file?
- [ ] Test log bersih: 0 failed, 0 skipped?
- [ ] Ada test state cleanup di awal setiap suite?

### ✅ Security
- [ ] Semua endpoint sensitif dilindungi middleware auth?
- [ ] Input validation ada di setiap endpoint yang menerima data?
- [ ] Tidak ada raw query tanpa parameter binding?
- [ ] Tidak ada data sensitif (password hash, token) di-expose di response?

### ✅ Code Quality
- [ ] Tidak ada N+1 query? (gunakan eager loading / join)
- [ ] DB Transaction digunakan di semua operasi multi-tabel?
- [ ] Tidak ada duplikasi logic? (DRY)
- [ ] Tidak ada dead code atau placeholder yang tidak diimplementasikan?

### ✅ Consistency
- [ ] Response format mengikuti standard di `DESIGN.md`?
- [ ] Naming convention konsisten dengan codebase?
- [ ] Struktur folder mengikuti arsitektur di `DESIGN.md`?
- [ ] Handoff sudah ditulis di `.agent/handoffs/`?

---

## Output

### Jika APPROVED
```
✅ REVIEW APPROVED — Issue #[N]: [Nama Fitur]

Semua [N] acceptance criteria terpenuhi.
Test log: [N] passed, 0 failed, 0 skipped.
Checklist: semua poin clear.
```

Antigravity eksekusi merge:
```bash
gh pr merge [nomor] --merge
```

### Jika REVISION NEEDED
```
⚠️ REVISION NEEDED — [N] masalah ditemukan:

1. `path/to/file.ts` baris [N]
   Masalah: [deskripsi eksak masalahnya]
   Solusi: [instruksi perbaikan spesifik — apa yang harus diubah]

2. `path/to/file.ts`
   Masalah: [deskripsi eksak]
   Solusi: [instruksi perbaikan spesifik]

@engineer: Perbaiki semua poin di atas.
Setelah selesai, jalankan ulang test dan sampaikan PR yang sama untuk di-review kembali.
```

---

## Larangan
- Tidak approve tanpa test log yang bersih
- Tidak menulis kode perbaikan
- Tidak melewati satu pun poin checklist meskipun perubahan tampak kecil
- Tidak approve jika handoff belum ada di `.agent/handoffs/`
