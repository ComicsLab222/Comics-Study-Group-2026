# Lesson 01 — Web Fundamental

> 📅 **Self-study 1:** 8–14 Oktober 2026 · 💬 Dibahas pada **Meeting 1 (22 Oktober)**

## Learning Objectives

Setelah menyelesaikan materi ini, peserta mampu:

- Membedakan **Internet** dan **World Wide Web**.
- Menjelaskan arsitektur **client–server** dan peran browser, web server, serta database.
- Menguraikan bagian-bagian sebuah **URL** dan menjelaskan peran **DNS** dan **IP address**.
- Menjelaskan alur **HTTP request–response**, termasuk method, status code, dan header.
- Menjelaskan perbedaan **HTTP** dan **HTTPS**.
- Menjelaskan apa yang terjadi sejak URL diketik hingga halaman tampil di browser.
- Membedakan peran **HTML, CSS, dan JavaScript**, serta **frontend vs backend** dan **static vs dynamic website**.
- Menggunakan **Browser DevTools** dan `curl` untuk menginspeksi komunikasi web.

## Prerequisites

**Materi prasyarat**

- Tidak ada. Lesson ini adalah titik awal track Web Development.

**Tools yang diperlukan**

- Browser modern: **Google Chrome**, **Microsoft Edge**, atau **Firefox** (untuk DevTools).
- Code editor: **[Visual Studio Code](https://code.visualstudio.com/)** + extension *Live Server* (disarankan).
- Terminal: PowerShell / Command Prompt (Windows), Terminal (macOS/Linux). `curl` dan `nslookup` sudah tersedia di Windows 10/11, macOS, dan Linux.

## Learning Materials

### 1. Internet vs Web

| | Internet | World Wide Web (WWW) |
| - | -------- | -------------------- |
| Apa itu | **Jaringan** global yang menghubungkan jutaan komputer | **Layanan** di atas internet berupa dokumen yang saling terhubung (hyperlink) |
| Analogi | Jalan raya | Toko-toko dan rambu yang ada di sepanjang jalan |
| Protokol | TCP/IP | HTTP/HTTPS |
| Layanan lain | Email (SMTP), file transfer (FTP), SSH, game online | — |

Web diciptakan oleh **Tim Berners-Lee** di CERN pada 1989 dengan tiga komponen inti: **HTML** (format dokumen), **URL** (alamat), dan **HTTP** (protokol transfer).

### 2. Arsitektur Client–Server

```text
┌────────────┐      HTTP Request       ┌────────────┐      Query      ┌────────────┐
│   Client   │ ──────────────────────► │   Server   │ ──────────────► │  Database  │
│ (Browser)  │                         │ (Web/App)  │                 │            │
│            │ ◄────────────────────── │            │ ◄────────────── │            │
└────────────┘     HTTP Response       └────────────┘      Data       └────────────┘
   Frontend          (HTML/JSON)           Backend
```

- **Client** — pihak yang meminta (request) resource. Biasanya browser, tetapi bisa juga aplikasi mobile atau `curl`.
- **Server** — komputer yang selalu menyala, menunggu request, dan mengirimkan response.
- **Database** — tempat data disimpan secara permanen (akan dipelajari pada topik Database, 20–25 Nov).

### 3. Anatomi URL

```text
https://www.example.com:443/blog/articles?page=2&sort=new#comments
└─┬─┘   └──────┬──────┘└┬┘└─────┬──────┘└───────┬───────┘└───┬───┘
scheme       host     port    path           query       fragment
```

| Bagian | Fungsi |
| ------ | ------ |
| **scheme** | protokol yang digunakan (`http`, `https`) |
| **host** | nama domain server (`www` = subdomain, `example` = domain, `.com` = TLD) |
| **port** | "pintu" di server; default `80` untuk HTTP, `443` untuk HTTPS (biasanya tidak ditulis) |
| **path** | lokasi resource di server |
| **query** | parameter tambahan berupa `key=value`, dipisah `&` |
| **fragment** | menunjuk bagian tertentu di halaman; **tidak dikirim** ke server |

### 4. IP Address & DNS

Komputer di internet berkomunikasi menggunakan **IP address** (contoh IPv4: `142.250.4.100`, IPv6: `2404:6800:4003::200e`). Karena angka sulit diingat, kita menggunakan nama domain. **DNS (Domain Name System)** adalah "buku telepon" internet yang menerjemahkan nama domain menjadi IP address.

```text
Browser: "IP-nya google.com berapa?"
   │
   ├─► Cache browser / OS  ──(tidak ada)──►  DNS Resolver (ISP / 8.8.8.8 / 1.1.1.1)
   │                                              │
   │                               Root server → TLD server (.com) → Authoritative server
   │                                              │
   ◄──────────────────── "142.250.4.100" ─────────┘
```

### 5. HTTP: Bahasa Komunikasi Web

**HTTP (HyperText Transfer Protocol)** adalah protokol berbasis teks dengan pola **request → response**. HTTP bersifat **stateless**: setiap request berdiri sendiri; server tidak "mengingat" request sebelumnya (karena itu ada cookies & session).

**Contoh HTTP request:**

```http
GET /blog/articles?page=2 HTTP/1.1
Host: www.example.com
User-Agent: Mozilla/5.0
Accept: text/html
```

**Contoh HTTP response:**

```http
HTTP/1.1 200 OK
Content-Type: text/html; charset=UTF-8
Content-Length: 1256
Cache-Control: max-age=3600

<!DOCTYPE html>
<html> ... </html>
```

**HTTP methods** (dibahas mendalam di REST API):

| Method | Fungsi | Contoh |
| ------ | ------ | ------ |
| `GET` | mengambil data | membuka halaman, melihat daftar produk |
| `POST` | mengirim/membuat data baru | submit form registrasi |
| `PUT` / `PATCH` | memperbarui data (seluruh / sebagian) | edit profil |
| `DELETE` | menghapus data | hapus komentar |

**HTTP status codes:**

| Kelompok | Arti | Contoh |
| -------- | ---- | ------ |
| `1xx` | Informational | `101 Switching Protocols` |
| `2xx` | **Sukses** | `200 OK`, `201 Created`, `204 No Content` |
| `3xx` | **Redirect** | `301 Moved Permanently`, `302 Found`, `304 Not Modified` |
| `4xx` | **Kesalahan client** | `400 Bad Request`, `401 Unauthorized`, `403 Forbidden`, `404 Not Found` |
| `5xx` | **Kesalahan server** | `500 Internal Server Error`, `502 Bad Gateway`, `503 Service Unavailable` |

### 6. HTTP vs HTTPS

**HTTPS = HTTP + TLS (enkripsi)**. Dengan HTTPS:

- **Confidentiality** — data terenkripsi; pihak ketiga (misal di WiFi publik) tidak bisa membaca password Anda.
- **Integrity** — data tidak bisa dimodifikasi di tengah jalan.
- **Authentication** — sertifikat digital membuktikan bahwa server memang milik domain tersebut.

> [!IMPORTANT]
> Ikon gembok 🔒 di browser berarti koneksi terenkripsi, **bukan** jaminan bahwa website tersebut aman/terpercaya. Situs phishing pun bisa menggunakan HTTPS.

### 7. Apa yang Terjadi Saat Anda Mengetik URL?

1. **Parsing URL** — browser memisahkan scheme, host, path.
2. **DNS lookup** — mencari IP address dari host.
3. **TCP connection** — membuka koneksi ke IP:port (three-way handshake).
4. **TLS handshake** — negosiasi enkripsi (khusus HTTPS).
5. **HTTP request** — browser mengirim `GET /path`.
6. **Server processing** — server membaca file statis atau menjalankan kode backend (bisa mengakses database).
7. **HTTP response** — server mengirim status code, header, dan body (HTML).
8. **Rendering** — browser mem-parsing HTML → membangun **DOM**, mem-parsing CSS → **CSSOM**, menjalankan JavaScript, lalu melakukan *layout* dan *paint*. Setiap resource tambahan (CSS, JS, gambar) memicu request baru.

### 8. HTML, CSS, JavaScript

| Teknologi | Peran | Analogi Rumah |
| --------- | ----- | ------------- |
| **HTML** | Struktur & konten | Kerangka, dinding, ruangan |
| **CSS** | Tampilan & layout | Cat, furnitur, dekorasi |
| **JavaScript** | Perilaku & interaktivitas | Listrik, saklar, pintu otomatis |

```html
<!-- HTML -->
<button id="greet">Klik saya</button>

<style>
  /* CSS */
  #greet { background: #6c5ce7; color: white; padding: 8px 16px; border-radius: 8px; }
</style>

<script>
  // JavaScript
  document.getElementById("greet").addEventListener("click", () => alert("Halo, COMICS!"));
</script>
```

### 9. Frontend vs Backend, Static vs Dynamic

| | Frontend | Backend |
| - | -------- | ------- |
| Berjalan di | Browser (client) | Server |
| Teknologi | HTML, CSS, JavaScript, React, Vue | Node.js, Python (Flask/Django/FastAPI), PHP, Go |
| Tanggung jawab | Tampilan, interaksi pengguna | Logika bisnis, autentikasi, akses database, API |

- **Static website** — server mengirim file yang sama untuk setiap pengunjung (contoh: portfolio, dokumentasi). Bisa di-host gratis di GitHub Pages.
- **Dynamic website** — konten dihasilkan berdasarkan user, waktu, atau data di database (contoh: media sosial, e-commerce).

### 10. Browser DevTools

Buka dengan **F12** atau **Ctrl+Shift+I** (macOS: **Cmd+Option+I**).

| Tab | Kegunaan |
| --- | -------- |
| **Elements** | Melihat & mengedit HTML/CSS secara live |
| **Console** | Menjalankan JavaScript, melihat error |
| **Network** | Melihat semua HTTP request/response, status code, ukuran, waktu |
| **Application** | Melihat cookies, localStorage |
| **Lighthouse** | Audit performance, accessibility, SEO |

## Guided Practice

**Step 1 — DNS lookup**

Buka terminal dan jalankan:

```bash
nslookup github.com
nslookup wikipedia.org  # coba juga domain lain yang Anda kenal
```

Catat IP address yang didapat. Coba buka IP tersebut langsung di browser — apa yang terjadi?

**Step 2 — Request HTTP dengan `curl`**

```bash
curl -I https://example.com                 # hanya header response
curl -I http://github.com                   # perhatikan status 301 dan header Location
curl -s https://example.com | head -n 20    # body HTML (Linux/macOS/WSL)
curl -I https://example.com/halaman-tidak-ada
```

> Pengguna PowerShell: gunakan `curl.exe` (bukan `curl`) agar tidak tertukar dengan alias `Invoke-WebRequest`.

**Step 3 — Network tab**

1. Buka <https://developer.mozilla.org> di browser.
2. Tekan **F12** → tab **Network** → centang **Disable cache** → refresh (**Ctrl+R**).
3. Klik request pertama (dokumen HTML). Amati tab **Headers**: *Request URL, Request Method, Status Code, Remote Address*, dan response headers seperti `content-type`.
4. Lihat kolom **Type** — berapa banyak request CSS, JS, gambar, dan font?
5. Lihat baris status bawah: total *requests*, *transferred*, dan *load time*.

**Step 4 — Edit halaman secara live**

Pada tab **Elements**, klik kanan sebuah judul → *Edit as HTML* → ganti teksnya. Ubah juga warna background di panel **Styles**. Refresh halaman — perubahan hilang. Mengapa?

**Step 5 — Halaman web pertama Anda**

1. Buat folder `week01/` dan file `index.html` di VS Code.
2. Ketik `!` lalu tekan **Tab** (Emmet) untuk membuat boilerplate HTML.
3. Isi `<body>` dengan:

   ```html
   <h1>Halo, Web!</h1>
   <p>Ini halaman web pertama saya di COMICS Study Group 2026.</p>
   <a href="https://developer.mozilla.org">Belajar di MDN</a>
   ```

4. Buka dengan **Live Server** (klik kanan → *Open with Live Server*). Perhatikan URL-nya (`http://127.0.0.1:5500/...`) — Anda sekarang menjalankan **web server lokal**!
5. Buka DevTools → Network dan refresh. Status code apa yang muncul?

## Assignment (Referencing ke /Assignment)

Kerjakan **[Assignment 01 — Web Fundamental](../Assignment/Assignment-01-Web-Fundamental.md)**. Deadline: **14 Oktober 2026, 23:59 WIB**.

- [ ] Task 1 — Conceptual questions
- [ ] Task 2 — URL dissection
- [ ] Task 3 — DNS & HTTP investigation dengan `curl`
- [ ] Task 4 — DevTools Network analysis
- [ ] Task 5 — Diagram "What happens when you type a URL"

## Self-Reflection

1. Apa konsep utama yang dipelajari?
2. Apa kesulitan yang ditemukan?
3. Setelah mempelajari materi ini, apa yang berubah dari cara Anda memandang sebuah website ketika membukanya?
4. Status code apa yang paling sering Anda temui selama investigasi, dan apa artinya?
5. Apa yang ingin Anda tanyakan atau diskusikan pada Meeting 1 (22 Oktober)?

## Further Reading

- [MDN — How the web works](https://developer.mozilla.org/en-US/docs/Learn_web_development/Getting_started/Web_standards/How_the_web_works)
- [MDN — An overview of HTTP](https://developer.mozilla.org/en-US/docs/Web/HTTP/Overview)
- [MDN — HTTP response status codes](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status)
- [How DNS Works (comic)](https://howdns.works/)
- [Chrome DevTools — Inspect network activity](https://developer.chrome.com/docs/devtools/network)
- [What happens when you type google.com into your browser? (GitHub)](https://github.com/alex/what-happens-when)
- [HTTP Cats](https://http.cat/) — cara menyenangkan menghafal status code.
