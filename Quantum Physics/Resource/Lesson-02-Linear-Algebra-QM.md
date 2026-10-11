# Lesson 02 — Linear Algebra for Quantum Mechanics

> 📅 **Self-study 2:** 15–21 Oktober 2026 · 💬 Dibahas pada **Meeting 1 (22 Oktober)**

## Learning Objectives

Setelah menyelesaikan materi ini, peserta mampu:

- Melakukan operasi pada **bilangan kompleks**: konjugat, modulus, bentuk polar, dan formula Euler.
- Merepresentasikan quantum state sebagai vektor kolom di ruang $\mathbb{C}^n$ menggunakan **Dirac notation** (ket $|\psi\rangle$ dan bra $\langle\psi|$).
- Menghitung **inner product**, **norm**, dan melakukan **normalisasi** state.
- Menjelaskan konsep **basis ortonormal** dan menuliskan state dalam basis berbeda ($\{|0\rangle, |1\rangle\}$ dan $\{|+\rangle, |-\rangle\}$).
- Menggunakan matriks sebagai **operator**: perkalian matriks–vektor, **conjugate transpose** ($\dagger$), operator **Hermitian** dan **unitary**.
- Menghitung **eigenvalue** dan **eigenvector** matriks $2\times2$, khususnya **Pauli matrices**.
- Mengenal **outer product** dan **tensor product** sebagai persiapan untuk sistem multi-qubit.
- Melakukan seluruh operasi di atas menggunakan **NumPy**.

## Prerequisites

**Materi prasyarat**

- [Lesson 01 — Introduction to Quantum Physics](Lesson-01-Intro-Quantum-Physics.md): wavefunction, superposition, Born rule.
- Aljabar dasar: vektor, matriks, perkalian matriks (tingkat SMA/semester awal).

**Tools yang diperlukan**

- Python 3.10+ dengan `numpy` (dan opsional `matplotlib`), atau [Google Colab](https://colab.research.google.com/).
- Kertas dan pensil — banyak latihan sebaiknya dikerjakan manual terlebih dahulu.

## Learning Materials

### 1. Mengapa Linear Algebra?

Mekanika kuantum **adalah** linear algebra di ruang vektor kompleks:

| Konsep Fisika | Objek Matematika |
| ------------- | ---------------- |
| Quantum state | Vektor (ternormalisasi) di ruang Hilbert |
| Superposition | Kombinasi linear vektor |
| Observable (besaran terukur) | Matriks Hermitian |
| Hasil pengukuran yang mungkin | Eigenvalue |
| Evolusi waktu / quantum gate | Matriks unitary |
| Probabilitas | Kuadrat modulus inner product |
| Sistem gabungan (multi-qubit) | Tensor product |

### 2. Bilangan Kompleks

Bilangan kompleks $z = a + bi$ dengan $i^2 = -1$.

| Operasi | Definisi | Contoh untuk $z = 3 + 4i$ |
| ------- | -------- | ------------------------- |
| Konjugat | $z^* = a - bi$ | $3 - 4i$ |
| Modulus | $\lvert z \rvert = \sqrt{a^2 + b^2} = \sqrt{z z^*}$ | $5$ |
| Modulus kuadrat | $\lvert z \rvert^2 = z z^*$ | $25$ |

**Bentuk polar & formula Euler:**

$$
z = r e^{i\theta} = r(\cos\theta + i\sin\theta), \qquad r = |z|
$$

Nilai penting: $e^{i\pi/2} = i$, $e^{i\pi} = -1$, $|e^{i\theta}| = 1$ untuk semua $\theta$.

> [!NOTE]
> Faktor $e^{i\theta}$ disebut **phase**. Global phase tidak memengaruhi probabilitas pengukuran, tetapi **relative phase** antar komponen superposition sangat penting (sumber interferensi kuantum).

### 3. Vektor & Dirac Notation

State sebuah **qubit** adalah vektor di $\mathbb{C}^2$. Dalam **Dirac notation**:

- **Ket** $|\psi\rangle$ = vektor kolom
- **Bra** $\langle\psi|$ = conjugate transpose dari ket (vektor baris dengan elemen dikonjugasi)

$$
|\psi\rangle = \begin{pmatrix} \alpha \\ \beta \end{pmatrix}, \qquad
\langle\psi| = \begin{pmatrix} \alpha^* & \beta^* \end{pmatrix}
$$

**Computational basis:**

$$
|0\rangle = \begin{pmatrix} 1 \\ 0 \end{pmatrix}, \qquad
|1\rangle = \begin{pmatrix} 0 \\ 1 \end{pmatrix}, \qquad
|\psi\rangle = \alpha|0\rangle + \beta|1\rangle
$$

### 4. Inner Product, Norm, dan Normalisasi

**Inner product** (bra-ket) menghasilkan bilangan kompleks:

$$
\langle\phi|\psi\rangle = \phi_1^*\psi_1 + \phi_2^*\psi_2
$$

Sifat penting: $\langle\phi|\psi\rangle = \langle\psi|\phi\rangle^*$.

- **Norm:** $\| \psi \| = \sqrt{\langle\psi|\psi\rangle}$
- **Ternormalisasi:** $\langle\psi|\psi\rangle = |\alpha|^2 + |\beta|^2 = 1$
- **Ortogonal:** $\langle\phi|\psi\rangle = 0$
- **Normalisasi** sebuah vektor: $|\psi\rangle \to \dfrac{|\psi\rangle}{\|\psi\|}$

**Born rule dalam notasi Dirac** — probabilitas mengukur state $|\psi\rangle$ dan mendapatkan hasil yang berkaitan dengan basis $|k\rangle$:

$$
P(k) = |\langle k|\psi\rangle|^2
$$

**Contoh:** $|\psi\rangle = \frac{1}{\sqrt{3}}|0\rangle + \frac{\sqrt{2}\,i}{\sqrt{3}}|1\rangle$ → $P(0) = \frac{1}{3}$, $P(1) = \frac{2}{3}$.

### 5. Basis Ortonormal

Himpunan $\{|e_1\rangle, |e_2\rangle\}$ adalah basis ortonormal jika $\langle e_i|e_j\rangle = \delta_{ij}$. Selain computational basis, basis yang sering dipakai adalah **Hadamard basis**:

$$
|+\rangle = \frac{1}{\sqrt{2}}\begin{pmatrix} 1 \\ 1 \end{pmatrix}, \qquad
|-\rangle = \frac{1}{\sqrt{2}}\begin{pmatrix} 1 \\ -1 \end{pmatrix}
$$

State yang sama dapat dituliskan di basis berbeda. Misalnya $|0\rangle = \frac{1}{\sqrt{2}}(|+\rangle + |-\rangle)$. Hasil pengukuran bergantung pada **basis mana yang digunakan untuk mengukur**.

### 6. Matriks sebagai Operator

Operator $A$ memetakan satu state ke state lain: $|\psi'\rangle = A|\psi\rangle$.

**Perkalian matriks–vektor:**

$$
\begin{pmatrix} a & b \\ c & d \end{pmatrix}
\begin{pmatrix} x \\ y \end{pmatrix}
=
\begin{pmatrix} ax + by \\ cx + dy \end{pmatrix}
$$

> [!IMPORTANT]
> Perkalian matriks umumnya **tidak komutatif**: $AB \neq BA$. Urutan operasi (dan urutan quantum gate) sangat penting. **Commutator** didefinisikan $[A, B] = AB - BA$.

**Conjugate transpose (adjoint / dagger):** $A^\dagger = (A^*)^T$ — transpose lalu konjugasi setiap elemen.

| Jenis Operator | Syarat | Makna Fisis |
| -------------- | ------ | ----------- |
| **Hermitian** | $A^\dagger = A$ | Observable; eigenvalue selalu **real** |
| **Unitary** | $U^\dagger U = UU^\dagger = I$ | Quantum gate / evolusi waktu; **menjaga norm** (probabilitas total tetap 1) |

### 7. Pauli Matrices & Hadamard

$$
X = \sigma_x = \begin{pmatrix} 0 & 1 \\ 1 & 0 \end{pmatrix}, \quad
Y = \sigma_y = \begin{pmatrix} 0 & -i \\ i & 0 \end{pmatrix}, \quad
Z = \sigma_z = \begin{pmatrix} 1 & 0 \\ 0 & -1 \end{pmatrix}, \quad
H = \frac{1}{\sqrt{2}}\begin{pmatrix} 1 & 1 \\ 1 & -1 \end{pmatrix}
$$

Keempatnya **Hermitian sekaligus unitary**. Beberapa aksi penting:

- $X|0\rangle = |1\rangle$, $X|1\rangle = |0\rangle$ → quantum NOT gate
- $Z|0\rangle = |0\rangle$, $Z|1\rangle = -|1\rangle$ → phase flip
- $H|0\rangle = |+\rangle$, $H|1\rangle = |-\rangle$ → menciptakan superposition

### 8. Eigenvalue & Eigenvector

Vektor $|v\rangle$ adalah **eigenvector** dari $A$ dengan **eigenvalue** $\lambda$ jika:

$$
A|v\rangle = \lambda|v\rangle
$$

**Cara menghitung (matriks 2×2):**

1. Selesaikan persamaan karakteristik $\det(A - \lambda I) = 0$ untuk mendapatkan $\lambda$.
2. Untuk setiap $\lambda$, selesaikan $(A - \lambda I)|v\rangle = 0$, lalu normalisasi.

**Contoh — Pauli X:**

$$
\det\begin{pmatrix} -\lambda & 1 \\ 1 & -\lambda \end{pmatrix} = \lambda^2 - 1 = 0
\;\Rightarrow\; \lambda = \pm 1
$$

Eigenvector: $\lambda = +1 \to |+\rangle$, $\lambda = -1 \to |-\rangle$.

| Matriks | Eigenvalue | Eigenvector |
| ------- | ---------- | ----------- |
| $Z$ | $+1, -1$ | $\lvert 0\rangle, \lvert 1\rangle$ |
| $X$ | $+1, -1$ | $\lvert +\rangle, \lvert -\rangle$ |
| $Y$ | $+1, -1$ | $\lvert +i\rangle = \tfrac{1}{\sqrt2}(\lvert 0\rangle + i\lvert 1\rangle),\ \lvert -i\rangle = \tfrac{1}{\sqrt2}(\lvert 0\rangle - i\lvert 1\rangle)$ |

> [!NOTE]
> Postulat kuantum: ketika mengukur observable $A$, hasil yang mungkin **hanya** eigenvalue dari $A$, dan setelah pengukuran state "runtuh" ke eigenvector yang bersesuaian. Topik ini akan dibahas detail di **Quantum Measurement**.

### 9. Outer Product

$$
|\psi\rangle\langle\phi| = \begin{pmatrix} \psi_1 \\ \psi_2 \end{pmatrix}\begin{pmatrix} \phi_1^* & \phi_2^* \end{pmatrix} = \begin{pmatrix} \psi_1\phi_1^* & \psi_1\phi_2^* \\ \psi_2\phi_1^* & \psi_2\phi_2^* \end{pmatrix}
$$

Contoh: $|0\rangle\langle 0| = \begin{pmatrix} 1 & 0 \\ 0 & 0 \end{pmatrix}$ adalah **projector** ke $|0\rangle$. Setiap operator dapat ditulis sebagai jumlah outer product, misalnya $X = |0\rangle\langle 1| + |1\rangle\langle 0|$, dan **completeness relation** $|0\rangle\langle 0| + |1\rangle\langle 1| = I$.

### 10. Tensor Product (Preview)

Untuk menggabungkan dua qubit, digunakan **tensor (Kronecker) product** $\otimes$:

$$
|0\rangle \otimes |1\rangle = |01\rangle = \begin{pmatrix} 1 \\ 0 \end{pmatrix} \otimes \begin{pmatrix} 0 \\ 1 \end{pmatrix} = \begin{pmatrix} 0 \\ 1 \\ 0 \\ 0 \end{pmatrix}
$$

Sistem $n$ qubit hidup di ruang berdimensi $2^n$ — inilah alasan simulasi kuantum di komputer klasik menjadi sangat mahal (dan alasan quantum computer menarik).

## Guided Practice

Kerjakan setiap step secara **manual** terlebih dahulu, lalu verifikasi dengan NumPy.

**Step 1 — Bilangan kompleks**

```python
import numpy as np

z = 3 + 4j                      # Python menggunakan j untuk unit imajiner
print(z.conjugate(), abs(z), abs(z)**2)
print(np.angle(z))              # fase θ (radian)
print(np.exp(1j * np.pi))       # ≈ -1 (formula Euler)
```

**Step 2 — Ket, bra, dan normalisasi**

```python
ket0 = np.array([[1], [0]], dtype=complex)
ket1 = np.array([[0], [1]], dtype=complex)

psi = 1 * ket0 + 1j * np.sqrt(2) * ket1        # belum ternormalisasi
norm = np.sqrt((psi.conj().T @ psi).item().real)
psi = psi / norm
print("psi =", psi.ravel())
print("<psi|psi> =", (psi.conj().T @ psi).item())   # harus 1
```

> `@` adalah operator perkalian matriks di Python. `.conj().T` adalah dagger ($\dagger$).

**Step 3 — Probabilitas dengan Born rule**

```python
def prob(basis_ket, state):
    amp = (basis_ket.conj().T @ state).item()
    return abs(amp)**2

print("P(0) =", prob(ket0, psi))   # 1/3
print("P(1) =", prob(ket1, psi))   # 2/3
```

**Step 4 — Pauli matrices, Hermitian & unitary check**

```python
I = np.eye(2, dtype=complex)
X = np.array([[0, 1], [1, 0]], dtype=complex)
Y = np.array([[0, -1j], [1j, 0]], dtype=complex)
Z = np.array([[1, 0], [0, -1]], dtype=complex)
H = np.array([[1, 1], [1, -1]], dtype=complex) / np.sqrt(2)

def dag(M):
    return M.conj().T

for name, M in [("X", X), ("Y", Y), ("Z", Z), ("H", H)]:
    print(name,
          "Hermitian:", np.allclose(dag(M), M),
          "| Unitary:", np.allclose(dag(M) @ M, I))
```

**Step 5 — Aksi gate & non-komutativitas**

```python
print("H|0> =", (H @ ket0).ravel())       # |+>
print("XZ == ZX ?", np.allclose(X @ Z, Z @ X))
print("[X, Z] =\n", X @ Z - Z @ X)        # = -2iY
```

**Step 6 — Eigenvalue & eigenvector**

```python
vals, vecs = np.linalg.eigh(X)    # eigh khusus untuk matriks Hermitian
print("Eigenvalues:", vals)
print("Eigenvectors (kolom):\n", vecs)
```

Perhatikan bahwa eigenvector dari NumPy bisa berbeda **global phase** (misal dikali $-1$) dari hasil manual — keduanya sama-sama benar.

**Step 7 — Outer & tensor product**

```python
proj0 = ket0 @ dag(ket0)
print("|0><0| =\n", proj0.real)
print("Completeness:", np.allclose(ket0 @ dag(ket0) + ket1 @ dag(ket1), I))

ket01 = np.kron(ket0, ket1)
print("|01> =", ket01.ravel().real)
```

## Assignment (Referencing ke /Assignment)

Kerjakan **[Assignment 02 — Linear Algebra for Quantum Mechanics](../Assignment/Assignment-02-Linear-Algebra-QM.md)**. Deadline: **21 Oktober 2026, 23:59 WIB**.

- [ ] Task 1 — Bilangan kompleks
- [ ] Task 2 — State, inner product, & normalisasi
- [ ] Task 3 — Operator: Hermitian, unitary, commutator
- [ ] Task 4 — Eigenvalue & eigenvector
- [ ] Task 5 — Notebook: mini quantum toolkit dengan NumPy

## Self-Reflection

1. Apa konsep utama yang dipelajari?
2. Apa kesulitan yang ditemukan?
3. Mengapa quantum gate harus berupa matriks unitary? Apa yang terjadi pada probabilitas jika tidak?
4. Bagaimana Anda menjelaskan hubungan antara eigenvalue dan hasil pengukuran kepada teman yang belum belajar materi ini?
5. Apa yang ingin Anda tanyakan atau diskusikan pada Meeting 1 (22 Oktober)?

## Further Reading

- [3Blue1Brown — Essence of Linear Algebra (video series)](https://www.3blue1brown.com/topics/linear-algebra) — intuisi visual vektor, matriks, eigenvector.
- [IBM Quantum Learning — Basics of Quantum Information: Single Systems](https://learning.quantum.ibm.com/course/basics-of-quantum-information)
- [Quantum Country — Quantum Computing for the Very Curious](https://quantum.country/qcvc) — Dirac notation & gate dengan spaced repetition.
- [NumPy — Absolute Beginner's Guide](https://numpy.org/doc/stable/user/absolute_beginners.html)
- [NumPy Linear Algebra (`numpy.linalg`)](https://numpy.org/doc/stable/reference/routines.linalg.html)
- M. A. Nielsen & I. L. Chuang, *Quantum Computation and Quantum Information*, Section 2.1 (Linear Algebra).
