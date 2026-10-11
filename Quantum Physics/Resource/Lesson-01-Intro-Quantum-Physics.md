# Lesson 01 — Introduction to Quantum Physics

> 📅 **Self-study 1:** 8–14 Oktober 2026 · 💬 Dibahas pada **Meeting 1 (22 Oktober)**

## Learning Objectives

Setelah menyelesaikan materi ini, peserta mampu:

- Menjelaskan fenomena-fenomena yang **tidak dapat dijelaskan oleh fisika klasik** dan memicu lahirnya mekanika kuantum (blackbody radiation, photoelectric effect, atomic spectra).
- Menggunakan hubungan Planck–Einstein $E = h\nu$ dan panjang gelombang de Broglie $\lambda = h/p$ dalam perhitungan sederhana.
- Menjelaskan **wave–particle duality** melalui eksperimen double-slit.
- Menjelaskan konsep **wavefunction**, **Born rule** (interpretasi probabilistik), **superposition**, dan **quantization**.
- Menerapkan **Heisenberg uncertainty principle** secara kualitatif dan kuantitatif.
- Menyebutkan cabang-cabang **quantum technology** (computing, communication, sensing, simulation) dan hubungannya dengan konsep di atas.
- Menggunakan Python (NumPy, Matplotlib) untuk menghitung dan memvisualisasikan fenomena kuantum sederhana.

## Prerequisites

**Materi prasyarat**

- Fisika dasar: energi, momentum, gelombang (panjang gelombang $\lambda$, frekuensi $\nu$, $c = \lambda\nu$).
- Matematika dasar: eksponen, logaritma, notasi ilmiah, turunan sederhana.
- Python dasar (variable, fungsi, list) — *akan sangat membantu, tetapi bisa dipelajari bersamaan*.

**Tools yang diperlukan**

- Python 3.10+ dengan `numpy` dan `matplotlib`, **atau** [Google Colab](https://colab.research.google.com/) (tanpa instalasi).
- Jupyter Notebook / JupyterLab (opsional jika memakai Colab).
- Instalasi lokal: `pip install numpy matplotlib jupyter`

## Learning Materials

### 1. Krisis Fisika Klasik (± 1900)

Pada akhir abad ke-19, fisika klasik (mekanika Newton + elektromagnetisme Maxwell) dianggap hampir "selesai". Namun beberapa eksperimen menunjukkan hasil yang **tidak bisa dijelaskan**:

| Fenomena | Prediksi Klasik | Observasi | Solusi Kuantum |
| -------- | --------------- | --------- | -------------- |
| Blackbody radiation | Energi radiasi → ∞ pada panjang gelombang pendek (*ultraviolet catastrophe*) | Kurva memuncak lalu turun ke nol | Planck (1900): energi terkuantisasi $E = nh\nu$ |
| Photoelectric effect | Energi elektron bergantung pada intensitas cahaya | Bergantung pada **frekuensi**; ada frekuensi ambang | Einstein (1905): cahaya terdiri atas **foton** |
| Atomic spectra | Spektrum kontinu; atom seharusnya runtuh | Spektrum garis diskrit; atom stabil | Bohr (1913): tingkat energi diskrit |

### 2. Kuantisasi Energi — Planck

Planck mengusulkan bahwa energi osilator hanya dapat bernilai kelipatan bulat dari satu "paket" (kuantum):

$$
E = h\nu = \frac{hc}{\lambda}
$$

dengan **konstanta Planck** $h = 6.626 \times 10^{-34}\ \text{J·s}$ dan $\hbar = h / 2\pi = 1.055 \times 10^{-34}\ \text{J·s}$.

Hukum radiasi Planck (radiansi spektral benda hitam):

$$
B_\lambda(\lambda, T) = \frac{2hc^2}{\lambda^5} \cdot \frac{1}{e^{hc/(\lambda k_B T)} - 1}
$$

Bandingkan dengan prediksi klasik **Rayleigh–Jeans** $B_\lambda = \dfrac{2ck_BT}{\lambda^4}$ yang divergen saat $\lambda \to 0$.

> [!TIP]
> Konversi praktis: $hc \approx 1240\ \text{eV·nm}$. Foton dengan $\lambda = 500\ \text{nm}$ memiliki energi $1240/500 \approx 2.48\ \text{eV}$.

### 3. Foton & Photoelectric Effect — Einstein

Cahaya terdiri atas partikel energi bernama **foton**. Ketika foton menumbuk logam, elektron terlepas jika energi foton melebihi **work function** $\phi$ logam:

$$
K_{\max} = h\nu - \phi
$$

Konsekuensinya:

- Di bawah frekuensi ambang $\nu_0 = \phi / h$, **tidak ada elektron** yang terlepas — seberapa pun terangnya cahaya.
- Intensitas hanya menentukan **jumlah** elektron, bukan energinya.

### 4. Wave–Particle Duality — de Broglie

Jika gelombang (cahaya) bisa berperilaku seperti partikel, de Broglie (1924) mengusulkan sebaliknya: **partikel juga memiliki sifat gelombang**:

$$
\lambda = \frac{h}{p} = \frac{h}{mv}
$$

| Objek | Massa | Kecepatan | $\lambda$ de Broglie |
| ----- | ----- | --------- | -------------------- |
| Bola baseball | 0.145 kg | 40 m/s | $\approx 1.1 \times 10^{-34}$ m (tak teramati) |
| Elektron (100 eV) | $9.11 \times 10^{-31}$ kg | $\approx 5.9 \times 10^{6}$ m/s | $\approx 0.12$ nm (seukuran atom!) |

Inilah mengapa efek kuantum dominan di skala atomik, tetapi tidak terlihat dalam kehidupan sehari-hari.

### 5. Eksperimen Double-Slit

Eksperimen paling terkenal dalam fisika kuantum:

```text
 sumber        celah ganda          layar
 elektron        ║                  ║ ░
   ●  ─ ─ ─ ─ ─ ─║  ─ ─ ─ ─ ─ ─ ─ ─ ║ ▓
   (satu         ║                  ║ ░
   per satu)     ║                  ║ ▓   ← pola interferensi
                 ║                  ║ ░      (terbentuk perlahan
                                    ║ ▓       dari titik-titik)
```

1. Elektron ditembakkan **satu per satu** — setiap elektron tiba sebagai **satu titik** (sifat partikel).
2. Setelah ribuan elektron, titik-titik membentuk **pola interferensi** (sifat gelombang).
3. Jika kita **mengukur** celah mana yang dilewati, pola interferensi **hilang**.

Kesimpulan: sebelum diukur, elektron berada dalam **superposisi** melewati kedua celah; pengukuran mengubah sistem.

### 6. Wavefunction & Born Rule

Keadaan sistem kuantum dideskripsikan oleh **wavefunction** $\psi(x, t)$ — sebuah fungsi bernilai **kompleks**. Wavefunction sendiri tidak dapat diukur langsung, tetapi menurut **Born rule**:

$$
P(x)\,dx = |\psi(x,t)|^2\,dx
$$

adalah probabilitas menemukan partikel di antara $x$ dan $x + dx$. Karena partikel pasti ada di suatu tempat, wavefunction harus **ternormalisasi**:

$$
\int_{-\infty}^{\infty} |\psi(x,t)|^2\,dx = 1
$$

Evolusi wavefunction terhadap waktu diatur oleh **persamaan Schrödinger** (akan dibahas lebih dalam nanti):

$$
i\hbar \frac{\partial \psi}{\partial t} = \hat{H}\psi
$$

### 7. Superposition

Jika $\psi_1$ dan $\psi_2$ adalah keadaan yang valid, maka kombinasi linear

$$
\psi = c_1\psi_1 + c_2\psi_2, \qquad |c_1|^2 + |c_2|^2 = 1
$$

juga keadaan yang valid. Saat diukur, sistem akan ditemukan di keadaan 1 dengan probabilitas $|c_1|^2$ dan di keadaan 2 dengan probabilitas $|c_2|^2$.

> [!NOTE]
> Inilah ide dasar **qubit**: $|\psi\rangle = \alpha|0\rangle + \beta|1\rangle$. Notasi $|\cdot\rangle$ (Dirac/ket) akan dipelajari di Lesson 02.

### 8. Heisenberg Uncertainty Principle

Posisi dan momentum partikel **tidak dapat diketahui dengan presisi sempurna secara bersamaan**:

$$
\Delta x \, \Delta p \geq \frac{\hbar}{2}
$$

Ini **bukan** keterbatasan alat ukur, melainkan sifat fundamental alam yang muncul dari sifat gelombang partikel. Contoh: elektron yang dibatasi dalam atom ($\Delta x \sim 10^{-10}$ m) memiliki ketidakpastian momentum minimal $\Delta p \sim 5 \times 10^{-25}$ kg·m/s.

### 9. Dari Fisika Kuantum ke Quantum Technology

**First quantum revolution** (abad ke-20) memanfaatkan efek kuantum secara kolektif: transistor, laser, MRI, LED. **Second quantum revolution** (sekarang) mengontrol sistem kuantum **individual**:

| Bidang | Konsep Kunci | Contoh |
| ------ | ------------ | ------ |
| Quantum Computing | Superposition, entanglement, interference | IBM Quantum, Google Sycamore/Willow |
| Quantum Communication | No-cloning, entanglement | Quantum Key Distribution (QKD) |
| Quantum Sensing | Sensitivitas tinggi keadaan kuantum | Atomic clock, magnetometer NV-center |
| Quantum Simulation | Sistem kuantum meniru sistem kuantum lain | Simulasi molekul untuk material & obat |

## Guided Practice

Buka Jupyter Notebook atau Google Colab, lalu jalankan setiap cell berikut.

**Step 1 — Definisikan konstanta fisika**

```python
import numpy as np
import matplotlib.pyplot as plt

h    = 6.62607015e-34   # J·s
hbar = h / (2 * np.pi)
c    = 2.99792458e8     # m/s
kB   = 1.380649e-23     # J/K
e    = 1.602176634e-19  # C (juga 1 eV = e joule)
m_e  = 9.1093837e-31    # kg
```

**Step 2 — Energi foton**

```python
def photon_energy_eV(wavelength_nm):
    """Energi foton (eV) dari panjang gelombang (nm)."""
    return h * c / (wavelength_nm * 1e-9) / e

for name, lam in [("Merah", 700), ("Hijau", 530), ("Ungu", 400), ("UV-C", 254)]:
    print(f"{name:6s} {lam:4d} nm → {photon_energy_eV(lam):.2f} eV")
```

**Step 3 — Panjang gelombang de Broglie**

```python
def de_broglie(m, v):
    return h / (m * v)

# Elektron dipercepat 100 V: E = 100 eV → p = sqrt(2 m E)
E = 100 * e
p = np.sqrt(2 * m_e * E)
print(f"Elektron 100 eV : λ = {h/p*1e9:.3f} nm")
print(f"Baseball        : λ = {de_broglie(0.145, 40):.2e} m")
```

**Step 4 — Ultraviolet catastrophe: Planck vs Rayleigh–Jeans**

```python
lam = np.linspace(50e-9, 3000e-9, 1000)   # 50–3000 nm
T = 5000                                  # K

planck = (2*h*c**2 / lam**5) / (np.exp(h*c / (lam*kB*T)) - 1)
rayleigh_jeans = 2*c*kB*T / lam**4

plt.figure(figsize=(8, 5))
plt.plot(lam*1e9, planck, label="Planck (kuantum)")
plt.plot(lam*1e9, rayleigh_jeans, "--", label="Rayleigh–Jeans (klasik)")
plt.ylim(0, planck.max() * 1.5)
plt.xlabel("Panjang gelombang (nm)")
plt.ylabel(r"$B_\lambda$ (W·sr$^{-1}$·m$^{-3}$)")
plt.title(f"Radiasi Benda Hitam, T = {T} K")
plt.legend(); plt.grid(alpha=0.3)
plt.show()
```

Amati: di panjang gelombang pendek, kurva klasik meledak ke tak hingga, sedangkan kurva Planck kembali ke nol.

**Step 5 — Superposition & Born rule (simulasi pengukuran)**

```python
rng = np.random.default_rng(seed=42)

c1, c2 = np.sqrt(0.7), np.sqrt(0.3)     # |c1|^2 = 0.7, |c2|^2 = 0.3
probs = [abs(c1)**2, abs(c2)**2]

outcomes = rng.choice([1, 2], size=1000, p=probs)
print("Hasil keadaan 1:", np.sum(outcomes == 1))
print("Hasil keadaan 2:", np.sum(outcomes == 2))
```

Setiap "pengukuran" memberikan hasil acak, tetapi statistik dari banyak pengukuran mengikuti $|c_i|^2$.

**Step 6 — Eksplorasi interaktif**

Buka simulasi [PhET Quantum Wave Interference](https://phet.colorado.edu/en/simulations/quantum-wave-interference). Pilih *Single Particles*, nyalakan double slit, dan amati bagaimana pola interferensi terbentuk perlahan dari partikel-partikel individual.

## Assignment (Referencing ke /Assignment)

Kerjakan **[Assignment 01 — Introduction to Quantum Physics](../Assignment/Assignment-01-Intro-Quantum-Physics.md)**. Deadline: **14 Oktober 2026, 23:59 WIB**.

- [ ] Task 1 — Conceptual questions
- [ ] Task 2 — Perhitungan: foton, photoelectric effect, de Broglie, uncertainty
- [ ] Task 3 — Notebook: blackbody radiation & Wien's law
- [ ] Task 4 — Notebook: simulasi pengukuran superposition
- [ ] Task 5 — Mini essay: quantum technology

## Self-Reflection

1. Apa konsep utama yang dipelajari?
2. Apa kesulitan yang ditemukan?
3. Konsep mana yang paling bertentangan dengan intuisi Anda sehari-hari, dan mengapa?
4. Apa perbedaan "probabilitas" dalam mekanika kuantum dengan probabilitas pada lemparan koin biasa?
5. Apa yang ingin Anda tanyakan atau diskusikan pada Meeting 1 (22 Oktober)?

## Further Reading

- [The Feynman Lectures on Physics, Vol. III — Chapter 1: Quantum Behavior](https://www.feynmanlectures.caltech.edu/III_01.html)
- [MIT OCW 8.04 Quantum Physics I (Spring 2016)](https://ocw.mit.edu/courses/8-04-quantum-physics-i-spring-2016/) — Lecture 1–3.
- [IBM Quantum Learning — Basics of Quantum Information](https://learning.quantum.ibm.com/course/basics-of-quantum-information)
- [PhET — Quantum Wave Interference](https://phet.colorado.edu/en/simulations/quantum-wave-interference)
- [HyperPhysics — Quantum Physics](http://hyperphysics.phy-astr.gsu.edu/hbase/quacon.html#quacon)
- D. J. Griffiths & D. F. Schroeter, *Introduction to Quantum Mechanics* (3rd ed.), Chapter 1.
