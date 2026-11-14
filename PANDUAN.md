# Panduan Pakai Spika

Panduan ini untuk kreator, UMKM, admin akun kampus/instansi, atau siapa pun
yang mengelola Instagram berbahasa Indonesia dan memakai Claude.

Intinya: **kamu tidak perlu menghafal perintah.** Setelah terpasang, cukup
minta ke Claude dengan bahasa biasa ("bikinin naskah reels soal X", "balasin
komen-komen ini"), dan Claude akan memakai skill yang cocok. Perintah `/spika-...`
hanya jalan pintas kalau kamu mau memilih skill-nya sendiri.

Spika **tidak pernah memposting apa pun.** Ia menulis, menilai, dan
merencanakan. Kamu yang memposting.

---

## 1. Pasang

### Di Claude Code (terminal)

```
/plugin marketplace add faavha/spika
/plugin install spika@spika
```

Skill akan muncul sebagai `spika:spika-reel`, `spika:spika-caption`, dan
seterusnya.

### Di aplikasi Claude (desktop / web)

Unduh file `spika.plugin` dari halaman
[Releases](https://github.com/faavha/spika/releases) (atau minta Claude
mengemasnya dari repo ini), lalu unggah ke percakapan dan pasang dari kartu
plugin yang muncul.

### Manual (salin skill saja)

```bash
git clone https://github.com/faavha/spika.git
cp -r spika/skills/spika-* ~/.claude/skills/
```

Salin semua folder `spika-*` sekaligus. `spika-viral` memakai script dari `spika-reel`.

**Syarat:** Python 3 untuk script penilai (tanpa library tambahan, tanpa internet).
Tanpa Python, skill tetap jalan sebagai panduan menulis, tapi skor otomatisnya hilang.

---

## 2. Langkah pertama: profil suara (10 menit, sekali saja)

Semua skill membaca file `~/.claude/instagram/voice.md`: siapa kamu, bicara ke
siapa, pakai "aku/kamu" atau "gue/lo", seberapa sering campur Inggris, kata yang
tidak pernah kamu ucapkan, dan angka yang boleh dipakai.

Cara paling gampang, bilang ke Claude:

> Ini tiga caption Reels-ku. Tulisin voice.md-ku dari sini.
> [tempel tiga caption atau transkrip]

Atau isi manual dari template `skills/spika-reel/voice-template.md`.

**Kalibrasi laju bicara (opsional, sangat disarankan).** Rekam dirimu membaca
satu naskah dengan tempo biasa, catat detiknya, lalu:

> Aku baca naskah ini 27 detik. Kalibrasi laju bicaraku.

Hasilnya (misalnya 6,2 suku kata/detik) disimpan di voice.md dan dipakai untuk
semua hitungan durasi Reels.

---

## 3. Alur kerja mingguan yang disarankan

```
Sebulan sekali   /spika-viral    riset apa yang jalan di niche-mu  -> swipe.md
                 /spika-audit    bedah 30 post terakhir           -> apa yang distop/diperbanyak
Seminggu sekali  /spika-plan     rencana 4-5 post + story + daftar engagement -> plan.md
Tiap konten      /spika-reel atau /spika-carousel  ->  /spika-caption  ->  (otomatis lewat /spika-human)
Tiap hari        /spika-story    3-5 frame
                 /spika-comment  20 menit engagement sebelum posting
                 /spika-reply    balas komen di jam pertama
Saat perlu       /spika-dm, /spika-profile, /spika-repurpose
```

Skill-skill ini saling membaca file di `~/.claude/instagram/`:

| file | ditulis oleh | dibaca oleh |
| --- | --- | --- |
| `voice.md` | kamu / `/spika-reel` | semua |
| `swipe.md` | `/spika-viral` | `/spika-reel`, `/spika-plan` |
| `plan.md` | `/spika-plan` | skill lain |
| `log.md` | `/spika-reel`, `/spika-comment` | `/spika-audit`, `/spika-plan` |

Makin sering dipakai, makin banyak yang berdasarkan bukti dari akunmu sendiri,
bukan aturan umum.

---

## 4. Contoh permintaan per skill

| skill | contoh yang bisa kamu ketik |
| --- | --- |
| `/spika-reel` | "Bikinin reels: aku hemat Rp400 ribu sebulan setelah pasang panel surya 1kW di rumah." |
| `/spika-caption` | "Caption buat reels tadi. Kata pencarian: panel surya rumah, hemat listrik." |
| `/spika-carousel` | "Jadikan carousel: rincian modal jualan sambal Rp750 ribu." |
| `/spika-story` | "Story hari ini, aku mau jualan PO kue lebaran tanpa bikin post." |
| `/spika-profile` | "Nilai profil IG-ku" + screenshot bagian atas profil |
| `/spika-plan` | "Rencanain minggu depan. Minggu ini aku dapat 3 klien baru dan 1 yang batal." |
| `/spika-viral` | "Cari reels yang lagi jalan di niche kuliner rumahan Solo." |
| `/spika-human` | "Bikin caption ini nggak kayak ChatGPT." + tempel teks |
| `/spika-comment` | "Komenin 5 post ini buat engagement hari ini." + tempel |
| `/spika-reply` | "Balasin komen-komen ini." + screenshot kolom komen |
| `/spika-dm` | "Dia komen MAU di reels-ku, kirim apa?" |
| `/spika-repurpose` | "Ini transkrip live IG 40 menit, potong jadi konten seminggu." |
| `/spika-audit` | "Ini insights 20 reels terakhir, apa yang jalan?" + screenshot |

---

## 5. Membaca hasil penilaian

**Skor hook** (`hookscore.py`), 0-100:

- **KUAT** (70+, tidak ada sifat di bawah 55): rekam.
- **OKE** (50-69): bisa, tapi perbaiki sifat terlemah yang disebut.
- **LEMAH** (<50): belum ada hook. Ganti formula, bukan dipoles.
- **fatal**: sapaan, "di video kali ini", "jangan scroll", hashtag atau emoji di
  hook. Masing-masing memotong 15 poin.

**Beat sheet** (`beats.py`): hook harus selesai dalam 3,5 detik, satu beat
maksimal 4 detik, dan kalimat terakhir sebaiknya mengulang satu kata dari hook
(loop).

**Cek caption** (`caption.py`): SIAP / TINJAU / PERBAIKI. Kotak di atas
menunjukkan persis apa yang terlihat sebelum "... selengkapnya".

**Panel deteksi AI** (`detect.py`): LULUS / TINJAU / TERDETEKSI. Pemeriksaan
terlemah disebut di bawah, perbaiki itu dulu. Untuk akun formal (kampus,
instansi) pakai register formal supaya "Anda" tidak dihitung sebagai kesalahan.

Semua skor ini heuristik dan **belum dikalibrasi pada data Indonesia**. Pakai
sebagai checklist. Grafik retensi di Insights akunmu selalu lebih benar.

---

## 6. Menjalankan script langsung (tanpa Claude)

Semua script bisa dipakai sendiri dari terminal:

```bash
cd skills/spika-reel
python3 hookscore.py --hook "Rp18 juta hilang gara-gara satu pasal di kontrak."
python3 beats.py naskah.txt --target 30 --sps 6.2

cd ../spika-caption
python3 caption.py caption.txt --keywords "foto produk,jualan online"

cd ../spika-human
python3 humanize.py draf.txt -o bersih.txt --report
python3 detect.py draf.txt bersih.txt
python3 detect.py draf.txt --register formal

cd ../spika-viral
python3 swipe.py tangkapan.tsv --out ~/.claude/instagram/swipe.md
```

Tambahkan `--json` ke script mana pun untuk output yang bisa diolah program lain.

---

## 7. Menyesuaikan

- **Kata yang memang gayamu ditandai sebagai "bahasa AI"?** Hapus entrinya di
  `skills/spika-human/slop.json`.
- **Menemukan pola hook baru di `/spika-viral`?** Tambahkan formula ke
  `skills/spika-reel/hooks.json` (id, template, contoh, regex `match`).
- **Rubrik profil kurang cocok untuk niche-mu?** Ubah bobot di
  `skills/spika-profile/rubric.json` (total harus tetap 100).

Kontribusi lewat pull request sangat diterima, terutama contoh caption dan hook
asli bahasa Indonesia untuk mengkalibrasi skor.

---

## 8. Pertanyaan umum

**Apakah Spika login ke Instagram atau memposting otomatis?**
Tidak. Tidak ada login, tidak ada API Instagram, tidak ada posting, follow,
like, atau DM otomatis. Otomatisasi seperti itu melanggar Ketentuan Instagram
dan bisa membuat akun dibatasi.

**Data saya dikirim ke mana?**
Script berjalan lokal di komputermu. Teks yang kamu tempel ke Claude diproses
seperti percakapan Claude biasa.

**Bisa untuk TikTok atau YouTube Shorts?**
Naskah, hook, beat sheet, dan humanizer bekerja untuk video pendek mana pun.
Batas caption, hashtag, dan fitur story spesifik Instagram.

**Bahasa daerah?**
Tulis di voice.md kata-kata daerah yang kamu pakai. Script menghitung suku
kata dengan baik untuk bahasa berejaan Latin seperti Jawa dan Sunda, tapi
kamus "bahasa AI"-nya baru bahasa Indonesia dan Inggris.
