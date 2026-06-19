# Skill: debug_issue
> Digunakan oleh: @debugger

## Objective
Temukan akar masalah, bukan tambal gejala.
Buat bug ticket tertulis sebelum ada satu baris pun kode yang diperbaiki.

---

## Trigger
HANYA dipanggil saat User melaporkan error merah dari terminal.
Bukan untuk code smell atau review biasa.

---

## Steps

### 1. Stop Semua Modifikasi
Sampaikan ke User:
> "Tahan dulu. Jangan modifikasi kode apapun sebelum RCA selesai."

### 2. Baca Error Log
Analisis log yang di-paste User secara menyeluruh.
Bedakan antara:
- **Symptom** — apa yang tampak di error
- **Root Cause** — mengapa error itu terjadi

### 3. Cek Konteks (Jika Perlu)
Baca file yang relevan di project untuk konfirmasi root cause.

### 4. Tentukan Nomor Bug
Format: `bug-[N]-[slug]`
N = nomor issue/handoff yang sedang dikerjakan saat bug muncul.

### 5. Tulis Bug Ticket
Simpan ke `bugs/bug-[N]-[slug].md`:

```markdown
# Bug [N]: [Judul Singkat]
**Terkait Issue:** #[nomor GitHub]
**Ditemukan di:** Fase [implementasi | review | testing]
**Status:** Open

## Symptom
[Copy paste error yang dilaporkan User]

## Root Cause
[Penjelasan teknis mengapa error ini terjadi — bukan hanya di mana]

## Fix Plan
Instruksi eksak untuk @engineer:
1. File `path/to/file.ext`: ubah [ini] menjadi [itu]
2. File `path/to/file.ext`: tambahkan [apa] di [mana]

## Verifikasi
Test scenario yang harus passed setelah fix:
- [ ] [test case spesifik]
```

### 6. Berikan Perintah Log Bug
```bash
gh issue create --title "bug: [judul singkat]" --body-file .agents/bugs/bug-[N]-[slug].md
```

### 7. Serahkan ke @engineer
```
Bug ticket siap di: .agents/bugs/bug-[N]-[slug].md

@engineer: Baca file tersebut dan terapkan Fix Plan yang sudah ditulis.
Setelah selesai, jalankan test dan paste output ke chat.
```

---

## Larangan
- Bug ticket tidak dihapus setelah fix — ini history permanen
- Tidak menulis kode perbaikan langsung tanpa bug ticket dulu
- Tidak skip RCA meskipun fix-nya terlihat sepele
