# RideMate — halaman pendukung

Lima halaman statis yang dipakai aplikasi Android **RideMate**, disajikan
GitHub Pages di `pantau.ridemate.my.id`.

Repo ini **bukan** situs resmi RideMate. Situsnya ada di
[`ridemate-web`](https://github.com/AkmalTw-Unpam/ridemate-web) dan tayang di
`ridemate.my.id`.

Tidak ada build di sini. Lima berkas HTML berdiri sendiri, tanpa npm, tanpa
kerangka kerja apa pun — diunggah apa adanya dan langsung tayang. Itu
disengaja: halaman-halaman ini harus tetap hidup meski seluruh perkakas di
sekitarnya berubah.

---

## Isinya

| Berkas | Alamat | Dipakai untuk |
|---|---|---|
| `index.html` | `/?t=<token>` | Memantau perjalanan rider secara langsung di peta |
| `privasi.html` | `/privasi.html` | Kebijakan privasi — wajib untuk Google Play |
| `ganti-password.html` | `/ganti-password.html` | Tujuan tautan "Lupa password?" dari email |
| `akun-aktif.html` | `/akun-aktif.html` | Tujuan tautan konfirmasi email saat mendaftar |
| `hapus-akun.html` | `/hapus-akun.html` | Menghapus akun tanpa perlu memasang aplikasinya |

---

## Kenapa alamatnya tidak boleh berubah

Tiga dari lima halaman ini **sudah tertulis di email yang terlanjur
terkirim** ke pengguna, dan di dalam APK yang sudah beredar. Mengganti nama
berkas atau memindahkannya memutus tautan yang sudah ada di kotak masuk
orang — dan mereka tidak akan pernah tahu kenapa.

Kalau suatu saat harus berpindah alamat, urutannya: pasang di alamat baru →
pastikan alamat lama masih hidup atau dialihkan → baru ubah `PANTAU_URL` di
aplikasi dan terbitkan APK baru. Jangan dibalik.

---

## Soal kunci di dalam berkas

`ganti-password.html` dan `hapus-akun.html` memuat **kunci anon Supabase**.
Itu disengaja dan aman: kunci anon memang dirancang publik dan sudah ikut
tertanam di dalam APK RideMate. Yang menjaga data tetap aman adalah Row
Level Security di database, bukan kerahasiaan kunci ini.

Yang **tidak boleh** ada di repo ini, selamanya:

- Service role key Supabase
- Kunci akun layanan Firebase
- App Certificate Agora

Ketiganya tinggal di Supabase Secrets dan di dalam Edge Function, dan tidak
pernah ikut ke peramban siapa pun.

`index.html` sendiri tidak memuat kunci apa pun. Ia hanya tahu alamat Edge
Function `pantau` dan token yang ada di URL.

---

## Dua hal yang sudah dipikirkan, jangan dicabut

**`index.html` memakai `noindex, nofollow` dan `referrer: no-referrer`.**
Alamat halaman pantau mengandung token perjalanan seseorang. Tanpa
`noindex`, tautan itu bisa muncul di hasil pencarian Google; tanpa
`no-referrer`, alamat lengkapnya ikut terkirim ke server penyedia peta
setiap kali petanya dimuat.

**Spanduk darurat di `index.html` tidak bisa ditutup.** Tanda bahaya yang
bisa disingkirkan akan tersingkir tanpa dibaca.

---

## Cara mengubah

Lewat tampilan GitHub langsung — buka berkasnya, klik ikon pensil, simpan.
Perubahan tayang satu sampai dua menit kemudian.

Untuk perubahan yang menyentuh banyak berkas sekaligus, tekan `.` di halaman
repo ini untuk membuka editor web, atau buka
`github.dev/AkmalTw-Unpam/ridemate-pantau`.
