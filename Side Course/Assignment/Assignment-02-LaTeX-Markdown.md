# Assignment 02 — LaTeX & Markdown

> 📚 **Materi terkait:** [Lesson 02 — LaTeX & Markdown](../Resource/Lesson-02-LaTeX-Markdown.md)

## Tujuan
Assignment ini memastikan Anda terampil menggunakan sintaks Markdown untuk formatting dokumen teknis dan menguasai penulisan rumus/persamaan matematika kompleks menggunakan LaTeX di Markdown. Kemampuan ini akan digunakan langsung saat Anda mengumpulkan tugas di track Quantum Physics, Computer Cluster, dan Web Development.

## Deliverables

```text
assignment-02/
├── cheat-sheet.md      ← Task 1 (Dokumen komprehensif sintaks Markdown)
├── math-formulas.md    ← Task 2 & Task 3 (Kumpulan persamaan LaTeX)
├── report-template.md  ← Task 4 (Template laporan tugas teknis yang siap pakai)
└── answers.md          ← Task 5 (Jawaban refleksi diri)
```

---

## Task 1 — Comprehensive Markdown Formatting Document

Buat file bernama `cheat-sheet.md` yang mendemonstrasikan **seluruh** elemen formatting Markdown berikut dengan konten bertema teknologi/sains komputer:

1. **Heading Hirarki**: Tampilkan contoh Heading level 1 (`#`) hingga level 4 (`####`).
2. **Penekanan Teks**: Paragraf yang memuat kata bercetak **tebal**, *miring*, ***tebal dan miring***, serta ~~dicoret~~.
3. **Daftar (Lists)**:
   - Satu ordered list (daftar nomor) dengan minimal 3 langkah instalasi/setup.
   - Satu unordered list dengan minimal 2 tingkat indentasi (*nested list*).
   - Satu task list (*checkbox*) dengan minimal 3 item (minimal satu item sudah dicentang `[x]`).
4. **Kutipan & Callout**:
   - Satu blockquote standar (`>`).
   - Minimal dua buah GitHub Alert blocks yang berbeda (misalnya `> [!NOTE]` dan `> [!TIP]`).
5. **Code Snippets**:
   - Contoh inline code.
   - Contoh fenced code block dengan penanda bahasa Python atau Bash (minimal 5 baris kode).
6. **Tabel Data**:
   - Tabel dengan minimal 4 baris data dan 3 kolom yang memiliki pengaturan alignment berbeda (satu kolom rata kiri, satu kolom rata tengah, dan satu kolom rata kanan).
7. **Hyperlink & Gambar**:
   - Satu tautan aktif ke sumber belajar eksternal.
   - Satu gambar (boleh dari URL publik, misal badge atau logo teknologi) lengkap dengan alt-text.

---

## Task 2 — Transkripsi Formula Matematika Dasar ke LaTeX

Di dalam file `math-formulas.md`, tuliskan kode LaTeX untuk formula-formula matematika berikut (tampilkan dalam bentuk Display Math `$$ ... $$`):

1. **Rumus Kuadratik (ABC)**:
   $$
   x = \frac{-b \pm \sqrt{b^2 - 4ac}}{2a}
   $$

2. **Deret Geometri Tak Hingga**:
   $$
   S_\infty = \sum_{n=0}^{\infty} a r^n = \frac{a}{1 - r} \quad \text{untuk } |r| < 1
   $$

3. **Limit Turunan Pertama (Definisi Diferensial)**:
   $$
   f'(x) = \lim_{\Delta x \to 0} \frac{f(x + \Delta x) - f(x)}{\Delta x}
   $$

4. **Integral Distribusi Normal (Gauss)**:
   $$
   I = \int_{-\infty}^{\infty} e^{-x^2}\,dx = \sqrt{\pi}
   $$

Di bawah setiap persamaan, tuliskan penjelasan singkat dalam Markdown tentang apa arti simbol-simbol yang digunakan.

---

## Task 3 — Formula Saintifik & Matriks Quantum State

Lanjutkan di file `math-formulas.md` dengan menambahkan persamaan-persamaan mekanika kuantum dan aljabar linear berikut:

1. **Tiga Matriks Pauli ($X, Y, Z$)**:
   Tuliskan ketiga matriks $2 \times 2$ berikut dalam satu baris display math menggunakan `\begin{pmatrix}`:
   $$
   \sigma_x = \begin{pmatrix} 0 & 1 \\ 1 & 0 \end{pmatrix}, \quad
   \sigma_y = \begin{pmatrix} 0 & -i \\ i & 0 \end{pmatrix}, \quad
   \sigma_z = \begin{pmatrix} 1 & 0 \\ 0 & -1 \end{pmatrix}
   $$

2. **Postulat Born Rule & Inner Product**:
   Tuliskan probabilitas pengukuran dalam notasi Dirac bra-ket:
   $$
   P(k) = |\langle k | \psi \rangle|^2
   $$

3. **Persamaan Schrödinger Bergantung Waktu (Multi-baris Aligned)**:
   Gunakan environment `\begin{aligned}` untuk menuliskan sistem persamaan berikut agar tanda sama dengan (`=`) sejajar rapi:
   $$
   \begin{aligned}
   i\hbar \frac{\partial}{\partial t} |\Psi(t)\rangle &= \hat{H} |\Psi(t)\rangle \\
   |\Psi(t)\rangle &= e^{-i\hat{H}t/\hbar} |\Psi(0)\rangle
   \end{aligned}
   $$

4. **Kombinasi Superposisi Keadaan 2-Qubit**:
   Tuliskan state Bell state $|\Phi^+\rangle$:
   $$
   |\Phi^+\rangle = \frac{1}{\sqrt{2}} (|00\rangle + |11\rangle) = \frac{1}{\sqrt{2}} \begin{pmatrix} 1 \\ 0 \\ 0 \\ 1 \end{pmatrix}
   $$

---

## Task 4 — Desain Template Laporan Teknis Terstruktur

Buat file bernama `report-template.md`. File ini adalah template generik siap pakai yang akan Anda gunakan untuk mengerjakan tugas-tugas mingguan berikutnya di COMICS Study Group.

Struktur template minimal memuat:
- Header dokumen (Judul tugas, metadata nama peserta, track, tanggal deadline, status pengerjaan).
- Section **Tujuan Pengerjaan**.
- Section **Ringkasan Jawaban / Solusi** (memuat tabel ringkas).
- Section **Detail Implementasi Kode & Output Terminal** (blok kode bash/python/html).
- Section **Persamaan Matematika yang Digunakan** (blok display math LaTeX).
- Section **Kendala & Troubleshooting** (callout block `> [!WARNING]` atau `> [!TIP]`).
- Section **Kesimpulan & Referensi** (list bullet + link).

Pastikan template tersebut rapi, bersih, dan memanjakan mata pembaca saat dirender di GitHub.

---

## Task 5 — Refleksi Pembelajaran

Buat file `answers.md` dan jawab seluruh pertanyaan refleksi yang tercantum pada [Lesson 02](../Resource/Lesson-02-LaTeX-Markdown.md#self-reflection).

---

## Bonus (Opsional)

1. Tuliskan formula [Hukum Radiasi Planck Spektral $B_\nu(T)$](https://en.wikipedia.org/wiki/Planck%27s_law) dalam domain frekuensi $\nu$ dan domain panjang gelombang $\lambda$ secara bersandingan di dalam `math-formulas.md`.
2. Buat diagram alur sederhana langsung di dalam file Markdown menggunakan sintaks [Mermaid](https://mermaid.js.org/) (contoh: diagram flowchart atau sequence diagram).

---

## Rubrik Penilaian

| Komponen | Bobot |
| -------- | ----- |
| Task 1 — Markdown Cheatsheet (Kelengkapan elemen) | 25% |
| Task 2 — Transkripsi Formula Matematika Dasar LaTeX | 20% |
| Task 3 — Formula Fisika Kuantum & Matriks LaTeX | 25% |
| Task 4 — Desain Template Laporan Teknis | 15% |
| Task 5 — Refleksi Diri | 15% |
| Bonus | +10% |
