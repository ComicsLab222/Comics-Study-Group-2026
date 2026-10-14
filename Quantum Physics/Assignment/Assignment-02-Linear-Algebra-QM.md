# Assignment 02 — Linear Algebra for Quantum Mechanics

> 📅 **Periode:** 15–21 Oktober 2026 · ⏰ **Deadline:** 21 Oktober 2026, 23:59 WIB
> 📚 **Materi terkait:** [Lesson 02 — Linear Algebra for Quantum Mechanics](../Resource/Lesson-02-Linear-Algebra-QM.md)

## Tujuan

Assignment ini melatih kelancaran Anda dalam "bahasa" mekanika kuantum: bilangan kompleks, Dirac notation, operator, dan eigenproblem — baik secara manual maupun komputasional. Kemampuan ini adalah fondasi untuk materi **Qubit & Quantum State** setelah Meeting 1.

## Deliverables

Upload deliverables ke repository GitHub masing-masing dengan ketentuan:
- **Format nama repository:** `<nama>-CSG-2026` (contoh: `budi-CSG-2026`; CSG = *Comics Study Group*).
- **README.md:** Wajib menyertakan file `README.md` pada root repository yang berisi deskripsi repository (format dibebaskan).
- **Struktur folder:** Masukkan deliverables ke dalam folder:

```text
assignment-02/
├── answers.md / answers.pdf    ← Task 1–4 (tulisan tangan yang di-scan diperbolehkan)
└── qtoolkit.ipynb              ← Task 5 (notebook yang sudah dijalankan)
```

> [!IMPORTANT]
> Task 1–4 **wajib dikerjakan manual** dengan langkah lengkap. Anda boleh memverifikasi jawaban dengan NumPy, tetapi nilai diberikan pada langkah penyelesaian.

---

## Task 1 — Bilangan Kompleks

Diberikan $z_1 = 1 + i$ dan $z_2 = \sqrt{3} - i$.

1. Hitung $z_1 + z_2$, $z_1 z_2$, $z_1^*$, dan $z_1 / z_2$.
2. Hitung $|z_1|$, $|z_2|$, dan $|z_1 z_2|$. Verifikasi bahwa $|z_1 z_2| = |z_1||z_2|$.
3. Tuliskan $z_1$ dan $z_2$ dalam bentuk polar $re^{i\theta}$.
4. Gunakan bentuk polar untuk menghitung $z_1^{8}$.
5. Tunjukkan bahwa $|e^{i\theta}|^2 = 1$ untuk sembarang $\theta$ real.

## Task 2 — State, Inner Product, & Normalisasi

Diberikan state (belum tentu ternormalisasi):

$$
|a\rangle = \begin{pmatrix} 1 \\ 2i \end{pmatrix}, \qquad
|b\rangle = \begin{pmatrix} 2 \\ -i \end{pmatrix}, \qquad
|c\rangle = \frac{1}{2}|0\rangle + \frac{\sqrt{3}}{2}e^{i\pi/4}|1\rangle
$$

1. Tuliskan $\langle a|$ dan $\langle b|$.
2. Hitung $\langle a|b\rangle$ dan $\langle b|a\rangle$. Verifikasi bahwa $\langle a|b\rangle = \langle b|a\rangle^*$.
3. Apakah $|a\rangle$ dan $|b\rangle$ ortogonal?
4. Normalisasi $|a\rangle$ dan $|b\rangle$.
5. Apakah $|c\rangle$ sudah ternormalisasi? Hitung $P(0)$ dan $P(1)$ jika $|c\rangle$ diukur di computational basis.
6. Tuliskan $|c\rangle$ dalam **Hadamard basis** $\{|+\rangle, |-\rangle\}$, lalu hitung $P(+)$ dan $P(-)$.
7. Buktikan bahwa $\{|+\rangle, |-\rangle\}$ adalah basis ortonormal.

## Task 3 — Operator: Hermitian, Unitary, Commutator

Diberikan matriks:

$$
A = \begin{pmatrix} 2 & 1 - i \\ 1 + i & 3 \end{pmatrix}, \qquad
S = \begin{pmatrix} 1 & 0 \\ 0 & i \end{pmatrix}, \qquad
B = \begin{pmatrix} 1 & 1 \\ 0 & 1 \end{pmatrix}
$$

1. Hitung $A^\dagger$, $S^\dagger$, dan $B^\dagger$.
2. Tentukan mana yang Hermitian, mana yang unitary (boleh keduanya atau tidak sama sekali). Tunjukkan perhitungannya.
3. Hitung $S|+\rangle$. State apa yang dihasilkan? *(Hint: bandingkan dengan eigenvector Pauli Y.)*
4. Hitung $HZH$ dan $HXH$, dengan $H$ adalah Hadamard. Apa yang Anda amati?
5. Hitung commutator $[X, Y]$ dan nyatakan hasilnya dalam bentuk kelipatan salah satu Pauli matrix.
6. Tunjukkan bahwa $X^2 = Y^2 = Z^2 = I$.
7. Mengapa $B$ **tidak bisa** menjadi quantum gate? Tunjukkan dengan contoh state ternormalisasi yang norm-nya berubah setelah dikenai $B$.

## Task 4 — Eigenvalue & Eigenvector

1. Hitung eigenvalue dan eigenvector ternormalisasi dari **Pauli Y** secara manual.
2. Hitung eigenvalue dan eigenvector ternormalisasi dari matriks $A$ pada Task 3. Apakah eigenvalue-nya real? Mengapa hal ini sudah dapat diprediksi?
3. Verifikasi bahwa kedua eigenvector dari $A$ saling ortogonal.
4. Hitung eigenvalue dari Hadamard $H$.
5. Tuliskan Pauli Z dalam bentuk **outer product**: $Z = \sum_k \lambda_k |v_k\rangle\langle v_k|$ (*spectral decomposition*).

## Task 5 — Notebook: Mini Quantum Toolkit dengan NumPy

Buat notebook `qtoolkit.ipynb` berisi fungsi-fungsi berikut. Setiap fungsi harus memiliki **docstring** dan minimal satu **test** menggunakan `assert` atau `np.allclose`.

| Fungsi | Deskripsi |
| ------ | --------- |
| `ket(*amps)` | Membuat vektor kolom kompleks dari daftar amplitudo |
| `dag(M)` | Conjugate transpose |
| `inner(a, b)` | Inner product $\langle a\|b\rangle$ |
| `normalize(psi)` | Mengembalikan state ternormalisasi |
| `is_hermitian(M)` | `True` jika $M^\dagger = M$ |
| `is_unitary(M)` | `True` jika $M^\dagger M = I$ |
| `probabilities(psi, basis)` | Daftar probabilitas pengukuran untuk sebuah basis (list of kets) |
| `measure(psi, basis, shots)` | Simulasi `shots` kali pengukuran, mengembalikan dictionary hitungan |

Kemudian gunakan toolkit Anda untuk:

1. Memverifikasi jawaban Task 2 (no. 2, 4, 5, 6), Task 3 (no. 2, 4, 5), dan Task 4 (no. 1, 2).
2. Mulai dari $|0\rangle$, terapkan $H$, lalu ukur di **computational basis** dan **Hadamard basis** masing-masing 1000 kali. Tampilkan hasilnya dalam bar chart dan jelaskan perbedaannya.
3. Ulangi no. 2 untuk state $S H |0\rangle$. Jelaskan mengapa hasil pengukuran di computational basis sama dengan no. 2, padahal state-nya berbeda.
4. Buat state 2-qubit $|+\rangle \otimes |0\rangle$ menggunakan `np.kron` dan hitung probabilitas keempat hasil pengukuran $|00\rangle, |01\rangle, |10\rangle, |11\rangle$.

---

## Bonus (Opsional)

1. Buat fungsi `random_state()` yang menghasilkan state qubit acak ternormalisasi, lalu verifikasi secara numerik bahwa untuk 1000 state acak, $\|U|\psi\rangle\| = 1$ untuk $U \in \{X, Y, Z, H, S\}$.
2. Representasikan state qubit pada **Bloch sphere**: tunjukkan bahwa setiap state dapat ditulis $|\psi\rangle = \cos\frac{\theta}{2}|0\rangle + e^{i\phi}\sin\frac{\theta}{2}|1\rangle$ dan hitung $(\theta, \phi)$ untuk $|0\rangle, |1\rangle, |+\rangle, |-\rangle, |+i\rangle, |-i\rangle$.

## Rubrik Penilaian

| Komponen | Bobot |
| -------- | ----- |
| Task 1 — Bilangan kompleks | 10% |
| Task 2 — State & inner product | 20% |
| Task 3 — Operator | 20% |
| Task 4 — Eigenproblem | 20% |
| Task 5 — Quantum toolkit notebook (kebenaran, test, kerapian kode) | 30% |
| Bonus | +10% |
