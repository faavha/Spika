---
name: spika-judul
description: >-
  Membuat judul dan konsep thumbnail YouTube berbahasa Indonesia yang diklik
  tanpa menipu: 8–10 kandidat judul dari pola outlier niche, skor per kandidat,
  3 konsep thumbnail yang saling melengkapi dengan judul, dan pasangan untuk
  diuji di fitur Test & Compare YouTube. Gunakan saat pengguna bilang "judul
  youtube", "bikinin judul", "thumbnail apa", "ide thumbnail", "judul yang
  clickbait tapi jujur", "CTR rendah", "ganti judul video ini", atau sebelum
  menulis naskah dengan /spika-video.
---

# spika-judul

Judul dan thumbnail adalah satu iklan dengan dua bagian. Judul memberi janji,
thumbnail memberi alasan percaya, dan keduanya **tidak boleh mengatakan hal yang
sama**. Di YouTube, video yang tidak diklik tidak ditonton, sebagus apa pun isinya.

Kerjakan skill ini **sebelum** `/spika-video`: naskah ditulis untuk menepati janji
judul.

## Sebelum menulis

1. **Satu kalimat janji.** Apa yang penonton dapat di akhir video. Tanpa ini,
   judul jadi tebakan.
2. **Bukti dari niche.** Kalau MCP Spika App tersedia:
   - `get_niche_outliers` (format sesuai: `video` atau `short`, 90 hari): kumpulkan
     10–20 judul outlier dan catat polanya: panjang, angka, pertanyaan, kata
     "diam-diam/ternyata/rahasia", sudut pandang orang pertama, nama/merek.
   - `get_topic_gaps`: kata yang **terbukti** atau **celah** boleh masuk judul;
     kata yang **jenuh** sebaiknya dihindari kecuali sudutnya baru.
   Tanpa MCP, minta pengguna menempelkan 10 judul outlier dari `/spika-viral`.
3. **Baca `~/.claude/instagram/voice.md`**: nada channel (serius, santai, misteri)
   menentukan seberapa jauh judul boleh "berteriak".

## Pola judul yang bekerja

| pola | contoh | kapan |
| --- | --- | --- |
| Rahasia/kontras | "Kenapa Orang Kaya Diam-Diam Menghindari Paylater" | status, uang, perilaku |
| Pertanyaan persis | "Habis Berapa Token Buat Bikin Aplikasi Ini?" | rasa penasaran yang bisa dijawab |
| Angka + hasil | "Gaji 4 Juta, Dana Darurat 12 Juta dalam 10 Bulan" | tutorial, keuangan, kebugaran |
| Ternyata | "Ternyata Nama Jakarta Dulu Bukan Batavia" | fakta, sejarah |
| Kesalahan | "3 Kesalahan Lari Pemula yang Bikin Lutut Sakit" | pemula, edukasi |
| Pengalaman | "Aku Coba Kerja Pakai AI Selama 30 Hari" | eksperimen, AI |
| Misteri | "Desa yang Hilang dari Peta Tahun 1982" | misteri, cerita |

Aturan teknis:
- **≤ 60 karakter** agar tidak terpotong di beranda HP; kata kunci utama di
  **5 kata pertama** (yang terbaca di hasil pencarian).
- Huruf Kapital Di Awal Kata boleh; HURUF BESAR SEMUA hanya untuk satu kata.
- Maksimal satu emoji, sebaiknya nol. Tanpa tagar di judul.
- Angka ditulis sebagai angka ("3", "12 Juta"), bukan kata.

## Alurnya

**1. Tulis 8–10 kandidat** dari minimal 4 pola berbeda di tabel. Sertakan sumber
pola untuk tiap kandidat ("pola dari outlier 15× Dea Afrizal").

**2. Skor setiap kandidat**, 1–5 per kriteria, dan tunjukkan tabelnya:

| kriteria | pertanyaan |
| --- | --- |
| **Jelas** | Dalam 2 detik, orang tahu videonya tentang apa? |
| **Penasaran** | Ada celah yang hanya bisa ditutup dengan menonton? |
| **Spesifik** | Ada angka, nama, waktu, atau objek konkret? |
| **Jujur** | Videonya benar-benar menepati ini di 30 detik pertama? (nilai 1–2 = gugur) |
| **Bukti niche** | Polanya muncul di outlier niche ini? Kata jenuh dikurangi. |

Hasil: urutkan, pilih **3 finalis** yang polanya berbeda.

**3. Tiga konsep thumbnail**, tiap konsep menjawab: apa satu hal yang dilihat mata
dalam 1 detik, dan apa yang **tidak** dikatakan judul.

```
KONSEP A  "objek + angka"
  fokus     tangan memegang HP dengan notifikasi tagihan merah
  teks      "+30%"  (maks 3 kata, besar, kontras)
  komposisi objek di kanan, teks di kiri, latar gelap polos
  pasangan  judul #2  → judul memberi alasan, thumbnail memberi angka
```

Untuk channel faceless: tanpa wajah, kekuatan ada di **satu objek besar**,
**kontras warna**, dan **maksimal 3 kata**. Hindari kolase banyak gambar, teks
kecil, dan elemen di pojok kanan bawah (tertutup durasi video). Ukuran 1280×720,
tetap terbaca saat dikecilkan ke lebar 168 piksel.

Jangan memakai wajah orang nyata, logo merek, atau karakter berhak cipta tanpa
izin. Prompt gambar AI boleh ditulis, tapi tandai bahwa hasilnya perlu diperiksa
(teks di gambar AI sering salah eja).

**4. Pasangan uji.** YouTube Studio punya **Test & Compare** untuk thumbnail.
Sarankan 2–3 thumbnail untuk diuji pada judul pemenang, dan catat hipotesisnya
("angka besar mengalahkan objek"). Setelah hasil keluar, catat di
`~/.claude/instagram/log.md` agar pelajaran itu tidak hilang.

**5. Cetak:**

```
JUDUL & THUMBNAIL
janji      3 biaya tersembunyi paylater + cara menghitungnya
pemenang   Kenapa Orang Kaya Diam-Diam Menghindari Paylater   (54 kar., skor 22/25)
cadangan   Cicilan 0% Ini Bikin Kamu Bayar 30% Lebih Mahal      (21/25)
           3 Biaya Paylater yang Tidak Ditulis di Aplikasi      (20/25)
uji        thumbnail A (+30%) vs B (struk panjang) pada judul pemenang
hindari    "gaji UMR" di judul: jenuh di niche ini (lift 0,6)
```

## Aturan

- **Jujur atau tidak sama sekali.** Judul yang tidak ditepati menaikkan klik dan
  menghancurkan retensi; YouTube menghitung keduanya. Clickbait yang dibayar
  lunas di 30 detik pertama itu boleh, yang tidak dibayar itu tidak.
- **Jangan menyalin judul outlier.** Ambil polanya, bukan kalimatnya.
- **Satu janji.** "X, Y, dan Z" di judul berarti tidak ada yang kuat.
- **Tanpa SARA, tuduhan, atau klaim kesehatan/keuangan yang menyesatkan.**
  "Pasti kaya", "sembuh total", "100% aman" adalah tanda bahaya, juga untuk
  kebijakan iklan YouTube.
