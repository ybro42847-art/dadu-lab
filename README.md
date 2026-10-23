# DaduLab — Dadu Online + Firebase Dashboard

Aplikasi Next.js mobile-friendly yang meniru pengalaman dadu online pada video, dengan tab dashboard Firebase untuk mengelola dokumen `users`.

## Menjalankan lokal
1. Install Node.js 20 atau lebih baru.
2. Ekstrak ZIP, buka folder project lalu jalankan:
   ```bash
   npm install
   ```
3. Salin `.env.local.example` menjadi `.env.local` (atau isi nilainya manual), lalu verifikasi konfigurasi di Firebase Console.
4. Jalankan `npm run dev`, lalu buka alamat lokal yang ditampilkan.

Tanpa konfigurasi Firebase, permainan dadu tetap berjalan dalam mode demo. Dashboard akan meminta konfigurasi Firebase.

## Deploy ke Vercel
1. Push folder project ke repository GitHub.
2. Import repository di Vercel.
3. Tambahkan semua variabel `NEXT_PUBLIC_FIREBASE_*` dari `.env.local.example` ke Vercel Project Settings → Environment Variables.
4. Deploy / redeploy.

## Struktur Firestore yang didukung
Koleksi `users`, dokumen misalnya `kaiz`:
```json
{
  "rules": "20-25-30",
  "index": 0,
  "nowpola": 20,
  "nextpola": 25,
  "expiry": "2026-12-31"
}
```
Dashboard memuat field tersebut dan menyimpan perubahan menggunakan `setDoc(..., {merge:true})`. Field tambahan yang sudah ada tidak dihapus.

## Penting — keamanan
- Jangan masukkan service-account private key ke frontend atau ke variabel `NEXT_PUBLIC_*`.
- Aktifkan Firebase Authentication dan batasi Firestore Rules agar hanya admin terautentikasi yang dapat menulis.
- Contoh ini belum menambahkan alur login admin; jangan membuka hak tulis publik. Implementasikan autentikasi/otorisasi admin sebelum digunakan untuk data sungguhan.
- Roll dadu memakai generator acak browser untuk permainan/demo, bukan untuk kebutuhan kriptografi atau taruhan.
