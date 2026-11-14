---
name: spika-video
description: >-
  Menulis naskah video YouTube panjang (5–20 menit) berbahasa Indonesia, termasuk
  untuk channel faceless dengan voiceover AI: struktur retensi (hook, janji isi,
  open loop, bab, re-hook), naskah narasi siap dibacakan, daftar visual per adegan,
  bab/chapters, dan perkiraan durasi per suku kata. Gunakan saat pengguna bilang
  "naskah youtube", "script video panjang", "bikin video 10 menit", "video faceless",
  "naskah voice over", "outline video", "bikin konten youtube soal X", atau punya
  topik dari /spika-viral dan ingin jadi video panjang.
---

# spika-video

Video panjang tidak gagal di menit ketujuh. Ia gagal di detik ketiga puluh,
saat penonton memutuskan apakah janji di judul akan ditepati. Skill ini menulis
naskah yang menahan orang di 30 detik pertama, lalu memberi alasan baru untuk
bertahan setiap dua sampai tiga menit.

Untuk video pendek (Shorts/Reels/TikTok di bawah 60 detik), pakai `/spika-reel`.
Untuk judul dan thumbnail, pakai `/spika-judul`, dan kerjakan judul **sebelum**
naskah: naskah harus menepati janji judul, bukan sebaliknya.

## Sebelum menulis

1. **Baca `~/.claude/instagram/voice.md`** kalau ada. Untuk channel faceless, isi
   juga bagian narator: siapa yang bicara (orang pertama "aku", narator netral,
   atau karakter), kecepatan bicara voiceover-nya (suku kata/detik), dan kata
   yang tidak boleh diucapkan. Voiceover AI membaca persis yang ditulis: tidak ada
   yang menyelamatkan kalimat kaku.
2. **Pegang judul dan janji.** Tanya atau pakai hasil `/spika-judul`: judul final,
   konsep thumbnail, dan **satu kalimat janji**: apa yang penonton tahu atau bisa
   lakukan di akhir video. Kalau janjinya tidak bisa ditulis dalam satu kalimat,
   topiknya terlalu lebar. Pecah jadi dua video.
3. **Ambil bukti.** Kalau MCP Spika App tersedia, `get_niche_outliers` (format
   `video`, 90 hari) dan `get_topic_gaps` untuk niche itu: lihat durasi, struktur
   judul, dan sudut video panjang yang meledak. Tanpa MCP, baca
   `~/.claude/instagram/swipe.md`. Bukti niche mengalahkan aturan di file ini.
4. **Kumpulkan isi yang benar.** Video edukasi/fakta hidup dari ketepatan. Minta
   atau cari sumber untuk setiap angka, tanggal, dan klaim. Tandai yang belum
   terverifikasi dengan `[CEK: ...]` di naskah. Jangan pernah mengarang data,
   kutipan, studi, atau pengalaman pribadi atas nama pengguna.

## Bentuknya

```
0:00 – 0:30   PEMBUKA      hook (≤ 3 dtk) → bukti cepat bahwa janji judul nyata →
                           peta singkat isi → satu open loop ("dan yang nomor tiga
                           justru kebalikan dari yang diajarkan orang")
0:30 – 1:30   KONTEKS      kenapa ini penting buat penonton sekarang, taruhannya
1:30 – akhir  BAB 1..N     tiap bab: klaim → bukti/contoh → arti buat penonton →
                           jembatan ke bab berikut
tiap 2–3 mnt  RE-HOOK      pertanyaan, kejutan, atau tutup satu open loop sambil
                           membuka yang baru
akhir         PEMBAYARAN   tepati janji judul secara eksplisit, satu ajakan
                           (tonton video X berikutnya > subscribe > komentar)
```

**Durasi**: pilih dari bukti niche, bukan dari "video panjang itu bagus". Patokan
awal: edukasi/tutorial 6–10 menit, cerita/misteri/sejarah 10–20 menit. Lebih
pendek dan padat mengalahkan lebih panjang dan encer.

## Alurnya

**1. Outline dulu, tunjukkan, tunggu "ya".** Judul, janji satu kalimat, 3–6 bab
dengan satu kalimat inti masing-masing, posisi open loop dan re-hook, perkiraan
durasi. Outline murah diubah; naskah 1.500 kata tidak.

**2. Tiga opsi pembuka.** Kalimat pertama ditulis dengan formula di
`../spika-reel/hooks.json` (formula berbeda untuk tiap opsi), lalu diskor:

```bash
python3 ../spika-reel/hookscore.py pembuka.txt --sps {laju voiceover}
```

Untuk video panjang, hook juga harus **cocok dengan judul dan thumbnail**: penonton
yang mengklik "Kenapa orang kaya diam-diam..." harus mendengar janji itu dalam
tiga detik, bukan salam pembuka.

**3. Tulis naskah narasi** per bab. Aturan untuk telinga, apalagi voiceover AI:
- Kalimat pendek. Satu gagasan per kalimat. Maksimal sekitar 20 kata.
- Angka ditulis seperti diucapkan ("dua koma tiga juta", "tahun sembilan belas
  empat puluh lima") di naskah voiceover; versi angka masuk ke teks layar.
- Tanpa singkatan yang dibaca aneh oleh TTS (dll, dsb, yg, krn). Tulis lengkap.
- Jeda dramatis ditulis eksplisit: `[jeda 1 dtk]`.
- Kata serapan dan nama asing yang sering salah ucap diberi ejaan bunyi di catatan
  produksi, bukan di naskah: `ASTRA → "as-tra"`.

**4. Daftar visual per adegan.** Faceless hidup dari visual yang berganti. Untuk
tiap 1–3 kalimat naskah, tulis satu baris visual:

```
[00:42] B-ROLL  layar aplikasi bank, saldo turun   | teks: "Rp2,3 jt/bulan"
[00:47] GRAFIK  batang 2019 vs 2026                 | sumber: BPS [CEK]
[00:53] STOK    orang menghitung uang di warung      | kata kunci stok: "counting money indonesia"
```

Jenis: `B-ROLL` (rekaman layar/milik sendiri), `STOK` (sertakan kata kunci
pencarian), `GRAFIK`, `TEKS`, `PETA`, `ILUSTRASI-AI` (tulis prompt singkat, dan
jangan untuk wajah orang nyata). Jangan memakai klip, musik, atau gambar milik
orang lain tanpa izin; tulis sumber yang aman.

**5. Hitung durasi.** Simpan naskah narasi saja (tanpa daftar visual) ke file:

```bash
python3 ../spika-reel/beats.py naskah.txt --sps {laju voiceover}
```

Pakai **total durasi** di baris judul; abaikan peringatan per-beat yang ditujukan
untuk Reels. Kalau lewat target lebih dari 15%, potong bab terlemah, jangan
mempercepat suara.

**6. Bab (chapters).** Daftar `0:00 Judul bab` untuk deskripsi YouTube, mulai dari
`0:00`, minimal tiga bab, masing-masing ≥ 10 detik. Judul bab ditulis sebagai
janji kecil, bukan label ("Kenapa gaji naik tapi tetap kurang", bukan "Bab 2").

**7. Humanize.** Jalankan naskah lewat `/spika-human` sebelum ditunjukkan. Untuk
voiceover AI ini wajib: "bahasa AI" yang dibacakan suara AI terdengar dua kali
lebih palsu, dan YouTube menolak monetisasi konten massal yang repetitif.

**8. Cetak paketnya:**

```
VIDEO SIAP
judul:      Kenapa Orang Kaya Diam-Diam Menghindari Paylater
janji:      di akhir, penonton tahu 3 biaya tersembunyi paylater dan cara menghitungnya
durasi:     ~8:40 (1.312 kata, 5,2 suku kata/dtk)
bab:        5 · open loop 2 · re-hook 3
pembuka:    #16 Pertanyaan Persis, skor 78 KUAT
visual:     41 adegan (12 b-roll, 18 stok, 7 grafik, 4 teks)
[CEK]:      3 klaim perlu sumber
humanizer:  skor manusia 84 LULUS
```

Lalu: naskah lengkap (blok kode), daftar visual, bab, dan catatan produksi
(pengucapan, musik latar yang aman, ide thumbnail dari `/spika-judul`).

**9. Jangan pernah mempublikasikan.** Saat pengguna bilang "ya", catat ke
`~/.claude/instagram/log.md`: tanggal, judul, formula pembuka, durasi, sehingga
`/spika-audit` bisa membandingkan rencana dengan hasil. Kalau MCP Spika tersedia
dan ada rencana minggu ini (`get_content_plans`), sebutkan slot mana yang diisi.

## Aturan yang membuat beda

- **Satu janji per video.** Semua bab melayani janji itu. Bab yang menarik tapi
  tidak melayani janji adalah video berikutnya.
- **Bukti sebelum klaim besar.** Tunjukkan angka, tangkapan layar, atau contoh,
  lalu simpulkan. Penonton faceless tidak punya wajah untuk dipercaya; mereka
  hanya punya buktimu.
- **Re-hook bukan clickbait.** Setiap "tapi tunggu" harus dibayar di menit itu
  juga atau di bab yang disebut.
- **Tanpa pembuka kosong.** Tidak ada "Halo semuanya, selamat datang kembali di
  channel...", intro logo 10 detik, atau "sebelum mulai jangan lupa subscribe".
  Ajakan subscribe paling cepat setelah janji pertama dibayar.
- **Fakta sensitif dengan hati-hati.** Kesehatan, hukum, keuangan: edukasi, bukan
  saran pribadi; sebut sumber. Misteri dan sejarah: bedakan fakta, legenda, dan
  dugaan dengan kata yang jelas ("menurut cerita warga", "belum ada bukti").
  Hindari SARA dan tuduhan ke orang yang bisa dikenali (UU ITE).
- **AI di produksi itu boleh; AI tanpa manusia tidak.** Riset, sudut pandang,
  pemilihan bukti, dan suntingan harus terasa dari manusia. Itu yang membedakan
  channel yang dimonetisasi dari channel yang ditandai "konten massal".

## Contoh

```
/spika-video jebakan paylater buat pekerja gaji UMR, 8 menit, faceless
```

```
OUTLINE (menunggu persetujuan)
judul   Kenapa Orang Kaya Diam-Diam Menghindari Paylater
janji   3 biaya tersembunyi paylater + cara menghitung bunga efektifnya sendiri
bukti   niche Keuangan: "diam-diam" & "strategi" terbukti (lift 3×), "gaji UMR" jenuh
        → sudut: bukan "atur gaji", tapi "yang tidak dikatakan aplikasi"

0:00  pembuka   #16 "Kenapa cicilan nol persen bisa bikin kamu bayar 30% lebih mahal?"
               open loop: biaya ketiga yang tidak tertulis di aplikasi
0:35  konteks   pengguna paylater muda naik; denda dan skor kredit (SLIK) [CEK sumber OJK]
1:40  bab 1     biaya layanan yang disebut "bukan bunga"
3:20  bab 2     denda harian dan efek ke SLIK         re-hook: "ini yang bikin KPR ditolak"
5:10  bab 3     biaya ketiga: harga barang dinaikkan   (tutup open loop)
6:40  hitung    rumus bunga efektif dengan kalkulator HP
7:50  bayar     ringkas 3 biaya, ajakan: video "dana darurat dari gaji UMR"

Balas "ya" untuk ditulis lengkap, atau ubah bab yang mana.
```
