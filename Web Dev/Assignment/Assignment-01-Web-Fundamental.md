# Assignment 01 — Web Fundamental

> 📅 **Periode:** 8–14 Oktober 2026 · ⏰ **Deadline:** 14 Oktober 2026, 23:59 WIB
> 📚 **Materi terkait:** [Lesson 01 — Web Fundamental](../Resource/Lesson-01-Web-Fundamental.md)

## Tujuan

Assignment ini menguji pemahaman Anda tentang cara kerja web — dari URL, DNS, hingga HTTP — melalui investigasi langsung menggunakan terminal dan Browser DevTools.

## Deliverables

```text
assignment-01/
├── answers.md          ← jawaban Task 1–4
├── screenshots/        ← screenshot pendukung Task 3–4
│   ├── network-overview.png
│   └── ...
└── how-the-web-works.png   ← diagram Task 5 (atau .pdf / .jpg)
```

---

## Task 1 — Conceptual Questions

Jawab dengan kata-kata Anda sendiri (2–5 kalimat per soal).

1. Apa perbedaan Internet dan World Wide Web? Sebutkan dua layanan internet yang **bukan** web.
2. Jelaskan arsitektur client–server menggunakan contoh aplikasi yang Anda pakai sehari-hari (misal: Instagram, e-learning kampus, marketplace).
3. Apa maksud HTTP bersifat **stateless**? Lalu bagaimana sebuah website bisa "mengingat" bahwa Anda sudah login?
4. Apa perbedaan status code `401` dan `403`? Serta `301` dan `302`?
5. Mengapa Anda **tidak boleh** memasukkan password pada website yang hanya menggunakan HTTP, terutama di WiFi publik?
6. Jelaskan perbedaan static dan dynamic website, masing-masing dengan dua contoh.

## Task 2 — URL Dissection

Uraikan setiap URL berikut menjadi **scheme, subdomain, domain, TLD, port, path, query parameters (key & value), dan fragment**. Tulis `-` jika bagian tersebut tidak ada. Sajikan dalam bentuk tabel.

1. `https://www.youtube.com/watch?v=dQw4w9WgXcQ&t=42s`
2. `http://localhost:3000/api/users/15?include=posts`
3. `https://developer.mozilla.org/en-US/docs/Web/HTTP/Status#successful_responses`
4. `https://shop.example.co.id:8443/products/search?q=keyboard+mechanical&sort=price&order=asc`
5. `ftp://files.example.org/pub/dataset.zip`

Pertanyaan tambahan:

6. Pada URL nomor 3, apakah bagian `#successful_responses` dikirim ke server? Bagaimana Anda membuktikannya menggunakan DevTools?
7. Mengapa URL nomor 1 dan nomor 4 tidak mencantumkan port yang sama, padahal keduanya menggunakan HTTPS?

## Task 3 — DNS & HTTP Investigation dengan `curl`

Jalankan command berikut, simpan output-nya di `answers.md` (dalam code block), lalu jawab pertanyaannya.

> Pengguna PowerShell: gunakan `curl.exe`.

1. **DNS**
   - Jalankan `nslookup` untuk 3 domain: `github.com`, `google.com`, dan satu website kampus/instansi pilihan Anda.
   - Apakah ada domain yang memiliki lebih dari satu IP address? Mengapa hal itu bisa terjadi?
2. **Status code & redirect**
   - Jalankan `curl -I http://github.com`. Status code apa yang didapat? Ke mana arah redirect-nya (lihat header `Location`)? Mengapa server melakukan redirect ini?
   - Jalankan `curl -I -L http://github.com`. Apa fungsi option `-L`?
   - Jalankan `curl -I https://github.com/halaman-yang-tidak-ada-123`. Status code apa yang didapat?
3. **Headers**
   - Jalankan `curl -I https://example.com` dan `curl -I https://www.wikipedia.org`.
   - Untuk masing-masing, catat: `content-type`, `server` (jika ada), `cache-control`, dan header lain yang menarik. Jelaskan arti 3 header yang Anda pilih.
4. **Request detail**
   - Jalankan `curl -v https://example.com -o /dev/null` (PowerShell: `curl.exe -v https://example.com -o NUL`).
   - Tandai bagian output yang menunjukkan: (a) IP address yang dihubungi, (b) TLS handshake, (c) request yang dikirim (`>`), (d) response header yang diterima (`<`).

## Task 4 — DevTools Network Analysis

Pilih **dua** website: satu website berita/marketplace populer **dan** satu website sederhana (misal <https://example.com> atau website dokumentasi). Untuk masing-masing:

1. Buka DevTools → **Network** → centang **Disable cache** → refresh.
2. Ambil screenshot ringkasan di bagian bawah panel (jumlah request, data transferred, load time).
3. Isi tabel berikut:

   | Metrik | Website A | Website B |
   | ------ | --------- | --------- |
   | Jumlah request | | |
   | Total transferred | | |
   | Waktu `Load` | | |
   | Jumlah request JS | | |
   | Jumlah request gambar | | |
   | Resource terbesar (nama & ukuran) | | |
   | Apakah ada request ke domain lain (third-party)? Sebutkan 2 | | |

4. Klik request dokumen utama (HTML). Catat **Request Method**, **Status Code**, **Remote Address**, dan **Protocol** (aktifkan kolom *Protocol* dengan klik kanan pada header tabel).
5. Bandingkan kedua website: mengapa jumlah request dan ukurannya bisa sangat berbeda? Apa dampaknya bagi pengguna dengan koneksi lambat?
6. Jalankan **Lighthouse** pada salah satu website dan catat skor Performance, Accessibility, Best Practices, dan SEO.

## Task 5 — Diagram "What Happens When You Type a URL"

Buat diagram (boleh digambar tangan lalu difoto, atau menggunakan [draw.io](https://app.diagrams.net/), [Excalidraw](https://excalidraw.com/), Figma, dsb.) yang menggambarkan seluruh proses dari mengetik `https://www.wikipedia.org` hingga halaman tampil.

Diagram minimal harus mencakup:

- [ ] Browser, DNS resolver, web server
- [ ] DNS lookup dan hasil IP address
- [ ] TCP connection & TLS handshake
- [ ] HTTP request (method + path) dan HTTP response (status code)
- [ ] Rendering: HTML → DOM, CSS → CSSOM, eksekusi JavaScript
- [ ] Request lanjutan untuk resource CSS/JS/gambar

---

## Bonus (Opsional)

1. Pada halaman web pertama Anda dari Guided Practice (Lesson 01), tambahkan sebuah tombol yang menampilkan `alert` ketika diklik. Buka DevTools → **Console** dan ketik `document.title = "Diubah dari Console"`. Jelaskan apa yang terjadi.
2. Cari tahu dan jelaskan secara singkat perbedaan **HTTP/1.1**, **HTTP/2**, dan **HTTP/3**.

## Rubrik Penilaian

| Komponen | Bobot |
| -------- | ----- |
| Task 1 — Conceptual questions | 20% |
| Task 2 — URL dissection | 15% |
| Task 3 — DNS & HTTP investigation | 25% |
| Task 4 — DevTools network analysis | 25% |
| Task 5 — Diagram | 15% |
| Bonus | +10% |
