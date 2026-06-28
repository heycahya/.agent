# Skill: debug_issue
> Digunakan oleh: @debugger

## Objective
Temukan akar masalah (root cause), bukan tambal gejala.
Bug ticket tertulis wajib ada sebelum ada satu baris kode yang diperbaiki.

---

## Trigger
HANYA dipanggil saat ada error merah dari terminal.
Bukan untuk code smell, review biasa, atau pertanyaan teknis.

---

## Steps

### 1. Stop Semua Modifikasi
Sampaikan ke user dan @engineer:
> "Tahan dulu. Jangan modifikasi kode apapun sebelum RCA selesai dan bug ticket siap."

### 2. Analisis Error Log
Baca log yang diberikan secara menyeluruh.
Bedakan dengan jelas:
- **Symptom** — apa yang tampak di error (pesan error, baris file)
- **Root Cause** — mengapa error itu terjadi (logic yang salah, missing validation, race condition, dll)

### 3. Konfirmasi Root Cause
Baca file yang relevan di project untuk verifikasi root cause sebelum menulis bug ticket.

### 4. Tentukan Nomor Bug
Format: `bug-[N]-[slug]`
N = nomor issue/handoff yang sedang dikerjakan saat bug muncul.

### 5. Tulis Bug Ticket
Simpan ke `.agent/bugs/bug-[N]-[slug].md`:

```markdown
# Bug [N]: [Judul Singkat]
**Terkait Issue:** #[nomor GitHub] — [URL]
**Ditemukan di Fase:** [implementasi | review | testing]
**Status:** Open

## Symptom
[Copy-paste error log yang dilaporkan]

## Root Cause
[Penjelasan teknis mengapa error ini terjadi — bukan hanya di mana, tapi mengapa]

## Fix Plan
Instruksi eksak untuk @engineer (tanpa menulis kode lengkap):
1. File `path/to/file.ts`: [apa yang harus diubah dan mengapa]
2. File `path/to/file.ts`: [apa yang harus ditambahkan dan di mana]

## Verifikasi Fix
Test scenario yang harus passed setelah fix:
- [ ] [test case spesifik yang merepresentasikan bug ini]
- [ ] [test case regression untuk memastikan tidak ada yang rusak]
```

### 6. Log Bug ke GitHub (Antigravity Eksekusi Mandiri)
```bash
gh issue create --title "bug: [judul singkat]" --body-file .agent/bugs/bug-[N]-[slug].md --label bug
```

### 7. Serahkan ke @engineer
```
Bug ticket siap: .agent/bugs/bug-[N]-[slug].md
GitHub Issue: [URL]

@engineer: Baca bug ticket tersebut dan terapkan Fix Plan.
Setelah fix, jalankan test (termasuk test case verifikasi di ticket) dan pastikan semua passed.
```

---

## Larangan
- Bug ticket tidak boleh dihapus setelah fix — ini adalah history permanen
- Tidak menulis kode perbaikan langsung di sini
- Tidak skip RCA meskipun fix-nya terlihat sepele
- Tidak gunakan nomor berbeda dari nomor issue yang sedang berjalan
