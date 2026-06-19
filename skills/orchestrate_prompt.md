# Skill: orchestrate_prompt
> Digunakan oleh: @orchestrator

## Objective
Baca konteks project terkini dan hasilkan prompt siap-tempel untuk @arsitek.

---

## Steps

### 1. Baca Konteks
- Baca handoff terbaru di `handoffs/` (file nomor tertinggi)
- Baca kodebase project langsung
- Baca `artifacts/orchestrator/system-design.md` untuk roadmap

### 2. Tentukan Nomor
- Cek nomor tertinggi yang sudah ada di `prompts/`
- Gunakan nomor berikutnya yang lebih kecil (99 → 98 → 97...)
- Jika `prompts/` masih kosong, mulai dari 99

### 3. Tulis Prompt
Simpan ke `prompts/[N]-[slug].md`:

```markdown
# Prompt [N]: [Nama Fitur]
> Paste seluruh isi file ini ke chat @arsitek

---

## Konteks Progress Terkini
[Ringkasan dari handoff terbaru — apa yang sudah selesai, apa yang belum]

## Fitur yang Akan Dibangun
[Deskripsi jelas fitur berikutnya berdasarkan roadmap]

## Hal yang Perlu Diperhatikan @arsitek
- [Constraint teknis atau dependency]
- [Hubungan dengan fitur yang sudah ada]
- [Edge case yang perlu di-cover]

## Instruksi
Buatkan issue spec untuk fitur di atas.
Simpan ke `artifacts/issues/[N]-[slug].md`.
Sertakan: tech stack, file tree, endpoint API, acceptance criteria,
perintah gh issue create, dan perintah git checkout -b.
```

### 4. Beritahu User
```
✅ Prompt [N] siap di: .agents/prompts/[N]-[slug].md

Langkah selanjutnya:
1. Buka file tersebut
2. Copy seluruh isinya
3. Paste ke chat @arsitek
```

---

## Larangan
- Jangan buat issue.md sendiri — itu tugas @arsitek
- Jangan skip membaca handoff terbaru
- Jangan gunakan nomor yang sudah dipakai
