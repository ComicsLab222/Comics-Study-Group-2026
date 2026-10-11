# Assignment 01 — Linux Fundamental

> 📅 **Periode:** 8–14 Oktober 2026 · ⏰ **Deadline:** 14 Oktober 2026, 23:59 WIB
> 📚 **Materi terkait:** [Lesson 01 — Linux Fundamental](../Resource/Lesson-01-Linux-Fundamental.md)

## Tujuan

Assignment ini menguji kemampuan Anda menggunakan Linux melalui command line: navigasi filesystem, manipulasi file, dan pengaturan permission. Seluruh task **wajib dikerjakan melalui terminal**, bukan file explorer.

## Deliverables

Kumpulkan dalam satu folder `assignment-01/` (lihat [aturan pengumpulan](README.md#cara-pengumpulan)):

```text
assignment-01/
├── answers.md          ← jawaban seluruh task
├── sysinfo.txt         ← output Task 1
├── structure.txt       ← output Task 3
└── command_log.txt     ← riwayat command Task 5
```

---

## Task 1 — Environment Setup & System Information

Siapkan environment Linux (WSL2/VM/native). Lalu jalankan command berikut dan simpan **semua output** ke file `sysinfo.txt`:

```bash
{ whoami; hostname; uname -a; cat /etc/os-release; echo "HOME=$HOME"; echo "SHELL=$SHELL"; } > sysinfo.txt
```

Di `answers.md`, jawab:

1. Distro dan versi apa yang Anda gunakan?
2. Versi kernel berapa yang berjalan?
3. Shell default apa yang Anda pakai?

## Task 2 — Filesystem Exploration

Gunakan `ls`, `cd`, `cat`, `head`, `file`, dan `man` untuk menjawab pertanyaan berikut di `answers.md`. Sertakan **command yang Anda gunakan** untuk tiap jawaban.

1. Apa isi file `/etc/hostname`? Apakah sama dengan output `hostname`?
2. Sebutkan 5 direktori di `/` beserta fungsinya masing-masing (dengan kata-kata Anda sendiri).
3. Berapa jumlah file/direktori (termasuk hidden) di home directory Anda? *(Hint: `ls -A | wc -l`)*
4. Di mana lokasi program `ls` dan `python3` pada filesystem? Apakah `cd` juga berupa program? *(Hint: `which`, `type`)*
5. Apa yang terjadi ketika Anda menjalankan `cd` tanpa argumen? Dan `cd -`?
6. Apa fungsi option `-h` pada `ls -lh` dan `-p` pada `mkdir -p`? Tuliskan bagian dari `man` yang menjelaskannya.

## Task 3 — Membangun Struktur Direktori Project

Buat struktur direktori berikut **di dalam home directory** menggunakan sesedikit mungkin command (target: ≤ 5 command untuk pembuatan direktori & file).

```text
~/cluster-project/
├── README.md
├── data/
│   ├── raw/
│   │   ├── sample_01.csv
│   │   ├── sample_02.csv
│   │   └── sample_03.csv
│   └── processed/
├── scripts/
│   └── run.sh
├── results/
└── logs/
```

Kemudian:

1. Isi `README.md` dengan satu baris: `Cluster project by <nama Anda>` menggunakan `echo` dan redirection `>`.
2. Copy `data/raw/sample_01.csv` ke `data/processed/` dan rename menjadi `sample_01_clean.csv`.
3. Pindahkan (move) `data/raw/sample_03.csv` ke `results/`.
4. Hapus direktori `logs/` (pastikan kosong).
5. Simpan struktur akhir ke `structure.txt`:

   ```bash
   cd ~/cluster-project && (tree 2>/dev/null || ls -R) > ~/structure.txt
   ```

Di `answers.md`, tuliskan **seluruh command** yang Anda gunakan untuk Task 3 secara berurutan.

> [!TIP]
> Gunakan **brace expansion**: `mkdir -p a/{b,c}` dan `touch file_{01..03}.txt`.

## Task 4 — File Permission Challenge

Kerjakan di direktori `~/cluster-project/`:

1. Tampilkan permission `scripts/run.sh` dengan `ls -l`. Tuliskan permission awalnya dan jelaskan arti tiap karakter.
2. Isi `run.sh` dengan:

   ```bash
   echo '#!/bin/bash' > scripts/run.sh
   echo 'echo "Job started on $(hostname) at $(date)"' >> scripts/run.sh
   ```

   Coba jalankan `./scripts/run.sh`. Apa error yang muncul dan mengapa?
3. Ubah permission sehingga **hanya owner** yang bisa read, write, dan execute; group dan others **tidak memiliki akses apa pun**. Tuliskan command dalam notasi **oktal** dan **simbolik**.
4. Jalankan kembali script tersebut dan tempelkan output-nya.
5. Konversi permission berikut (isi tabel di `answers.md`):

   | Simbolik    | Oktal |
   | ----------- | ----- |
   | `rw-r--r--` | ?     |
   | `rwxr-x---` | ?     |
   | ?           | `644` |
   | ?           | `700` |
   | ?           | `775` |

6. Buat sebuah direktori `secret/`, lalu hapus permission `x` untuk owner (`chmod u-x secret`). Coba `cd secret` dan `ls secret`. Jelaskan perbedaan hasilnya. Kembalikan permission setelah selesai.

## Task 5 — Command Log & Reflection

1. Simpan riwayat command Anda selama mengerjakan assignment:

   ```bash
   history > ~/command_log.txt
   ```

2. Di bagian akhir `answers.md`, jawab pertanyaan **Self-Reflection** dari Lesson 01 (minimal 3–5 kalimat per pertanyaan).

---

## Bonus (Opsional)

Selesaikan [OverTheWire: Bandit](https://overthewire.org/wargames/bandit/) **Level 0 → Level 5**. Catat command kunci yang Anda gunakan di setiap level (jangan tuliskan password-nya).

## Rubrik Penilaian

| Komponen | Bobot |
| -------- | ----- |
| Task 1 — Environment & system info | 10% |
| Task 2 — Filesystem exploration | 20% |
| Task 3 — Struktur direktori (efisiensi command & hasil akhir benar) | 25% |
| Task 4 — Permission | 25% |
| Task 5 — Command log & refleksi | 20% |
| Bonus — Bandit | +10% |
