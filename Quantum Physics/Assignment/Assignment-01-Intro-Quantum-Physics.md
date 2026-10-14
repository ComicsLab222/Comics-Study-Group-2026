# Assignment 01 — Introduction to Quantum Physics

> 📅 **Periode:** 8–14 Oktober 2026 · ⏰ **Deadline:** 14 Oktober 2026, 23:59 WIB
> 📚 **Materi terkait:** [Lesson 01 — Introduction to Quantum Physics](../Resource/Lesson-01-Intro-Quantum-Physics.md)

## Tujuan

Assignment ini menguji pemahaman konseptual Anda terhadap fondasi fisika kuantum, kemampuan melakukan perhitungan sederhana, serta kemampuan menggunakan Python untuk memvisualisasikan dan mensimulasikan fenomena kuantum.

## Deliverables

Upload deliverables ke repository GitHub masing-masing dengan ketentuan:
- **Format nama repository:** `<nama>-CSG-2026` (contoh: `budi-CSG-2026`; CSG = *Comics Study Group*).
- **README.md:** Wajib menyertakan file `README.md` pada root repository yang berisi deskripsi repository (format dibebaskan).
- **Struktur folder:** Masukkan deliverables ke dalam folder:

```text
assignment-01/
├── answers.md                  ← Task 1 & 2 (boleh juga PDF hasil tulisan tangan yang di-scan)
├── assignment01.ipynb          ← Task 3 & 4 (notebook yang sudah dijalankan, output terlihat)
└── slides.pdf / presentation.* ← Task 5 (slide deck wrap up/resume presentasi penjelasan Task 1–4)
```

**Konstanta yang digunakan:**
$h = 6.626 \times 10^{-34}$ J·s · $\hbar = 1.055 \times 10^{-34}$ J·s · $c = 3.00 \times 10^{8}$ m/s · $e = 1.602 \times 10^{-19}$ C · $m_e = 9.109 \times 10^{-31}$ kg · $m_n = 1.675 \times 10^{-27}$ kg · $k_B = 1.381 \times 10^{-23}$ J/K

---

## Task 1 — Conceptual Questions

Jawab dengan kata-kata Anda sendiri (3–6 kalimat per soal).

1. Apa yang dimaksud dengan *ultraviolet catastrophe*, dan bagaimana hipotesis Planck menyelesaikannya?
2. Dalam photoelectric effect, mengapa menaikkan **intensitas** cahaya merah tidak membuat elektron terlepas dari logam, sedangkan cahaya ultraviolet redup dapat melakukannya?
3. Jelaskan apa yang terjadi pada eksperimen double-slit jika elektron ditembakkan satu per satu, dan apa yang berubah jika kita memasang detektor di salah satu celah.
4. Wavefunction $\psi$ bernilai kompleks dan tidak dapat diukur langsung. Lalu besaran apa yang memiliki makna fisis, dan apa artinya?
5. Seorang teman berkata: *"Uncertainty principle muncul karena alat ukur kita belum cukup canggih."* Apakah pernyataan ini benar? Jelaskan.
6. Mengapa kita tidak melihat efek interferensi saat melempar bola melalui dua pintu?

## Task 2 — Perhitungan

Tuliskan langkah penyelesaian, bukan hanya jawaban akhir. Sertakan satuan.

1. **Energi foton.** Sebuah laser pointer merah memancarkan cahaya $\lambda = 650$ nm dengan daya 5 mW.
   - (a) Berapa energi satu foton dalam joule dan eV?
   - (b) Berapa jumlah foton yang dipancarkan per detik?
2. **Photoelectric effect.** Natrium memiliki work function $\phi = 2.28$ eV.
   - (a) Berapa panjang gelombang ambang (threshold) untuk natrium?
   - (b) Jika disinari cahaya $\lambda = 400$ nm, berapa energi kinetik maksimum elektron yang terlepas (dalam eV)?
   - (c) Berapa stopping potential yang diperlukan untuk menghentikan elektron tersebut?
   - (d) Apakah cahaya $\lambda = 600$ nm dapat melepaskan elektron? Jelaskan.
3. **de Broglie wavelength.**
   - (a) Pada eksperimen Davisson–Germer (1927), elektron dipercepat dengan beda potensial 54 V. Hitung panjang gelombang de Broglie-nya.
   - (b) Hitung panjang gelombang de Broglie neutron termal yang bergerak dengan kecepatan 2200 m/s.
   - (c) Bandingkan hasil (a) dan (b) dengan jarak antar-atom pada kristal ($\sim 0.1$–$0.3$ nm). Apa implikasinya?
4. **Uncertainty principle.**
   - (a) Sebuah elektron dibatasi dalam daerah selebar 1 nm. Hitung ketidakpastian minimum momentum dan kecepatannya.
   - (b) Lakukan perhitungan yang sama untuk sebuah debu bermassa $10^{-9}$ kg yang posisinya diketahui dengan ketelitian 1 µm. Bandingkan dan beri komentar.

## Task 3 — Notebook: Blackbody Radiation & Wien's Law

Buat notebook `assignment01.ipynb` dan kerjakan:

1. Tulis fungsi `planck(lam, T)` yang mengembalikan $B_\lambda(\lambda, T)$.
2. Plot kurva Planck untuk $T = 3000, 4000, 5000, 5800, 7000$ K dalam satu grafik ($\lambda$ = 100–3000 nm). Beri label, judul, dan legend yang jelas.
3. Arsir/tandai rentang cahaya tampak (380–750 nm) pada grafik (*hint:* `plt.axvspan`).
4. Untuk setiap temperatur, temukan $\lambda_{\max}$ secara **numerik** (*hint:* `np.argmax`).
5. Verifikasi **Wien's displacement law** $\lambda_{\max} T = b$ dengan menghitung $b$ dari data Anda dan bandingkan dengan nilai teoritis $b = 2.898 \times 10^{-3}$ m·K. Hitung persentase error-nya.
6. Matahari memiliki suhu permukaan $\approx 5800$ K. Di bagian spektrum mana puncak radiasinya? Kaitkan dengan fakta bahwa mata manusia paling sensitif terhadap cahaya hijau-kuning.

## Task 4 — Notebook: Simulasi Pengukuran Superposition

Sebuah sistem kuantum berada dalam superposisi tiga keadaan:

$$
\psi = c_1\psi_1 + c_2\psi_2 + c_3\psi_3, \qquad c_1 = \tfrac{1}{2},\quad c_2 = \tfrac{1}{\sqrt{2}},\quad c_3 = \tfrac{i}{2}
$$

1. Tunjukkan (secara analitis dan dengan Python) bahwa keadaan ini ternormalisasi.
2. Hitung probabilitas teoritis mendapatkan masing-masing keadaan saat diukur.
3. Simulasikan $N$ pengukuran menggunakan `np.random.default_rng().choice` untuk $N = 10, 100, 1000, 10000$.
4. Buat bar chart yang membandingkan frekuensi relatif hasil simulasi dengan probabilitas teoritis untuk setiap $N$.
5. Plot bagaimana frekuensi relatif keadaan 2 **konvergen** ke nilai teoritis seiring bertambahnya jumlah pengukuran (sumbu-x log scale).
6. Jika $c_3$ diubah menjadi $-\tfrac{1}{2}$ (tanpa $i$), apakah probabilitasnya berubah? Apa yang dapat Anda simpulkan tentang **fase** koefisien?

## Task 5 — Wrap Up Presentation: Resume & Explanation (Slides)

Buat presentasi singkat (resume / wrap up) dalam format slide deck (PDF, PPTX, Google Slides link, dsb.) yang merangkum serta menjelaskan kembali intisari pemahaman Anda dari pengerjaan **Task 1 sampai Task 4**. 

Struktur dan jumlah slide **dibebaskan** (tidak dibatasi secara kaku per-slide).

> 💡 *Tips:* Utamakan penyampaian visual yang komunikatif, sertakan grafik/tangkapan visual dari notebook Anda, dan sampaikan kesimpulan secara lugas.

---

## Bonus (Opsional)

Gunakan simulasi [PhET Quantum Wave Interference](https://phet.colorado.edu/en/simulations/quantum-wave-interference). Ambil screenshot pola interferensi untuk (a) foton dan (b) elektron dengan double slit. Ubah kecepatan elektron dan jelaskan bagaimana jarak antar-pita interferensi berubah, kaitkan dengan $\lambda = h/p$.

## Rubrik Penilaian

| Komponen | Bobot |
| -------- | ----- |
| Task 1 — Conceptual questions | 20% |
| Task 2 — Perhitungan (langkah, satuan, hasil) | 25% |
| Task 3 — Blackbody notebook | 20% |
| Task 4 — Superposition simulation | 20% |
| Task 5 — Wrap up presentation (slides) | 15% |
| Bonus — PhET exploration | +10% |
