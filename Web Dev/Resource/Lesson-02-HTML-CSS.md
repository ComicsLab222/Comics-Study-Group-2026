# Lesson 02 — HTML & CSS

> 📅 **Self-study 2:** 15–21 Oktober 2026 · 💬 Dibahas pada **Meeting 1 (22 Oktober)**

## Learning Objectives

Setelah menyelesaikan materi ini, peserta mampu:

- Menyusun dokumen HTML yang valid dengan struktur `<!DOCTYPE>`, `<head>`, dan `<body>`.
- Menggunakan elemen HTML umum (heading, paragraph, list, link, image, table, form) beserta atributnya.
- Menerapkan **semantic HTML** (`<header>`, `<nav>`, `<main>`, `<section>`, `<article>`, `<footer>`) dan prinsip dasar **accessibility**.
- Menghubungkan CSS ke HTML dan menggunakan **selector**, memahami **cascade** dan **specificity**.
- Menjelaskan dan menerapkan **box model** (content, padding, border, margin).
- Mengatur tipografi, warna, dan unit CSS (`px`, `rem`, `%`, `vw`).
- Membuat layout menggunakan **Flexbox** dan **CSS Grid**.
- Membuat halaman **responsive** menggunakan media query dengan pendekatan *mobile-first*.

## Prerequisites

**Materi prasyarat**

- [Lesson 01 — Web Fundamental](Lesson-01-Web-Fundamental.md): peran HTML/CSS/JS, cara browser merender halaman, DevTools.

**Tools yang diperlukan**

- **Visual Studio Code** + extension **Live Server**.
- Browser modern dengan DevTools (Chrome / Edge / Firefox).
- Opsional: extension **Prettier** (auto-format kode) dan **HTML CSS Support**.

## Learning Materials

### 1. Struktur Dokumen HTML

**HTML (HyperText Markup Language)** menggunakan **elemen** yang ditandai dengan **tag** untuk mendeskripsikan struktur konten.

```html
<!DOCTYPE html>                     <!-- deklarasi HTML5 -->
<html lang="id">                    <!-- root element + bahasa halaman -->
  <head>                            <!-- metadata: tidak tampil di halaman -->
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta name="description" content="Profil peserta COMICS Study Group 2026" />
    <title>Profil Saya</title>
    <link rel="stylesheet" href="style.css" />
  </head>
  <body>                            <!-- konten yang tampil -->
    <h1>Halo!</h1>
  </body>
</html>
```

**Anatomi elemen:**

```text
<a href="https://mdn.dev" target="_blank">Belajar MDN</a>
│  └────────┬───────────┘ └─────┬──────┘│          │
│       attribute           attribute   content   closing tag
└─ opening tag
```

Beberapa elemen tidak memiliki content/closing tag (*void element*): `<img>`, `<br>`, `<hr>`, `<input>`, `<meta>`, `<link>`.

### 2. Elemen HTML yang Sering Digunakan

| Kategori | Elemen | Keterangan |
| -------- | ------ | ---------- |
| Heading | `<h1>` – `<h6>` | Gunakan **satu `<h1>`** per halaman; jangan lompat level |
| Teks | `<p>`, `<strong>`, `<em>`, `<br>`, `<blockquote>`, `<code>` | `<strong>` = penting (bukan sekadar tebal) |
| List | `<ul>`, `<ol>`, `<li>` | Unordered / ordered list |
| Link | `<a href="...">` | `href` bisa URL absolut, relatif, `#id`, `mailto:` |
| Gambar | `<img src="..." alt="...">` | `alt` **wajib** untuk accessibility |
| Tabel | `<table>`, `<thead>`, `<tbody>`, `<tr>`, `<th>`, `<td>` | Hanya untuk data tabular, **bukan** untuk layout |
| Form | `<form>`, `<label>`, `<input>`, `<textarea>`, `<select>`, `<button>` | Setiap input sebaiknya punya `<label>` |
| Generic | `<div>` (block), `<span>` (inline) | Gunakan jika tidak ada elemen semantik yang cocok |

**Contoh form:**

```html
<form action="/subscribe" method="post">
  <label for="email">Email</label>
  <input type="email" id="email" name="email" placeholder="nama@email.com" required />

  <label for="track">Track</label>
  <select id="track" name="track">
    <option value="webdev">Web Dev</option>
    <option value="cluster">Computer Cluster</option>
    <option value="quantum">Quantum Physics</option>
  </select>

  <button type="submit">Daftar</button>
</form>
```

### 3. Semantic HTML & Accessibility

Semantic HTML memberi **makna** pada struktur halaman, bukan hanya tampilan. Manfaatnya: lebih mudah dibaca developer, lebih baik untuk **SEO**, dan dapat dipahami **screen reader** (pengguna tunanetra).

```text
┌───────────────────────── <header> ─────────────────────────┐
│  Logo                       <nav> Home | About | Contact   │
├────────────────────────────────────────────────────────────┤
│ <main>                                                     │
│   ┌────────── <section> ──────────┐  ┌──── <aside> ────┐   │
│   │ <article>  <article>          │  │ Sidebar / info  │   │
│   └───────────────────────────────┘  └─────────────────┘   │
├───────────────────────── <footer> ─────────────────────────┤
│  © 2026 COMICS                                             │
└────────────────────────────────────────────────────────────┘
```

**Checklist accessibility dasar:**

- Setiap `<img>` memiliki `alt` yang deskriptif (atau `alt=""` jika dekoratif).
- Setiap input form memiliki `<label for="...">`.
- Gunakan heading secara berurutan (`h1 → h2 → h3`).
- Kontras warna teks dan background cukup tinggi.
- Halaman dapat dinavigasi dengan keyboard (**Tab**).

### 4. Menghubungkan CSS

| Cara | Contoh | Rekomendasi |
| ---- | ------ | ----------- |
| Inline | `<p style="color: red">` | ❌ Hindari |
| Internal | `<style> p { color: red; } </style>` di `<head>` | Untuk eksperimen kecil |
| **External** | `<link rel="stylesheet" href="style.css">` | ✅ **Gunakan ini** |

**Anatomi aturan CSS:**

```css
selector {
  property: value;   /* declaration */
}

h1 {
  color: #2d3436;
  font-size: 2rem;
}
```

### 5. Selector

| Selector | Contoh | Target |
| -------- | ------ | ------ |
| Element | `p` | semua `<p>` |
| Class | `.card` | elemen dengan `class="card"` (bisa banyak elemen) |
| ID | `#hero` | elemen dengan `id="hero"` (unik per halaman) |
| Descendant | `nav a` | `<a>` di dalam `<nav>` |
| Child | `ul > li` | `<li>` anak langsung `<ul>` |
| Group | `h1, h2, h3` | semua heading tersebut |
| Attribute | `input[type="email"]` | input bertipe email |
| Pseudo-class | `a:hover`, `li:nth-child(2)`, `input:focus` | berdasarkan state/posisi |
| Pseudo-element | `p::first-line`, `.btn::after` | bagian dari elemen |

### 6. Cascade & Specificity

Ketika beberapa aturan menargetkan elemen yang sama, browser menentukan pemenangnya dengan urutan:

1. **Importance** — `!important` (hindari sebisa mungkin).
2. **Specificity** — semakin spesifik selector, semakin kuat.
3. **Source order** — jika specificity sama, aturan yang ditulis **terakhir** menang.

| Selector | Specificity (ID, Class, Element) |
| -------- | -------------------------------- |
| `p` | (0, 0, 1) |
| `.intro` | (0, 1, 0) |
| `p.intro` | (0, 1, 1) |
| `#main .intro p` | (1, 1, 1) |
| `style="..."` (inline) | mengalahkan semua selector di atas |

Beberapa property seperti `color` dan `font-family` juga **diwariskan (inherited)** dari parent ke child.

### 7. Box Model

Setiap elemen HTML adalah sebuah kotak:

```text
┌──────────────────────── margin ────────────────────────┐
│  ┌───────────────────── border ─────────────────────┐  │
│  │  ┌────────────────── padding ─────────────────┐  │  │
│  │  │                                            │  │  │
│  │  │                 content                    │  │  │
│  │  │            (width × height)                │  │  │
│  │  │                                            │  │  │
│  │  └────────────────────────────────────────────┘  │  │
│  └──────────────────────────────────────────────────┘  │
└────────────────────────────────────────────────────────┘
```

```css
.card {
  width: 300px;
  padding: 16px;              /* ruang di dalam border */
  border: 2px solid #dfe6e9;
  margin: 24px auto;          /* ruang di luar border; auto = center horizontal */
}
```

> [!TIP]
> Secara default, `width` hanya menghitung **content**, sehingga lebar total `.card` di atas = 300 + 2×16 + 2×2 = **336px**. Tambahkan reset berikut di awal setiap project agar `width` mencakup padding dan border:
>
> ```css
> *, *::before, *::after { box-sizing: border-box; }
> ```

**Display:** `block` (mengambil satu baris penuh, contoh `div`, `p`, `h1`), `inline` (mengalir dalam teks, width/height diabaikan, contoh `span`, `a`), `inline-block`, `none` (disembunyikan), `flex`, `grid`.

### 8. Unit, Warna, dan Tipografi

| Unit | Relatif terhadap | Penggunaan |
| ---- | ---------------- | ---------- |
| `px` | absolut | border, shadow |
| `rem` | font-size root (`<html>`, default 16px) | **font-size, spacing** (direkomendasikan) |
| `em` | font-size elemen itu sendiri | padding tombol |
| `%` | ukuran parent | lebar layout |
| `vw` / `vh` | 1% lebar / tinggi viewport | hero section full-screen |

**Warna:** `#6c5ce7` (hex), `rgb(108 92 231)`, `hsl(248 75% 63%)`, atau dengan transparansi `rgb(0 0 0 / 50%)`.

**CSS custom properties (variables):**

```css
:root {
  --color-primary: #6c5ce7;
  --color-text: #2d3436;
  --radius: 12px;
  --font-body: "Inter", system-ui, sans-serif;
}

body {
  font-family: var(--font-body);
  color: var(--color-text);
  line-height: 1.6;
}

.btn {
  background: var(--color-primary);
  border-radius: var(--radius);
}
```

Gunakan font dari [Google Fonts](https://fonts.google.com/) dengan menambahkan `<link>` yang disediakan di `<head>`.

### 9. Flexbox — Layout Satu Dimensi

Flexbox mengatur item dalam **satu arah** (baris atau kolom).

```css
.navbar {
  display: flex;
  flex-direction: row;            /* row | column */
  justify-content: space-between; /* alignment di main axis */
  align-items: center;            /* alignment di cross axis */
  gap: 1rem;                      /* jarak antar item */
  flex-wrap: wrap;                /* item turun ke baris baru jika tidak muat */
}
```

```text
justify-content:
flex-start     [■■■         ]
center         [    ■■■     ]
space-between  [■     ■    ■]
space-around   [ ■   ■   ■  ]
```

### 10. CSS Grid — Layout Dua Dimensi

Grid mengatur item dalam **baris dan kolom** sekaligus.

```css
.gallery {
  display: grid;
  grid-template-columns: repeat(3, 1fr);  /* 3 kolom sama lebar */
  gap: 1.5rem;
}

/* Responsive otomatis tanpa media query */
.gallery-auto {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
  gap: 1.5rem;
}
```

> **Kapan pakai apa?** Flexbox untuk komponen (navbar, tombol berjajar, card content). Grid untuk layout halaman atau galeri. Keduanya sering dikombinasikan.

### 11. Responsive Design

Pendekatan **mobile-first**: tulis style untuk layar kecil terlebih dahulu, lalu tambahkan media query untuk layar yang lebih besar.

```css
/* Mobile (default) */
.container {
  padding: 1rem;
}
.features {
  display: grid;
  grid-template-columns: 1fr;
  gap: 1rem;
}

/* Tablet ke atas */
@media (min-width: 768px) {
  .features { grid-template-columns: repeat(2, 1fr); }
}

/* Desktop ke atas */
@media (min-width: 1024px) {
  .container { max-width: 1100px; margin: 0 auto; }
  .features { grid-template-columns: repeat(3, 1fr); }
}
```

> [!IMPORTANT]
> Tanpa `<meta name="viewport" content="width=device-width, initial-scale=1.0">` di `<head>`, media query tidak akan bekerja dengan benar di perangkat mobile.

Uji responsivitas dengan **Device Toolbar** di DevTools (**Ctrl+Shift+M**).

### 12. Transisi & Hover (Sentuhan Interaktif)

```css
.card {
  transition: transform 0.2s ease, box-shadow 0.2s ease;
}
.card:hover {
  transform: translateY(-4px);
  box-shadow: 0 12px 24px rgb(0 0 0 / 12%);
}
```

## Guided Practice

Kita akan membuat **komponen profile card** yang responsive.

**Step 1 — Struktur folder**

```text
week02-practice/
├── index.html
└── style.css
```

**Step 2 — HTML (`index.html`)**

```html
<!DOCTYPE html>
<html lang="id">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Tim COMICS</title>
    <link rel="preconnect" href="https://fonts.googleapis.com" />
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;800&display=swap" rel="stylesheet" />
    <link rel="stylesheet" href="style.css" />
  </head>
  <body>
    <header class="site-header">
      <h1>Tim COMICS Study Group</h1>
      <nav>
        <a href="#team">Team</a>
        <a href="#contact">Contact</a>
      </nav>
    </header>

    <main class="container">
      <section id="team" class="team-grid">
        <article class="card">
          <img src="https://api.dicebear.com/9.x/thumbs/svg?seed=Andi" alt="Avatar Andi" />
          <h2>Andi</h2>
          <p class="role">Computer Cluster</p>
          <p>Suka mengoprek Linux dan menjalankan simulasi di cluster.</p>
        </article>
        <article class="card">
          <img src="https://api.dicebear.com/9.x/thumbs/svg?seed=Citra" alt="Avatar Citra" />
          <h2>Citra</h2>
          <p class="role">Web Development</p>
          <p>Senang membuat UI yang rapi dan mudah digunakan.</p>
        </article>
        <article class="card">
          <img src="https://api.dicebear.com/9.x/thumbs/svg?seed=Eka" alt="Avatar Eka" />
          <h2>Eka</h2>
          <p class="role">Quantum Physics</p>
          <p>Tertarik pada quantum computing dan simulasi kuantum.</p>
        </article>
      </section>
    </main>

    <footer id="contact" class="site-footer">
      <p>&copy; 2026 COMICS Study Group</p>
    </footer>
  </body>
</html>
```

**Step 3 — CSS (`style.css`)**

```css
*, *::before, *::after { box-sizing: border-box; }

:root {
  --bg: #0f172a;
  --surface: #1e293b;
  --primary: #8b5cf6;
  --text: #e2e8f0;
  --muted: #94a3b8;
  --radius: 16px;
}

body {
  margin: 0;
  font-family: "Inter", system-ui, sans-serif;
  background: var(--bg);
  color: var(--text);
  line-height: 1.6;
}

.site-header {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  align-items: center;
  gap: 1rem;
  padding: 1rem 1.5rem;
}

.site-header h1 { font-size: 1.25rem; margin: 0; }
.site-header nav { display: flex; gap: 1rem; }
.site-header a { color: var(--muted); text-decoration: none; }
.site-header a:hover { color: var(--primary); }

.container { padding: 1.5rem; }

.team-grid {
  display: grid;
  grid-template-columns: 1fr;
  gap: 1.5rem;
}

.card {
  background: var(--surface);
  border-radius: var(--radius);
  padding: 1.5rem;
  text-align: center;
  transition: transform 0.2s ease, box-shadow 0.2s ease;
}

.card:hover {
  transform: translateY(-6px);
  box-shadow: 0 16px 32px rgb(139 92 246 / 25%);
}

.card img { width: 96px; height: 96px; border-radius: 50%; }
.card h2 { margin: 0.75rem 0 0.25rem; }
.role { color: var(--primary); font-weight: 600; margin: 0 0 0.5rem; }

.site-footer { text-align: center; padding: 2rem; color: var(--muted); }

@media (min-width: 768px) {
  .team-grid { grid-template-columns: repeat(2, 1fr); }
}

@media (min-width: 1024px) {
  .container { max-width: 1100px; margin: 0 auto; }
  .team-grid { grid-template-columns: repeat(3, 1fr); }
}
```

**Step 4 — Eksperimen**

1. Buka dengan **Live Server**, lalu aktifkan **Device Toolbar** (**Ctrl+Shift+M**). Ubah lebar layar dan amati perubahan jumlah kolom.
2. Di DevTools → **Elements**, klik sebuah `.card` dan lihat diagram **box model** di tab *Computed*. Ubah `padding` dan amati perubahannya.
3. Ganti `grid-template-columns` menjadi `repeat(auto-fit, minmax(240px, 1fr))` dan hapus kedua media query. Apa yang terjadi?
4. Ubah nilai `--primary` di `:root` dan lihat bagaimana seluruh warna aksen berubah sekaligus.
5. Tekan **Tab** berulang kali — apakah link di navbar dapat difokuskan? Tambahkan style `a:focus-visible { outline: 2px solid var(--primary); }`.

## Assignment (Referencing ke /Assignment)

Kerjakan **[Assignment 02 — HTML & CSS](../Assignment/Assignment-02-HTML-CSS.md)**. Deadline: **21 Oktober 2026, 23:59 WIB**.

- [ ] Task 1 — Semantic HTML: struktur halaman personal profile
- [ ] Task 2 — Styling dengan CSS variables, box model, dan tipografi
- [ ] Task 3 — Layout dengan Flexbox & Grid
- [ ] Task 4 — Responsive design (mobile, tablet, desktop)
- [ ] Task 5 — Validasi, accessibility, & Lighthouse audit

## Self-Reflection

1. Apa konsep utama yang dipelajari?
2. Apa kesulitan yang ditemukan?
3. Kapan Anda memilih Flexbox dan kapan memilih Grid? Berikan contoh dari pekerjaan Anda.
4. Mengapa semantic HTML dan accessibility penting, meskipun tampilan halaman terlihat sama?
5. Apa yang ingin Anda tanyakan atau diskusikan pada Meeting 1 (22 Oktober)?

## Further Reading

- [MDN — Structuring content with HTML](https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/Structuring_content)
- [MDN — CSS styling basics](https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/Styling_basics)
- [web.dev — Learn HTML](https://web.dev/learn/html)
- [web.dev — Learn CSS](https://web.dev/learn/css)
- [CSS-Tricks — A Complete Guide to Flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)
- [CSS-Tricks — A Complete Guide to CSS Grid](https://css-tricks.com/snippets/css/complete-guide-grid/)
- [Flexbox Froggy](https://flexboxfroggy.com/) & [Grid Garden](https://cssgridgarden.com/) — game untuk melatih Flexbox dan Grid.
- [W3C Markup Validation Service](https://validator.w3.org/)
