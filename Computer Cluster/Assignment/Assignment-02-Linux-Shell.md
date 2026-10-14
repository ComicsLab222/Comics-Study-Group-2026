# Assignment 02 — Linux & Shell

> 📅 **Periode:** 15–21 Oktober 2026 · ⏰ **Deadline:** 21 Oktober 2026, 23:59 WIB
> 📚 **Materi terkait:** [Lesson 02 — Linux & Shell](../Resource/Lesson-02-Linux-Shell.md)

## Tujuan

Assignment ini melatih kemampuan Anda mengombinasikan command dengan pipe & redirection untuk mengolah data, mengonfigurasi shell, dan menulis bash script yang rapi dan dapat digunakan ulang — fondasi penting sebelum menulis SLURM job script.

## Dataset

Gunakan file [`data/cluster_jobs.log`](data/cluster_jobs.log) — log simulasi 60 job yang berjalan di sebuah cluster. Format tiap baris:

```text
<tanggal> <jam> <LEVEL> <node> job_id=<id> user=<user> status=<STATUS> runtime=<detik>
2026-10-15 08:44:44 INFO node04 job_id=10002 user=citra status=COMPLETED runtime=2922
```

Copy file tersebut ke environment Linux Anda. Jika Anda menggunakan WSL dan repository ada di drive Windows (misal `D:\`), file dapat diakses dari `/mnt/d/...`:

```bash
mkdir -p ~/assignment-02 && cd ~/assignment-02
cp "/mnt/d/LAB COMICS/Study Group 2026/Computer Cluster/Assignment/data/cluster_jobs.log" .
```

## Deliverables

Upload deliverables ke repository GitHub masing-masing dengan ketentuan:
- **Format nama repository:** `<nama>-CSG-2026` (contoh: `budi-CSG-2026`; CSG = *Comics Study Group*).
- **README.md:** Wajib menyertakan file `README.md` pada root repository yang berisi deskripsi repository (format dibebaskan).
- **Struktur folder:** Masukkan deliverables ke dalam folder:

```text
assignment-02/
├── answers.md          ← jawaban + command untuk Task 1–3
├── bashrc_snippet.txt  ← potongan konfigurasi Task 3
├── sysreport.sh        ← Task 4
├── organize.sh         ← Task 5
└── sweep_tree.txt      ← output Task 5
```

---

## Task 1 — Redirection & Pipe Drill

Tuliskan **satu baris command** untuk masing-masing soal berikut, beserta output-nya, di `answers.md`.

1. Simpan daftar isi direktori `/etc` (long format) ke `etc_list.txt`, lalu **tambahkan** tanggal saat ini ke akhir file yang sama.
2. Jalankan `ls /etc /folder-palsu` sehingga output normal masuk ke `out.txt` dan pesan error masuk ke `err.txt`.
3. Jalankan command yang sama, tetapi gabungkan stdout dan stderr ke `all.txt`.
4. Hitung berapa banyak file di `/usr/bin` yang namanya diawali huruf `p`.
5. Jelaskan perbedaan `cmd > file 2>&1` dan `cmd 2>&1 > file`. Uji keduanya dan tunjukkan hasilnya.

## Task 2 — Log Analysis Pipeline

Gunakan **hanya** command line tools (`grep`, `cut`, `sort`, `uniq`, `wc`, `awk`, `head`, `tail`, `tr`, `sed`) — tanpa Python/Excel. Untuk setiap soal, tulis command (boleh multi-pipe) dan hasilnya.

1. Berapa total job dalam log?
2. Berapa job dengan status `COMPLETED`, `FAILED`, `TIMEOUT`, dan `CANCELLED`? *(satu command untuk semuanya)*
3. Ada berapa **user unik**? Sebutkan.
4. Node mana yang menjalankan job terbanyak? Tampilkan jumlah job per node, urut dari terbanyak.
5. Siapa user dengan job **gagal** (`FAILED` + `TIMEOUT`) terbanyak?
6. Berapa **rata-rata runtime** (dalam detik dan menit) dari job yang `COMPLETED`?
7. Tampilkan 5 job `COMPLETED` dengan runtime **terlama** (job_id, user, runtime).
8. Pada jam berapa (00–23) paling banyak job tercatat?
9. Simpan semua baris berlevel `ERROR` ke file `errors_only.log`, lalu tampilkan jumlah barisnya.

> [!TIP]
> Untuk mengambil nilai dari `key=value`, kombinasikan `cut -d'=' -f2` atau gunakan `awk`, misalnya:
> `awk '{split($7, a, "="); print a[2]}'`. Uji pipeline secara bertahap — tambahkan satu `| command` setiap kali dan periksa output-nya.

## Task 3 — Konfigurasi Shell

1. Backup `~/.bashrc` Anda terlebih dahulu.
2. Tambahkan ke `~/.bashrc`:
   - Minimal **3 alias** yang menurut Anda berguna (contoh: `ll`, `..`, `cls`).
   - Sebuah environment variable `COMICS_HOME` yang menunjuk ke `~/comics-sg`.
   - Direktori `~/bin` ke dalam `PATH`.
3. Jalankan `source ~/.bashrc` lalu buktikan konfigurasi bekerja: `alias`, `echo $COMICS_HOME`, `echo $PATH`.
4. Salin bagian yang Anda tambahkan ke `bashrc_snippet.txt`.
5. Di `answers.md`, jelaskan: mengapa variable perlu di-`export`? Apa yang terjadi jika `~/bin` diletakkan **di akhir** vs **di awal** `PATH`?

## Task 4 — Bash Script: `sysreport.sh`

Buat script `sysreport.sh` yang menghasilkan laporan singkat kondisi sistem.

**Spesifikasi:**

- Memiliki shebang dan `set -euo pipefail`.
- Menerima argument opsional: nama file output. Default: `report_<YYYY-MM-DD>.txt`.
- Laporan berisi minimal:
  - Username, hostname, tanggal & jam
  - Distro dan versi kernel
  - Jumlah CPU core (`nproc`)
  - Penggunaan memory (`free -h`)
  - Penggunaan disk home directory (`df -h ~`)
  - 5 process yang paling banyak menggunakan memory (`ps aux --sort=-%mem | head -n 6`)
- Menampilkan pesan `Report saved to <file>` di akhir.
- Jika file output sudah ada, tampilkan peringatan ke **stderr** dan keluar dengan exit code `1`.

**Contoh penggunaan:**

```bash
./sysreport.sh
./sysreport.sh my_report.txt
./sysreport.sh my_report.txt   # dijalankan kedua kali → peringatan + exit 1
echo $?
```

## Task 5 — Bash Script: `organize.sh` (Simulasi Parameter Sweep)

Di cluster, kita sering menjalankan program yang sama dengan banyak kombinasi parameter (**parameter sweep**). Buat script `organize.sh` yang menyiapkan struktur direktori untuk eksperimen tersebut.

**Spesifikasi:**

- Penggunaan: `./organize.sh <nama_eksperimen> <jumlah_run>`
- Validasi input:
  - Jika argument kurang dari 2 → tampilkan usage ke stderr dan `exit 1`.
  - Jika `<jumlah_run>` bukan bilangan bulat positif → error dan `exit 2`.
- Untuk setiap nilai `temperature` di `{100, 200, 300}` dan setiap run `1..N`, buat direktori:

  ```text
  <nama_eksperimen>/T<temperature>/run_<nn>/
  ```

  dengan `nn` berformat 2 digit (`01`, `02`, ...). *(Hint: `printf "%02d" $i`)*
- Di setiap direktori run, buat file `params.txt` berisi:

  ```text
  experiment=<nama_eksperimen>
  temperature=<temperature>
  run=<nn>
  created=<timestamp>
  ```

- Di akhir, tampilkan ringkasan: jumlah direktori dan file `params.txt` yang dibuat (gunakan `find ... | wc -l`).

**Uji script:**

```bash
./organize.sh sweep_test 3
(tree sweep_test 2>/dev/null || find sweep_test) > sweep_tree.txt
cat sweep_test/T200/run_02/params.txt
./organize.sh                 # harus error, exit 1
./organize.sh exp abc         # harus error, exit 2
```

> [!NOTE]
> Struktur seperti ini akan kita gunakan kembali saat mempelajari **SLURM job array** dan **parameter sweep** di minggu-minggu berikutnya.

---

## Bonus (Opsional)

1. Jalankan `shellcheck` pada kedua script dan perbaiki seluruh warning. Lampirkan screenshot/output sebelum dan sesudah.
2. Tambahkan opsi `-h` / `--help` pada `organize.sh`.
3. Buat versi `organize.sh` yang menerima daftar temperature sebagai argument tambahan: `./organize.sh exp 3 50 150 250`.

## Rubrik Penilaian

| Komponen | Bobot |
| -------- | ----- |
| Task 1 — Redirection & pipe | 15% |
| Task 2 — Log analysis (ketepatan hasil & efisiensi pipeline) | 30% |
| Task 3 — Konfigurasi shell | 10% |
| Task 4 — `sysreport.sh` (fungsionalitas, validasi, kerapian) | 20% |
| Task 5 — `organize.sh` (fungsionalitas, validasi, kerapian) | 25% |
| Bonus | +10% |

**Kriteria script yang baik:** dapat dijalankan tanpa error, memiliki komentar singkat, variable diberi quote, pesan error jelas, dan exit code sesuai spesifikasi.
