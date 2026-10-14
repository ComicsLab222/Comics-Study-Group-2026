# Assignment 02 — HTML & CSS

> 📅 **Periode:** 15–21 Oktober 2026 · ⏰ **Deadline:** 21 Oktober 2026, 23:59 WIB
> 📚 **Materi terkait:** [Lesson 02 — HTML & CSS](../Resource/Lesson-02-HTML-CSS.md)

## Tujuan

Membangun **halaman personal profile / portfolio** yang semantik, menarik, accessible, dan responsive — **tanpa framework CSS** (tanpa Bootstrap/Tailwind) dan **tanpa template**. Halaman ini akan terus Anda kembangkan pada topik-topik berikutnya (JavaScript, Git & GitHub Pages).

## Deliverables

Upload deliverables ke repository GitHub masing-masing dengan ketentuan:
- **Format nama repository:** `<nama>-CSG-2026` (contoh: `budi-CSG-2026`; CSG = *Comics Study Group*).
- **README.md:** Wajib menyertakan file `README.md` pada root repository yang berisi deskripsi repository (format dibebaskan).
- **Struktur folder:** Masukkan deliverables ke dalam folder:

```text
assignment-02/
├── index.html
├── style.css
├── assets/
│   └── (gambar, ikon, dll.)
├── screenshots/
│   ├── mobile.png       ← lebar 375px
│   ├── tablet.png       ← lebar 768px
│   ├── desktop.png      ← lebar ≥ 1280px
│   └── lighthouse.png
└── REPORT.md            ← jawaban Task 5 + refleksi
```

---

## Task 1 — Semantic HTML: Struktur Halaman

Buat `index.html` dengan struktur semantik berikut:

```text
<header>   → nama/logo + <nav> berisi link ke setiap section (anchor #id)
<main>
  <section id="about">     → foto/avatar, nama (h1), tagline, paragraf perkenalan
  <section id="skills">    → daftar skill / tools yang sedang/ingin dipelajari (list)
  <section id="projects">  → minimal 3 <article> project/aktivitas (boleh rencana project)
  <section id="schedule">  → <table> jadwal Meeting COMICS Study Group 2026
  <section id="contact">   → <form> kontak: nama, email, track (select), pesan (textarea), tombol submit
</main>
<footer>   → copyright + link sosial media / GitHub
```

**Ketentuan:**

- [ ] Menggunakan `<!DOCTYPE html>`, `lang="id"`, `meta charset`, `meta viewport`, `meta description`, dan `<title>` yang deskriptif.
- [ ] Hanya **satu** `<h1>`; heading lain berurutan (`h2`, `h3`).
- [ ] Setiap `<img>` memiliki atribut `alt` yang bermakna.
- [ ] Setiap input form memiliki `<label>` yang terhubung (`for` ↔ `id`), dan input email menggunakan `type="email"` serta `required`.
- [ ] Tabel jadwal menggunakan `<thead>`, `<tbody>`, dan `<th>`; isi dengan jadwal meeting dari [README track](../README.md#roadmap) (tanggal + agenda).
- [ ] Tidak menggunakan `<div>` jika ada elemen semantik yang lebih tepat.

## Task 2 — Styling: CSS Variables, Box Model, & Tipografi

Buat `style.css` (external stylesheet) dengan ketentuan:

- [ ] Reset `box-sizing: border-box` untuk semua elemen.
- [ ] Mendefinisikan **minimal 5 CSS custom properties** di `:root` (warna, radius, font, spacing).
- [ ] Menggunakan **Google Fonts** (maksimal 2 font family).
- [ ] Font size dan spacing menggunakan `rem` (bukan `px`).
- [ ] Palet warna yang konsisten (3–5 warna) dengan kontras teks yang baik.
- [ ] State `:hover` dan `:focus-visible` pada link, tombol, dan input.
- [ ] Minimal satu efek **transition** (misal hover pada card project).
- [ ] Tidak menggunakan inline style maupun `!important`.

## Task 3 — Layout: Flexbox & Grid

- [ ] **Navbar** di header menggunakan **Flexbox** (logo di kiri, menu di kanan).
- [ ] Section `about` menggunakan Flexbox untuk menyusun foto dan teks berdampingan (di desktop).
- [ ] Section `projects` menggunakan **CSS Grid** untuk menampilkan card project.
- [ ] Form kontak tersusun rapi (label di atas input, lebar input konsisten).
- [ ] Konten utama memiliki `max-width` dan berada di tengah layar pada desktop.

Di `REPORT.md`, jelaskan secara singkat mengapa Anda memilih Flexbox atau Grid untuk setiap bagian di atas.

## Task 4 — Responsive Design

Terapkan pendekatan **mobile-first** dengan minimal **2 breakpoint**:

| Layar | Lebar | Ekspektasi Layout |
| ----- | ----- | ----------------- |
| Mobile | < 768px | Satu kolom; navbar boleh tersusun vertikal/wrap; foto di atas teks |
| Tablet | ≥ 768px | Grid project 2 kolom |
| Desktop | ≥ 1024px | Grid project 3 kolom; foto & teks about berdampingan |

- [ ] Tidak ada **horizontal scroll** di lebar 375px.
- [ ] Gambar tidak melebihi container (`max-width: 100%`).
- [ ] Tabel jadwal tetap terbaca di mobile (*hint:* bungkus dengan container `overflow-x: auto`).
- [ ] Ambil screenshot di ketiga ukuran menggunakan **Device Toolbar** DevTools (*Capture screenshot* / *Capture full size screenshot* dari menu ⋮).

## Task 5 — Validasi, Accessibility, & Lighthouse

1. Validasi HTML Anda di [W3C Markup Validation Service](https://validator.w3.org/#validate_by_input) (tab *Validate by Direct Input*). Perbaiki hingga **0 error**. Catat warning yang tersisa (jika ada) di `REPORT.md`.
2. Navigasikan seluruh halaman **hanya dengan keyboard** (Tab, Shift+Tab, Enter). Apakah semua link dan input dapat dijangkau dan terlihat fokusnya?
3. Jalankan **Lighthouse** (DevTools → Lighthouse → mode *Navigation*, device *Mobile*) dan lampirkan screenshot hasilnya. Target: **Accessibility ≥ 90** dan **SEO ≥ 90**.
4. Jika ada skor di bawah target, tuliskan rekomendasi Lighthouse yang muncul dan apa yang sudah Anda perbaiki.
5. Tulis jawaban **Self-Reflection** Lesson 02 di bagian akhir `REPORT.md`.

---

## Bonus (Opsional)

1. Tambahkan **dark mode** otomatis menggunakan `@media (prefers-color-scheme: dark)` dan CSS variables.
2. Buat navbar menjadi **sticky** (`position: sticky`) dan tambahkan `scroll-behavior: smooth` agar navigasi antar section terasa halus.
3. Selesaikan seluruh level [Flexbox Froggy](https://flexboxfroggy.com/) dan [Grid Garden](https://cssgridgarden.com/), lampirkan screenshot level terakhir.

## Rubrik Penilaian

| Komponen | Bobot |
| -------- | ----- |
| Task 1 — Semantic HTML & struktur | 25% |
| Task 2 — Styling & konsistensi desain | 20% |
| Task 3 — Layout Flexbox & Grid | 20% |
| Task 4 — Responsive design | 20% |
| Task 5 — Validasi, accessibility, Lighthouse | 15% |
| Bonus | +10% |

> [!NOTE]
> Penilaian desain tidak menuntut Anda menjadi desainer profesional — yang dinilai adalah **konsistensi**, **keterbacaan**, dan **penerapan konsep** dari Lesson 02. Halaman sederhana yang rapi dan semantik lebih baik daripada halaman ramai yang berantakan.
