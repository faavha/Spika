# Changelog

## 0.2.0 - 2026-11-14

**Ganti nama: InstaPulse → Spika.** Meta melarang aplikasi yang terhubung ke
API Instagram memakai "Insta", "Gram", atau "IG" di namanya, dan proyek ini
akan meluas ke TikTok, YouTube, dan Facebook. Spika = *spike* (lonjakan
outlier) + Spica (bintang paling terang di rasi Virgo).

- Plugin `instapulse` → `spika`; perintah sekarang `/plugin install spika@spika`.
- Semua skill `ig-*` → `spika-*` (`spika-reel`, `spika-plan`, `spika-viral`, dst.).
- Repo pindah ke `github.com/faavha/spika` (nama lama tetap di-redirect GitHub).
- Folder kerja `~/.claude/instagram/` **tidak berubah**, jadi voice.md, swipe.md,
  plan.md, dan log.md yang sudah ada tetap terbaca.

**Migrasi:** uninstall `instapulse`, lalu pasang ulang dengan perintah di
README. Kalau dulu menyalin manual, hapus folder `~/.claude/skills/ig-*` dan
salin `spika-*`.

## 0.1.1 - 2026-11-03

Ditemukan saat uji pertama InstaPulse membuat Reel dan caption untuk dirinya sendiri.

- **ig-human**: kutipan pendek dalam tanda petik ("Halo guys, aku mau bahas")
  tidak lagi diganti humanizer dan tidak dihitung sebagai klise, pola
  struktural, atau register kaku. Kutipan biasanya contoh, bukan suara penulis.
- **ig-human**: kalimat sangat pendek ("Gratis.", "Hasilnya kaku.") sekarang
  ikut dihitung di pemeriksaan VARIASI. Sebelumnya dibuang, sehingga naskah
  yang sengaja ritmis dinilai seragam.
- **ig-caption**: ajakan "Link GitHub-nya ada di bio" (ada kata di antara
  "link" dan "di bio") sekarang terbaca sebagai CTA.

## 0.1.0 - 2026-11-03

Rilis pertama: 13 skill, adaptasi bahasa Indonesia dari instagram-agent-skill.
