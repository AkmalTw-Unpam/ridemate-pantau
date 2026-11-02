# ridemate-pantau — pengalih alamat

Repo ini **sudah tidak berisi halaman sungguhan lagi**. Kelima halamannya
pindah ke [`ridemate-web`](https://github.com/AkmalTw-Unpam/ridemate-web)
dan sekarang tayang di `ridemate.my.id`.

Yang tersisa di sini lima halaman pengalih, satu per alamat lama.

| Alamat lama | Dialihkan ke |
|---|---|
| `pantau.ridemate.my.id/` | `ridemate.my.id/pantau/` |
| `pantau.ridemate.my.id/privasi.html` | `ridemate.my.id/privasi.html` |
| `pantau.ridemate.my.id/akun-aktif.html` | `ridemate.my.id/akun-aktif.html` |
| `pantau.ridemate.my.id/ganti-password.html` | `ridemate.my.id/ganti-password.html` |
| `pantau.ridemate.my.id/hapus-akun.html` | `ridemate.my.id/hapus-akun.html` |

---

## Jangan hapus repo ini

Tiga alamat di atas sudah tertulis di tempat yang tidak bisa ditarik kembali:

- **Email konfirmasi dan reset password** yang sudah terkirim ke pengguna
- **APK RideMate yang sudah beredar**, yang `PANTAU_URL`-nya masih menunjuk
  ke sini
- **Tautan pantau** yang sudah dibagikan seseorang ke keluarganya

Menghapus repo ini berarti orang yang menekan tautan di emailnya mendarat di
halaman kosong, dan tidak akan pernah tahu kenapa. Biaya menyimpannya nol.

Repo ini boleh dihapus kalau suatu saat ketiganya sudah pasti habis: semua
pengguna memakai APK yang `PANTAU_URL`-nya sudah menunjuk ke alamat baru,
dan email lama sudah lewat masa berlakunya. Sampai saat itu, biarkan.

---

## Kenapa pengalihannya pakai JavaScript, bukan hanya meta refresh

Supabase mengirim token hasil autentikasi **di belakang tanda pagar**:

```
/ganti-password.html#access_token=eyJhbGci...
```

Bagian di belakang pagar tidak pernah dikirim ke server, dan
`<meta http-equiv="refresh">` membuangnya. Orang yang menekan tautan reset
password akan mendarat di alamat baru tanpa token, lalu diberi tahu
"tautannya tidak berlaku lagi" — padahal tautannya baik-baik saja.

Jadi tiap halaman di sini membawa `location.search` **dan** `location.hash`
serta ke alamat baru. Meta refresh tetap dipasang sebagai cadangan untuk
peramban tanpa JavaScript, dengan tombol manual yang terlihat.

`location.replace`, bukan `location.href`: alamat lama tidak tertinggal di
riwayat peramban, jadi tombol Mundur tidak memantulkan orang kembali ke
pengalih ini.

---

## Yang harus tetap ada

- **`CNAME`** — berisi `pantau.ridemate.my.id`. Berkas ini yang membuat
  alamatnya hidup. Kalau terhapus, seluruh pengalihan di atas mati sekaligus.
- Kelima berkas `.html` di akar repo.

## Yang tidak boleh masuk ke sini

Tidak ada kunci apa pun. Halaman pengalih tidak bicara ke Supabase, tidak
butuh kunci anon, dan tidak boleh dibuat butuh.
