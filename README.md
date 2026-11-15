# Latihan TKA Kelas 9 (V2)

Aplikasi web latihan **Tes Kemampuan Akademik (TKA) untuk siswa SMP/MTs kelas 9** —
produk Toko Aplikasi Edukasi AwwanMahda. Model 3 (Tryout Bertahap), Fase 1.

Aplikasi ini adalah **latihan simulasi**: soal-soal disusun sendiri mengikuti
kisi-kisi resmi TKA SMP (Perkaban BSKAP 047/H/AN/2025), bukan soal resmi, dan
tidak mengklaim format/jumlah soal/waktu ujian resmi.

## Isi V2

- **Dua mapel kelas 9:** Bahasa Indonesia & Matematika.
- **Bank soal: 70 soal asli** (7 topik × 10 soal), semua dengan pembahasan.
  - Matematika (40 soal): Bilangan & Operasi (gratis), Aljabar (versi penuh),
    Geometri & Pengukuran (versi penuh), Statistika & Peluang (versi penuh).
  - Bahasa Indonesia (30 soal): Membaca Teks Informasi (gratis),
    Membaca Teks Sastra & Kebahasaan (versi penuh), Menyunting & Menulis (versi penuh).
  - Seluruh topik sudah berisi soal — tidak ada lagi topik berstatus "Segera".
- **Latihan per topik:** 10 soal, umpan balik + pembahasan langsung per soal,
  tanpa batas waktu (penunjuk waktu berjalan), bisa berhenti di tengah dan
  **dilanjutkan** (resume dari localStorage).
- **Tryout Mini (gratis):** 10 soal campuran (5 MTK + 5 BI), 15 menit, navigasi
  antar soal + daftar nomor, tandai ragu-ragu, konfirmasi sebelum kumpul,
  waktu habis terkumpul otomatis.
- **Tryout Utuh (versi penuh, SUDAH AKTIF):** 50 soal (25 per mapel, dipilih dari
  bank soal), 100 menit, pola tryout yang sama seperti Tryout Mini. Syarat
  otomatisnya — bank soal tiap mapel ≥ 25 soal — kini terpenuhi
  (Matematika 40, Bahasa Indonesia 30).
- **Hasil:** skor 0–100, benar/salah/kosong, analisis per topik (sesi ini +
  kumulatif), review semua soal dengan pembahasan.
- **Progres lokal tanpa akun** (localStorage): skor terbaik & riwayat per topik,
  status buka kunci, sesi latihan yang belum selesai, tombol reset progres.
- **Kode akses (Model B, pola Calistung Ceria):** versi demo membuka Tryout Mini
  + topik pertama tiap mapel. Aplikasi **hanya menyimpan hash SHA-256** kode
  (daftar `KODE_HASH` di `index.html`); plaintext kode hanya dipegang admin.
- **PWA dasar:** manifest + service worker (cache-first, cache
  `latihan-tka-kelas9-v2`), ikon, dapat dibuka offline setelah muat pertama.
  Tanpa dependensi CDN — satu `index.html` vanilla JS.

## Menjalankan lokal

```bash
cd ~/workspace/projects/latihan-tka-kelas9
python3 -m http.server 8765
# buka http://localhost:8765/
```

## Catatan pengembangan

- Naikkan nama cache di `sw.js` setiap kali isi berubah.
- Tambah soal: tambahkan objek ke array `BANK` di `index.html`
  (`{id, topik, stimulus?, soal, opsi:[4], kunci, pembahasan, level}`).
  Tryout Utuh aktif otomatis saat tiap mapel mencapai 25 soal.
- Tambah kode akses: hitung SHA-256 dari kode (format `TKA9-XXXXXX`),
  tambahkan hash-nya ke `KODE_HASH`. Jangan pernah menulis plaintext di kode.
- Rilis (GitHub/Vercel) adalah langkah terpisah di luar V2 ini.
