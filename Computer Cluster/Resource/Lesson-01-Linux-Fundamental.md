# Lesson 01 — Linux Fundamental

> 📅 **Self-study 1:** 8–14 Oktober 2026 · 💬 Dibahas pada **Meeting 1 (22 Oktober)**

## Learning Objectives

Setelah menyelesaikan materi ini, peserta mampu:

- Menjelaskan apa itu Linux, kernel, dan distribusi (distro), serta alasan Linux digunakan di hampir seluruh computer cluster/HPC.
- Menyiapkan environment Linux di komputer sendiri (WSL2, Virtual Machine, atau native).
- Memahami anatomi sebuah command: `command [options] [arguments]`.
- Menjelaskan struktur filesystem Linux (Filesystem Hierarchy Standard) dan perbedaan **absolute path** vs **relative path**.
- Melakukan navigasi dan manipulasi file/direktori melalui command line.
- Membaca dan mengubah **file permission** (`rwx`) menggunakan `chmod`.
- Mencari bantuan secara mandiri menggunakan `man`, `--help`, dan `type`.

## Prerequisites

**Materi prasyarat**

- Tidak ada. Lesson ini adalah titik awal track Computer Cluster.
- Familiar dengan penggunaan komputer sehari-hari (file, folder, mengetik).

**Tools yang diperlukan**

Pilih **salah satu** environment Linux berikut:

| Sistem Operasi | Opsi yang Disarankan |
| -------------- | -------------------- |
| Windows 10/11  | **WSL2 + Ubuntu** (paling mudah) — `wsl --install` di PowerShell (Run as Administrator) |
| macOS          | Terminal bawaan (berbasis Unix, mayoritas command sama) atau VM Ubuntu via UTM |
| Linux          | Terminal bawaan distro Anda |
| Alternatif     | VirtualBox + Ubuntu 24.04 LTS, atau cloud shell gratis |

> [!TIP]
> Setelah WSL terpasang, buka aplikasi **Ubuntu** dari Start Menu. Pada first launch Anda akan diminta membuat username dan password Linux (password tidak terlihat saat diketik — itu normal).

## Learning Materials

### 1. Apa itu Linux?

**Linux** sebenarnya adalah sebuah **kernel** — inti dari sistem operasi yang mengatur komunikasi antara hardware (CPU, memory, disk, network) dan software. Kernel ini kemudian dikombinasikan dengan tools (GNU utilities, shell, package manager, dsb.) menjadi sebuah **distribusi** seperti Ubuntu, Debian, Fedora, Rocky Linux, atau Arch.

```text
┌───────────────────────────────┐
│   User & Applications         │  ← Anda, Python, browser, simulasi
├───────────────────────────────┤
│   Shell (bash, zsh)           │  ← penerjemah perintah Anda
├───────────────────────────────┤
│   Kernel (Linux)              │  ← manajemen process, memory, device
├───────────────────────────────┤
│   Hardware                    │  ← CPU, RAM, disk, network card
└───────────────────────────────┘
```

**Mengapa Linux di cluster?**

- **100% superkomputer di daftar TOP500** menjalankan Linux.
- Open source, stabil, dan dapat dikustomisasi.
- Dirancang multi-user: banyak pengguna bisa login ke mesin yang sama secara bersamaan.
- Hampir semua tool HPC (SLURM, MPI, compiler scientific) dikembangkan untuk Linux.
- Akses cluster hampir selalu melalui **command line**, bukan GUI.

### 2. Terminal, Shell, dan Prompt

- **Terminal** — jendela/aplikasi tempat Anda mengetik.
- **Shell** — program yang membaca perintah Anda dan menjalankannya. Default di kebanyakan distro adalah **bash**.
- **Prompt** — teks yang menandakan shell siap menerima perintah:

```text
budi@laptop:~/projects$
 │     │      │       └─ $ = user biasa (# = root/superuser)
 │     │      └───────── current directory (~ = home directory)
 │     └──────────────── hostname (nama mesin)
 └────────────────────── username
```

### 3. Anatomi Command

```text
ls   -l -a   /etc
│    │       └─ argument  : objek yang dikenai perintah
│    └───────── options   : mengubah perilaku perintah (flag)
└────────────── command   : program yang dijalankan
```

- Option pendek bisa digabung: `ls -l -a` = `ls -la`.
- Option panjang diawali dua strip: `ls --all`.
- Linux bersifat **case-sensitive**: `File.txt` ≠ `file.txt`.

### 4. Filesystem Hierarchy

Linux tidak memiliki drive `C:` atau `D:`. Semua file berada dalam satu pohon yang berakar pada **root** `/`.

```text
/
├── bin/      → program/command esensial (ls, cp, mv)
├── etc/      → file konfigurasi sistem
├── home/     → home directory setiap user (/home/budi)
├── root/     → home directory milik superuser
├── tmp/      → file sementara (dihapus saat reboot)
├── usr/      → program & library yang diinstal user/sistem
├── var/      → data yang berubah-ubah (log, cache)
├── opt/      → software tambahan (sering dipakai di cluster)
├── proc/     → filesystem virtual berisi info process & kernel
└── dev/      → representasi device (disk, terminal)
```

**Path:**

| Simbol | Arti | Contoh |
| ------ | ---- | ------ |
| `/`    | root directory (jika di awal path) | `/etc/hostname` |
| `~`    | home directory user saat ini | `~/Documents` = `/home/budi/Documents` |
| `.`    | direktori saat ini | `./script.sh` |
| `..`   | direktori induk (parent) | `cd ..` |

- **Absolute path** — dimulai dari `/`, selalu menunjuk lokasi yang sama: `/home/budi/data/input.txt`
- **Relative path** — relatif terhadap posisi saat ini: `data/input.txt` atau `../shared/input.txt`

### 5. Command Navigasi

| Command | Fungsi | Contoh |
| ------- | ------ | ------ |
| `pwd` | print working directory | `pwd` |
| `ls` | list isi direktori | `ls -lah /var/log` |
| `cd` | change directory | `cd ~/projects`, `cd ..`, `cd -` (kembali ke dir sebelumnya) |
| `tree` | tampilkan struktur pohon (install: `sudo apt install tree`) | `tree -L 2` |

Option `ls` yang paling sering dipakai: `-l` (long format), `-a` (tampilkan hidden file yang diawali `.`), `-h` (ukuran human-readable), `-t` (urut waktu), `-R` (rekursif).

### 6. Manipulasi File & Direktori

| Command | Fungsi | Contoh |
| ------- | ------ | ------ |
| `mkdir` | buat direktori | `mkdir -p project/{data,src,results}` |
| `touch` | buat file kosong / update timestamp | `touch notes.txt` |
| `cp` | copy | `cp a.txt b.txt`, `cp -r dir1 dir2` |
| `mv` | move / rename | `mv old.txt new.txt`, `mv file.txt data/` |
| `rm` | hapus file | `rm file.txt`, `rm -r folder/` |
| `rmdir` | hapus direktori kosong | `rmdir empty_dir` |

> [!CAUTION]
> Linux **tidak memiliki Recycle Bin** di command line. `rm` menghapus permanen. Jangan pernah menjalankan `rm -rf` tanpa memeriksa path dengan teliti. Gunakan `rm -i` untuk konfirmasi saat belajar.

### 7. Melihat Isi File

| Command | Fungsi |
| ------- | ------ |
| `cat file` | tampilkan seluruh isi file |
| `less file` | baca file per halaman (`q` keluar, `/kata` cari, `space` halaman berikutnya) |
| `head -n 5 file` | 5 baris pertama |
| `tail -n 5 file` | 5 baris terakhir |
| `tail -f file` | ikuti file secara real-time (berguna untuk memantau log job di cluster) |
| `wc -l file` | hitung jumlah baris |
| `file nama` | deteksi tipe file |

### 8. User & Permission

Linux adalah sistem multi-user. Setiap file memiliki **owner**, **group**, dan **permission**.

```text
$ ls -l script.sh
-rwxr-xr--  1  budi  research  512  Oct 8 10:00  script.sh
│└┬┘└┬┘└┬┘      └┬─┘ └──┬───┘
│ │  │  │        │      └─ group
│ │  │  │        └──────── owner
│ │  │  └───────────────── others : r-- (read saja)
│ │  └──────────────────── group  : r-x (read + execute)
│ └─────────────────────── user   : rwx (read + write + execute)
└───────────────────────── tipe   : - file, d directory, l symlink
```

| Simbol | Pada File | Pada Direktori | Nilai Oktal |
| ------ | --------- | -------------- | ----------- |
| `r` | baca isi file | list isi direktori | 4 |
| `w` | ubah isi file | buat/hapus file di dalamnya | 2 |
| `x` | eksekusi sebagai program | masuk (`cd`) ke direktori | 1 |

**Mengubah permission dengan `chmod`:**

```bash
chmod u+x script.sh      # tambah execute untuk user (owner)
chmod go-w data.txt      # hapus write dari group & others
chmod 755 script.sh      # rwx r-x r-x  (7=4+2+1, 5=4+1)
chmod 600 secret.key     # rw- --- ---  (hanya owner yang bisa baca/tulis)
```

Command terkait user: `whoami`, `id`, `groups`, `sudo <command>` (menjalankan sebagai superuser — **di cluster Anda biasanya tidak memiliki akses sudo**).

### 9. Mencari Bantuan

```bash
man ls          # manual lengkap (q untuk keluar)
ls --help       # ringkasan option
type cd         # apakah builtin shell, alias, atau program?
which python3   # lokasi program di filesystem
apropos copy    # cari command berdasarkan kata kunci
```

> [!TIP]
> Kebiasaan terpenting di Linux: **baca pesan error**. Pesan seperti `No such file or directory` atau `Permission denied` hampir selalu memberi tahu persis apa yang salah.

## Guided Practice

Ikuti langkah berikut di terminal Anda. Ketik sendiri setiap command (jangan copy-paste) dan amati output-nya.

**Step 1 — Kenali environment**

```bash
whoami
hostname
pwd
uname -a                 # info kernel
cat /etc/os-release      # info distro
```

**Step 2 — Jelajahi filesystem**

```bash
cd /
ls
ls -l /etc | head -n 10
cd ~
ls -la                   # perhatikan hidden files seperti .bashrc
```

**Step 3 — Buat struktur project**

```bash
mkdir -p ~/comics-sg/week01/{data,scripts,results}
cd ~/comics-sg/week01
tree                      # atau: ls -R
```

**Step 4 — Manipulasi file**

```bash
echo "Hello Cluster" > data/hello.txt
cat data/hello.txt
cp data/hello.txt results/hello_copy.txt
mv results/hello_copy.txt results/greeting.txt
ls -l results/
```

**Step 5 — Absolute vs relative path**

```bash
cd ~/comics-sg/week01/scripts
cat ../data/hello.txt                       # relative
cat ~/comics-sg/week01/data/hello.txt       # absolute (via ~)
```

**Step 6 — Permission**

```bash
echo 'echo "Script berjalan dari $(pwd)"' > run.sh
ls -l run.sh             # perhatikan: belum ada x
./run.sh                 # → Permission denied
chmod u+x run.sh
ls -l run.sh
./run.sh                 # → berhasil
```

**Step 7 — Cari bantuan**

```bash
man mkdir                # temukan arti option -p
cp --help | head -n 20
```

**Step 8 — Bersihkan (dengan hati-hati)**

```bash
cd ~/comics-sg/week01
rm -i results/greeting.txt
```

## Assignment (Referencing ke /Assignment)

Kerjakan **[Assignment 01 — Linux Fundamental](../Assignment/Assignment-01-Linux-Fundamental.md)**. Deadline: **14 Oktober 2026, 23:59 WIB**.

- [ ] Task 1 — Environment setup & system information
- [ ] Task 2 — Filesystem exploration (FHS)
- [ ] Task 3 — Membangun struktur direktori project
- [ ] Task 4 — File permission challenge
- [ ] Task 5 — Command log & reflection

## Self-Reflection

1. Apa konsep utama yang dipelajari?
2. Apa kesulitan yang ditemukan?
3. Apa perbedaan absolute path dan relative path, dan kapan sebaiknya masing-masing digunakan dalam script?
4. Mengapa permission file penting pada sistem multi-user seperti cluster?
5. Error apa yang paling sering Anda temui minggu ini, dan bagaimana Anda menyelesaikannya?

## Further Reading

- [Linux Journey — Command Line & Filesystem](https://linuxjourney.com/) — materi interaktif, sangat cocok untuk pemula.
- [Ubuntu Tutorial — The Linux command line for beginners](https://ubuntu.com/tutorials/command-line-for-beginners)
- [The Linux Command Line (William Shotts) — free book](https://linuxcommand.org/tlcl.php) — Bab 1–9.
- [Install WSL — Microsoft Learn](https://learn.microsoft.com/en-us/windows/wsl/install)
- [Filesystem Hierarchy Standard 3.0](https://refspecs.linuxfoundation.org/FHS_3.0/fhs/index.html)
- [OverTheWire: Bandit](https://overthewire.org/wargames/bandit/) — game untuk melatih command Linux (level 0–5 relevan untuk minggu ini).
- [explainshell.com](https://explainshell.com/) — tempel sebuah command untuk melihat penjelasan tiap bagiannya.
