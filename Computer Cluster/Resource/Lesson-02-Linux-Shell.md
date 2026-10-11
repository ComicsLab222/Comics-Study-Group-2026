# Lesson 02 — Linux & Shell

> 📅 **Self-study 2:** 15–21 Oktober 2026 · 💬 Dibahas pada **Meeting 1 (22 Oktober)**

## Learning Objectives

Setelah menyelesaikan materi ini, peserta mampu:

- Menggunakan **redirection** (`>`, `>>`, `<`, `2>`) dan **pipe** (`|`) untuk menggabungkan command.
- Memproses data teks menggunakan `grep`, `sort`, `uniq`, `cut`, `wc`, `tr`, dan `awk` dasar.
- Mencari file menggunakan `find` dan wildcard (globbing).
- Memahami **environment variable** (`PATH`, `HOME`) dan mengonfigurasi shell melalui `~/.bashrc`.
- Mengedit file langsung dari terminal menggunakan `nano` (dan mengenal `vim`).
- Menulis **bash script** sederhana dengan variable, argument, kondisi (`if`), loop (`for`), dan exit code.

## Prerequisites

**Materi prasyarat**

- [Lesson 01 — Linux Fundamental](Lesson-01-Linux-Fundamental.md): navigasi, path, manipulasi file, permission.

**Tools yang diperlukan**

- Environment Linux dari Lesson 01 (WSL2 / VM / native).
- Text editor terminal: `nano` (sudah terinstal di Ubuntu) dan opsional `vim`.
- Opsional: [ShellCheck](https://www.shellcheck.net/) untuk memeriksa script (`sudo apt install shellcheck`).

## Learning Materials

### 1. Standard Streams

Setiap process di Linux memiliki tiga "saluran" data:

```text
             ┌──────────────┐
 stdin (0) ─►│   command    ├─► stdout (1)   → output normal
             │              ├─► stderr (2)   → pesan error
             └──────────────┘
```

### 2. Redirection

| Operator | Fungsi | Contoh |
| -------- | ------ | ------ |
| `>` | tulis stdout ke file (**menimpa**) | `ls > files.txt` |
| `>>` | tambahkan stdout ke akhir file | `date >> log.txt` |
| `<` | gunakan file sebagai stdin | `wc -l < data.csv` |
| `2>` | tulis stderr ke file | `ls /nope 2> error.txt` |
| `&>` atau `> f 2>&1` | stdout + stderr ke file yang sama | `./run.sh > out.log 2>&1` |
| `/dev/null` | "lubang hitam" — buang output | `cmd 2> /dev/null` |

> [!NOTE]
> Pola `> output.log 2>&1` akan sangat sering Anda temui pada SLURM job script nanti, karena job berjalan tanpa terminal dan seluruh output harus disimpan ke file.

### 3. Pipe

Pipe `|` mengalirkan **stdout** satu command menjadi **stdin** command berikutnya. Ini adalah filosofi Unix: *small tools that do one thing well, combined together*.

```bash
cat access.log | grep "ERROR" | wc -l
#   └ baca file ─┘ └ filter ──┘ └ hitung ┘
```

### 4. Text Processing Toolkit

| Command | Fungsi | Contoh |
| ------- | ------ | ------ |
| `grep` | cari baris yang cocok dengan pola | `grep -i "error" app.log`, `grep -c`, `grep -v`, `grep -r` |
| `sort` | urutkan baris | `sort -n` (numerik), `sort -r` (terbalik), `sort -t, -k2` (kolom ke-2, delimiter koma) |
| `uniq` | hapus duplikat **berurutan** (biasanya setelah `sort`) | `sort names.txt \| uniq -c` |
| `cut` | ambil kolom | `cut -d',' -f1,3 data.csv` |
| `wc` | hitung baris/kata/karakter | `wc -l`, `wc -w` |
| `tr` | translate/hapus karakter | `tr 'a-z' 'A-Z'`, `tr -d '\r'` |
| `head`/`tail` | ambil awal/akhir | `tail -n +2 data.csv` (lewati header) |
| `awk` | bahasa mini untuk data berkolom | `awk -F',' '{sum+=$3} END {print sum}' data.csv` |

Contoh pipeline lengkap — 5 IP address paling sering muncul di log:

```bash
cut -d' ' -f1 access.log | sort | uniq -c | sort -rn | head -n 5
```

### 5. Wildcard (Globbing) & `find`

| Pola | Arti | Contoh |
| ---- | ---- | ------ |
| `*` | nol atau lebih karakter apa pun | `ls *.csv` |
| `?` | tepat satu karakter | `ls run_?.log` |
| `[abc]` | satu karakter dari himpunan | `ls data_[123].txt` |
| `{a,b}` | brace expansion (bukan glob, tapi sering dipakai) | `cp file.{txt,bak}` |

`find` mencari file secara rekursif berdasarkan kriteria:

```bash
find ~/project -name "*.csv"                 # berdasarkan nama
find . -type d -name "results*"              # hanya direktori
find /var/log -size +1M 2>/dev/null          # ukuran > 1 MB
find . -name "*.tmp" -mtime +7 -delete       # hapus .tmp yang lebih tua dari 7 hari
```

### 6. Variable & Environment

```bash
NAME="Budi"            # TIDAK boleh ada spasi di sekitar '='
echo "Halo, $NAME"     # gunakan double quote agar variable ter-expand
echo 'Halo, $NAME'     # single quote → literal, tidak di-expand

TODAY=$(date +%F)      # command substitution: simpan output command
echo "Hari ini: $TODAY"

export PROJECT_DIR=~/cluster-project   # export → diwariskan ke child process
env | grep PROJECT
```

**`PATH`** adalah daftar direktori (dipisah `:`) tempat shell mencari program:

```bash
echo $PATH
# /usr/local/bin:/usr/bin:/bin:...
```

Jika Anda membuat folder `~/bin` berisi script sendiri, tambahkan ke `PATH` agar bisa dipanggil dari mana saja.

### 7. Konfigurasi Shell: `~/.bashrc`

File `~/.bashrc` dijalankan setiap kali Anda membuka shell interaktif. Tempat yang tepat untuk alias, variable, dan modifikasi `PATH`:

```bash
# ~/.bashrc
alias ll='ls -lah'
alias ..='cd ..'
export PATH="$HOME/bin:$PATH"
```

Terapkan perubahan tanpa membuka terminal baru: `source ~/.bashrc`.

> [!NOTE]
> Di cluster, `~/.bashrc` sering digunakan untuk me-load software via `module load`. Kesalahan di file ini bisa membuat login Anda bermasalah — selalu backup sebelum mengedit: `cp ~/.bashrc ~/.bashrc.bak`.

### 8. Text Editor di Terminal

**nano** (direkomendasikan untuk pemula):

| Shortcut | Fungsi |
| -------- | ------ |
| `Ctrl+O` lalu `Enter` | simpan |
| `Ctrl+X` | keluar |
| `Ctrl+W` | cari |
| `Ctrl+K` / `Ctrl+U` | cut / paste baris |

**vim** (opsional, sangat umum di server): `i` masuk mode insert, `Esc` kembali ke normal mode, `:wq` simpan & keluar, `:q!` keluar tanpa menyimpan. Jalankan `vimtutor` untuk tutorial 30 menit.

### 9. Bash Scripting

Bash script adalah file teks berisi rangkaian command yang dijalankan berurutan. Inilah fondasi dari **SLURM job script** yang akan Anda tulis nanti.

```bash
#!/bin/bash
# hello.sh — contoh script dengan argument, if, dan for

set -euo pipefail          # berhenti jika ada error / variable tidak terdefinisi

NAME=${1:-"World"}         # argument pertama, default "World"
echo "Hello, $NAME!"
echo "Script: $0 | Jumlah argument: $#"

# Kondisi
if [[ -d "data" ]]; then
    echo "Direktori data/ ditemukan"
else
    echo "Membuat direktori data/"
    mkdir data
fi

# Loop
for i in {1..3}; do
    echo "Run ke-$i" > "data/run_$i.txt"
done

# Loop atas file
for f in data/*.txt; do
    echo "$f berisi: $(cat "$f")"
done

exit 0
```

**Elemen penting:**

| Elemen | Arti |
| ------ | ---- |
| `#!/bin/bash` | **shebang** — menentukan interpreter yang menjalankan script |
| `$1, $2, ...` | argument posisi |
| `$0` | nama script |
| `$#` | jumlah argument |
| `$@` | seluruh argument |
| `$?` | exit code command terakhir (`0` = sukses, selain itu = gagal) |
| `[[ -f file ]]` | true jika file ada · `-d` direktori · `-z "$s"` string kosong |
| `[[ $a -gt $b ]]` | perbandingan angka: `-eq -ne -lt -le -gt -ge` |
| `&&` / `\|\|` | jalankan berikutnya jika sukses / jika gagal |

**Menjalankan script:**

```bash
chmod +x hello.sh
./hello.sh Budi
echo $?        # cek exit code
```

> [!TIP]
> Selalu beri **double quote** pada variable (`"$file"`) untuk menghindari bug ketika nama file mengandung spasi. Jalankan `shellcheck script.sh` untuk menemukan kesalahan umum.

## Guided Practice

**Step 1 — Siapkan data latihan**

```bash
mkdir -p ~/comics-sg/week02 && cd ~/comics-sg/week02

cat > students.csv << 'EOF'
name,track,score
Andi,cluster,85
Budi,quantum,72
Citra,webdev,90
Dewi,cluster,78
Eka,quantum,95
Fajar,webdev,66
Gita,cluster,88
EOF
```

> `<< 'EOF'` disebut **here-document** — cara menulis teks multi-baris ke stdin.

**Step 2 — Redirection**

```bash
ls -l > listing.txt
date >> listing.txt
cat listing.txt
ls /folder-tidak-ada 2> error.txt
cat error.txt
```

**Step 3 — Pipe & text processing**

```bash
tail -n +2 students.csv | wc -l                                  # jumlah peserta
grep "cluster" students.csv                                      # peserta track cluster
tail -n +2 students.csv | cut -d',' -f2 | sort | uniq -c         # jumlah per track
tail -n +2 students.csv | sort -t',' -k3 -rn | head -n 3         # top 3 skor
awk -F',' 'NR>1 {sum+=$3; n++} END {print "Rata-rata:", sum/n}' students.csv
```

**Step 4 — Variable & alias**

```bash
cp ~/.bashrc ~/.bashrc.bak
echo "alias ll='ls -lah'" >> ~/.bashrc
source ~/.bashrc
ll
```

**Step 5 — Script pertama**

```bash
nano track_report.sh
```

Tulis isi berikut, simpan (`Ctrl+O`), keluar (`Ctrl+X`):

```bash
#!/bin/bash
set -euo pipefail

FILE=${1:?"Usage: $0 <csv_file>"}

if [[ ! -f "$FILE" ]]; then
    echo "Error: file '$FILE' tidak ditemukan" >&2
    exit 1
fi

for track in cluster quantum webdev; do
    count=$(grep -c ",$track," "$FILE" || true)
    echo "$track: $count peserta"
done
```

```bash
chmod +x track_report.sh
./track_report.sh students.csv
./track_report.sh nofile.csv; echo "Exit code: $?"
```

## Assignment (Referencing ke /Assignment)

Kerjakan **[Assignment 02 — Linux & Shell](../Assignment/Assignment-02-Linux-Shell.md)**. Deadline: **21 Oktober 2026, 23:59 WIB**.

- [ ] Task 1 — Redirection & pipe drill
- [ ] Task 2 — Log analysis pipeline
- [ ] Task 3 — Konfigurasi shell (`.bashrc`, alias, `PATH`)
- [ ] Task 4 — Bash script: `sysreport.sh`
- [ ] Task 5 — Bash script: `organize.sh` (simulasi parameter sweep)

## Self-Reflection

1. Apa konsep utama yang dipelajari?
2. Apa kesulitan yang ditemukan?
3. Bagaimana pipe mengubah cara Anda berpikir dalam menyelesaikan masalah pemrosesan data?
4. Bagian mana dari bash scripting yang menurut Anda paling berguna untuk menjalankan eksperimen komputasi berulang?
5. Apa yang ingin Anda tanyakan atau diskusikan pada Meeting 1 (22 Oktober)?

## Further Reading

- [The Missing Semester of Your CS Education (MIT) — Shell Tools and Scripting](https://missing.csail.mit.edu/2020/shell-tools/)
- [The Missing Semester — Data Wrangling](https://missing.csail.mit.edu/2020/data-wrangling/)
- [GNU Bash Reference Manual](https://www.gnu.org/software/bash/manual/)
- [The Linux Command Line (William Shotts) — free book](https://linuxcommand.org/tlcl.php) — Bab 6, 11, 19–20, 24–29.
- [ShellCheck — online script analyzer](https://www.shellcheck.net/)
- [OverTheWire: Bandit](https://overthewire.org/wargames/bandit/) — level 6–12 melatih `find`, `grep`, `sort`, `uniq`.
- [explainshell.com](https://explainshell.com/)
