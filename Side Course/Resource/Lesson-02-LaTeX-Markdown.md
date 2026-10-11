# Lesson 02 — LaTeX & Markdown

## Learning Objectives
Setelah menyelesaikan materi ini, peserta mampu:
- Menjelaskan konsep dan fungsi **Markdown** sebagai format penulisan dokumentasi teknis serta **LaTeX** sebagai sistem typesetting saintifik dan formula matematika.
- Melakukan pemformatan teks Markdown secara komprehensif: header tingkat 1–6, bold, italic, strikethrough, quote/callout, list (bernomor, tak bernomor, task list), tabel, link, gambar, dan code block.
- Mengintegrasikan penulisan persamaan matematika LaTeX di dalam dokumen Markdown baik secara inline (`$ ... $`) maupun display/block (`$$ ... $$`).
- Menuliskan berbagai notasi matematika dan fisika dalam sintaks LaTeX: pecahan, eksponen/subskrip, akar, integral, sumasi, matriks, hingga notasi Dirac bra-ket.
- Menulis persamaan matematika multi-baris sejajar menggunakan environment `\begin{aligned}`.
- Memanfaatkan Markdown + LaTeX untuk menyusun laporan tugas dan dokumentasi proyek yang rapi dan profesional di GitHub dan Jupyter Notebook.

## Prerequisites
- Materi prasyarat:
  - Tidak ada prasyarat khusus. Materi ini dirancang untuk mendukung ketiga track studi (Quantum Physics, Computer Cluster, dan Web Dev).
- Tools yang diperlukan:
  - Text editor: [Visual Studio Code](https://code.visualstudio.com/) dengan ekstensi:
    - *Markdown All in One* (oleh Yu Zhang)
    - *Markdown Preview Enhanced* (oleh Yiyi Wang)
  - Alternatif: Editor Markdown seperti [Obsidian](https://obsidian.md/), [Typora](https://typora.io/), atau langsung menggunakan [Google Colab](https://colab.research.google.com/) / Jupyter Notebook.

## Learning Materials

### 1. Apa itu Markdown & LaTeX?

| Karakteristik | Markdown (`.md`) | LaTeX (`.tex` / `$ ... $`) |
| ------------- | ---------------- | -------------------------- |
| **Tujuan Utama** | Penulisan catatan, dokumentasi, README, web content dengan cepat dan ringan. | Typesetting dokumen ilmiah, paper akademik, formula matematika, dan buku. |
| **Kemudahan** | Sangat mudah dibaca manusia (*human-readable*) bahkan dalam bentuk plain text. | Sintaks lebih kaya dan kompleks dengan kontrol presisi tinggi. |
| **Kelebihan** | Standar de-facto di GitHub, GitLab, Stack Overflow, Discord, dan Jupyter. | Standar publikasi sains (IEEE, Springer, arXiv) untuk representasi formula matematika. |

**Kombinasi Sempurna:**
Di era modern, platform seperti **GitHub**, **Jupyter Notebook**, dan berbagai static site generator mendukung **persamaan LaTeX di dalam file Markdown** menggunakan render engine matematika seperti **MathJax** atau **KaTeX**. Anda mendapatkan kecepatan dan kemudahan struktur Markdown sekaligus keindahan dan ketepatan rumus matematika LaTeX!

---

### 2. Sintaks Dasar Formatting Teks Markdown

#### A. Heading (Judul & Subjudul)
Gunakan tanda pagar `#` diikuti spasi. Semakin banyak tanda pagar, semakin kecil ukuran headingnya:
```markdown
# Heading 1 (Judul Utama)
## Heading 2 (Subjudul Section)
### Heading 3 (Sub-subjudul)
#### Heading 4
##### Heading 5
###### Heading 6
```

#### B. Penekanan Teks (Emphasis)
```markdown
*Teks miring (italic)* atau _teks miring_
**Teks tebal (bold)** atau __teks tebal__
***Teks tebal dan miring***
~~Teks dicoret (strikethrough)~~
```

#### C. List (Daftar)
```markdown
<!-- Unordered List (Daftar Tak Bernomor) -->
- Item pertama
- Item kedua
  - Sub-item A (gunakan indentasi 2 spasi atau 1 tab)
  - Sub-item B
* Opsi bullet lain menggunakan tanda bintang

<!-- Ordered List (Daftar Bernomor) -->
1. Langkah pertama
2. Langkah kedua
3. Langkah ketiga

<!-- Task List / Checkbox (Sangat populer di GitHub) -->
- [x] Tugas selesai
- [ ] Tugas belum selesai
```

#### D. Blockquote & Alert Block
```markdown
> Ini adalah kutipan (blockquote).
> Baris kedua kutipan.

<!-- GitHub Alert Blocks (Gunakan ini untuk catatan penting) -->
> [!NOTE]
> Informasi tambahan yang berguna.

> [!TIP]
> Tips dan trik efisiensi.

> [!IMPORTANT]
> Hal krusial yang wajib diperhatikan.

> [!WARNING]
> Peringatan potensi kesalahan atau bug.
```

#### E. Code Formatting
```markdown
Gunakan backtick tunggal untuk kode inline: `git status` atau variabel `x = 10`.

Untuk blok kode multi-baris, gunakan triple backticks dengan menyertakan nama bahasa:
```python
def hitung_energi(foton_nu, h=6.626e-34):
    return h * foton_nu
```
```

#### F. Link & Gambar
```markdown
<!-- Format Link: [Teks Tautan](https://example.com) -->
Kunjungi [Portal LAB COMICS](https://github.com) untuk info terbaru.

<!-- Format Gambar: ![Alt Teks Gambar](https://example.com/gambar.png) -->
![Diagram Alur](https://example.com/diagram.png)
```

#### G. Tabel
```markdown
| Nama Partikel | Simbol | Muatan (e) | Massa (kg) |
| :------------ | :----: | ---------: | :--------- |
| Elektron      | $e^-$  |         -1 | 9.109e-31  |
| Proton        | $p^+$  |         +1 | 1.672e-27  |
| Neutron       | $n^0$  |          0 | 1.675e-27  |
```
> Keterangan titik dua `:` pada pembatas kolom:
> - `:---` = rata kiri (left-aligned)
> - `:---:` = rata tengah (centered)
> - `---:` = rata kanan (right-aligned)

---

### 3. Menulis Formula Matematika LaTeX di Markdown

Di Markdown (GitHub, Jupyter, Obsidian, VS Code preview), persamaan matematika ditulis menggunakan tanda dollar:
1. **Inline Math (`$ ... $`)**: Rumus berada menyatu di dalam baris teks.
   - Contoh: Nilai konstanta Planck adalah `$h = 6.626 \times 10^{-34}\ \text{J}\cdot\text{s}$` menghasilkan: Nilai konstanta Planck adalah $h = 6.626 \times 10^{-34}\ \text{J}\cdot\text{s}$.
2. **Display / Block Math (`$$ ... $$`)**: Rumus ditampilkan tersendiri di baris baru dan rata tengah.
   ```markdown
   $$
   E = mc^2
   $$
   ```

---

### 4. Kamus Sintaks Matematika LaTeX Esensial

#### A. Pangkat, Indeks, dan Simbol Yunani
| Deskripsi | Sintaks LaTeX | Hasil Render |
| :--- | :--- | :---: |
| Pangkat / Superscript | `x^2`, `e^{-i\omega t}` | $x^2$, $e^{-i\omega t}$ |
| Indeks / Subscript | `x_0`, `a_{ij}` | $x_0$, $a_{ij}$ |
| Huruf Yunani kecil | `\alpha, \beta, \gamma, \theta, \lambda, \pi, \psi, \omega` | $\alpha, \beta, \gamma, \theta, \lambda, \pi, \psi, \omega$ |
| Huruf Yunani kapital | `\Gamma, \Delta, \Theta, \Lambda, \Psi, \Omega` | $\Gamma, \Delta, \Theta, \Lambda, \Psi, \Omega$ |
| Simbol Khusus Fisika | `\hbar, \nabla, \partial, \infty, \approx, \pm` | $\hbar, \nabla, \partial, \infty, \approx, \pm$ |

> [!TIP]
> Jika pangkat atau indeks terdiri lebih dari 1 karakter, bungkus dengan kurung kurawal `{...}`. Contoh: `x^10`, bukan `x^10` (yang menghasilkan $x^10$).

#### B. Pecahan dan Akar
```latex
\frac{pembilang}{penyebut}   % Pecahan
\sqrt{x}                     % Akar kuadrat
\sqrt[n]{x}                  % Akar pangkat n
```
Contoh:
$$
\frac{-b \pm \sqrt{b^2 - 4ac}}{2a}
$$
Dituliskan sebagai: `\frac{-b \pm \sqrt{b^2 - 4ac}}{2a}`.

#### C. Sumasi, Integral, dan Limit
```latex
\sum_{i=1}^{N} x_i           % Sumasi dari i=1 sampai N
\prod_{i=1}^{N} x_i          % Produk (perkalian berulang)
\int_{-\infty}^{\infty} f(x)\,dx   % Integral tertentu
\lim_{x \to 0} \frac{\sin x}{x}    % Limit
```

#### D. Teks di Dalam Persamaan & Spasi
LaTeX menganggap huruf biasa sebagai variabel (dicetak miring dan tanpa spasi antar kata). Gunakan `\text{...}` untuk menyisipkan teks atau satuan:
```latex
K_{\max} = h\nu - \phi \quad \text{untuk } \nu \ge \nu_0
```
Untuk mengatur spasi di LaTeX:
- `\,` (spasi tipis)
- `\quad` (spasi 1 karakter)
- `\qquad` (spasi 2 karakter)

#### E. Matriks dan Vektor
Gunakan environment `\begin{pmatrix} ... \end{pmatrix}` (kurung bulat) atau `\begin{bmatrix} ... \end{bmatrix}` (kurung siku). Baris dipisahkan dengan `\\`, kolom dipisahkan dengan `&`:

```latex
X = \begin{pmatrix}
0 & 1 \\
1 & 0
\end{pmatrix}, \quad
\vec{v} = \begin{pmatrix}
v_x \\
v_y
\end{pmatrix}
```
Hasil render:
$$
X = \begin{pmatrix}
0 & 1 \\
1 & 0
\end{pmatrix}, \quad
\vec{v} = \begin{pmatrix}
v_x \\
v_y
\end{pmatrix}
$$

#### F. Notasi Dirac Bra-Ket (Penting untuk Quantum Physics!)
Dalam mekanika kuantum, keadaan sistem ditulis dalam bra-ket:
```latex
|\psi\rangle = \alpha |0\rangle + \beta |1\rangle
\langle\phi|\psi\rangle
|\psi\rangle\langle\psi|
```
Hasil render:
$$
|\psi\rangle = \alpha |0\rangle + \beta |1\rangle, \quad \langle\phi|\psi\rangle, \quad |\psi\rangle\langle\psi|
$$

#### G. Persamaan Multi-baris Sejajar (`aligned`)
Gunakan simbol `&` sebagai titik patokan perataan (biasanya di depan tanda sama dengan `=`):
```latex
$$
\begin{aligned}
\hat{H} |\psi\rangle &= E |\psi\rangle \\
i\hbar \frac{\partial}{\partial t} |\Psi(t)\rangle &= \hat{H} |\Psi(t)\rangle
\end{aligned}
$$
```
Hasil render:
$$
\begin{aligned}
\hat{H} |\psi\rangle &= E |\psi\rangle \\
i\hbar \frac{\partial}{\partial t} |\Psi(t)\rangle &= \hat{H} |\Psi(t)\rangle
\end{aligned}
$$

---

## Guided Practice

Ikuti langkah-langkah latihan berikut di komputer Anda:

**Step 1 — Setup file di VS Code**
1. Buat folder `~/markdown-latex-practice` dan buat file `latihan.md`.
2. Buka file tersebut di VS Code.
3. Buka panel preview Markdown di VS Code dengan menekan tombol kombinasi **Ctrl+K V** (atau **Cmd+K V** di macOS).

**Step 2 — Buat struktur artikel Markdown**
Salin dan lengkapi template berikut di `latihan.md`:
```markdown
# Catatan Studi Mandiri: Fundamental Fisika Kuantum

Disusun oleh: **Nama Peserta**  
Tanggal: *12 Oktober 2026*

---

## 1. Ringkasan Topik
Pada pembelajaran minggu pertama, kita mengidentifikasi fenomena radiasi benda hitam yang melahirkan postulat Planck:
- Kuantisasi energi foton
- Efek fotolistrik Einstein
- Dualisme gelombang-partikel de Broglie

### Tabel Parameter Fisika
| Parameter | Notasi | Nilai Standar | Satuan |
| :--- | :---: | :---: | :--- |
| Kecepatan Cahaya | $c$ | $2.998 \times 10^8$ | $\text{m/s}$ |
| Konstanta Planck | $h$ | $6.626 \times 10^{-34}$ | $\text{J}\cdot\text{s}$ |
| Reduksi Planck | $\hbar$ | $1.055 \times 10^{-34}$ | $\text{J}\cdot\text{s}$ |
```

**Step 3 — Menulis persamaan LaTeX kompleks**
Tambahkan blok persamaan berikut ke dalam `latihan.md`:
```markdown
## 2. Persamaan Kunci

Persamaan radiansi spektral benda hitam menurut **Max Planck**:
$$
B_\lambda(\lambda, T) = \frac{2hc^2}{\lambda^5} \cdot \frac{1}{\exp\left(\frac{hc}{\lambda k_B T}\right) - 1}
$$

Hubungan ketidakpastian posisi dan momentum **Heisenberg**:
$$
\Delta x \cdot \Delta p \ge \frac{\hbar}{2}
$$

Representasi keadaan qubit dalam superposisi:
$$
|\psi\rangle = \begin{pmatrix} \cos\frac{\theta}{2} \\ e^{i\phi} \sin\frac{\theta}{2} \end{pmatrix}
$$
```

Amati bagaimana persamaan dirender dengan indah di panel preview!

## Assignment (Referencing ke /Assignment)

Kerjakan **[Assignment 02 — LaTeX & Markdown](../Assignment/Assignment-02-LaTeX-Markdown.md)**.

- [ ] Task 1 — Comprehensive Markdown Formatting Document
- [ ] Task 2 — Transkripsi Formula Matematika Dasar ke LaTeX
- [ ] Task 3 — Formula Saintifik & Matriks Quantum State
- [ ] Task 4 — Desain Template Laporan Teknis Terstruktur
- [ ] Task 5 — Refleksi Pembelajaran

## Self-Reflection
1. Apa konsep utama yang dipelajari?
2. Apa kesulitan yang ditemukan saat menuliskan rumus matematika di LaTeX?
3. Mengapa penulisan persamaan matematika menggunakan LaTeX di Markdown jauh lebih disukai oleh komunitas sains dan rekayasa perangkat lunak dibandingkan mengetik di Microsoft Word biasa?
4. Bagaimana Anda akan memanfaatkan Markdown dan LaTeX untuk mengumpulkan tugas-tugas di COMICS Study Group 2026?

## Further Reading
- [GitHub Flavored Markdown (GFM) Spec](https://github.github.com/gfm/) — standar resmi Markdown di GitHub.
- [KaTeX Supported Functions](https://katex.org/docs/supported.html) — daftar fungsi matematika yang didukung KaTeX (render engine di GitHub/Notion).
- [Overleaf LaTeX Mathematical Expressions](https://www.overleaf.com/learn/latex/Mathematical_expressions) — tutorial komprehensif penulisan matematika di LaTeX.
- [Mathpix Snip](https://mathpix.com/) — tool praktis untuk mengubah gambar tulisan tangan/rumus menjadi kode LaTeX secara instan.
