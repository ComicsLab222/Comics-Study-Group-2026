# Lesson 01 — Git & GitHub

## Learning Objectives
Setelah menyelesaikan materi ini, peserta mampu:
- Menjelaskan perbedaan fundamental antara **Git** (Version Control System lokal) dan **GitHub** (remote hosting & platform kolaborasi).
- Membuat dan mengonfigurasi akun GitHub dengan aman (profil, autentikasi 2FA, dan token/SSH key).
- Melakukan instalasi dan setup awal Git pada local machine (konfigurasi nama, email, default branch, dan credentials).
- Menghubungkan local repository ke remote GitHub menggunakan protokol SSH atau Personal Access Token (PAT).
- Menjalankan siklus kerja dasar Git: `git init`, `git status`, `git add`, `git commit`, `git log`, dan `git push`.
- Memahami dan membuat file `.gitignore` untuk mencegah file sensitif atau temporary terunggah.
- Memahami konsep kolaborasi: **branching**, **forking**, dan membuat **Pull Request (PR)** untuk peer review.

## Prerequisites
- Materi prasyarat:
  - Kemampuan dasar navigasi command line/terminal (relevan dengan materi [Computer Cluster Lesson 01](../../Computer%20Cluster/Resource/Lesson-01-Linux-Fundamental.md)).
- Tools yang diperlukan:
  - Web browser & koneksi internet (untuk akses [GitHub.com](https://github.com)).
  - Aplikasi terminal: Git Bash (Windows), Terminal (macOS/Linux), atau PowerShell.
  - Text editor: [Visual Studio Code](https://code.visualstudio.com/).

## Learning Materials

### 1. Apa itu Git & Mengapa Kita Butuh GitHub?
Pernahkah Anda menyimpan tugas dengan nama seperti ini?
- `tugas_akhir.docx`
- `tugas_akhir_revisi.docx`
- `tugas_akhir_revisi_FIX.docx`
- `tugas_akhir_revisi_FIX_beneran.docx`

**Git** menyelesaikan masalah ini dengan menjadi sistem pelacak riwayat file (**Version Control System / VCS**). Setiap perubahan dicatat sebagai checkpoint (**commit**) yang memiliki ID unik, tanggal, pembuat, dan pesan penjelasan.

```text
┌─────────────────────────────────┐           ┌─────────────────────────────────┐
│          Local Machine          │           │          Remote Server          │
│                                 │           │                                 │
│  📁 Working Directory           │           │             GitHub              │
│         │ (git add)             │           │  (Cloud Hosting, Issue Tracker, │
│         ▼                       │ git push  │   Pull Request, Collaboration)  │
│  📦 Staging Area                │──────────►│                                 │
│         │ (git commit)          │           │                                 │
│         ▼                       │ git pull  │                                 │
│  🏛️ Local Repository (.git)     │◄──────────│                                 │
└─────────────────────────────────┘           └─────────────────────────────────┘
```

- **Git**: Tools berbasis CLI yang berjalan di komputer lokal Anda tanpa butuh internet.
- **GitHub**: Layanan cloud berbasis web untuk menyimpan repositori Git, memudahkan backup, kolaborasi tim, dan review kode.

---

### 2. Membuat Akun GitHub & Konfigurasi Profil
1. Buka [https://github.com](https://github.com) lalu klik tombol **Sign up**.
2. Masukkan alamat email aktif (gunakan email yang sama untuk konfigurasi Git lokal nanti).
3. Buat password yang kuat dan pilih username profesional (misal: `namalengkap` atau `inisial-nama`).
4. Selesaikan verifikasi captcha dan konfirmasi kode yang dikirim ke email Anda.
5. *(Sangat disarankan)* Aktifkan **Two-Factor Authentication (2FA)** di menu **Settings → Password and authentication → Two-factor authentication**.

---

### 3. Setup Git di Local Machine

#### A. Instalasi
- **Windows**: Download installer [Git for Windows](https://git-scm.com/download/win). Saat instalasi, centang opsi *Git Bash* dan pilih default editor (misal VS Code).
- **macOS**: Buka Terminal dan ketik `git --version`. Jika belum terpasang, macOS akan otomatis menawarkan instalasi Xcode Command Line Tools. Atau via Homebrew: `brew install git`.
- **Linux (Ubuntu/Debian)**:
  ```bash
  sudo apt update && sudo apt install git -y
  ```

Verifikasi instalasi dengan menjalankan:
```bash
git --version
```

#### B. Konfigurasi Identitas (Wajib)
Jalankan command berikut di terminal:
```bash
git config --global user.name "Nama Lengkap Anda"
git config --global user.email "email-anda@example.com"
git config --global init.defaultBranch main
```
> [!IMPORTANT]
> Pastikan email yang Anda masukkan persis sama dengan email yang terdaftar di akun GitHub Anda agar commit terhitung di profil GitHub Anda.

Cek konfigurasi yang tersimpan:
```bash
git config --list
```

#### C. Setup Credentials (Autentikasi Aman)
Sejak Agustus 2021, GitHub tidak lagi menerima password akun untuk `git push` via terminal. Anda harus menggunakan **SSH Key** (direkomendasikan) atau **Personal Access Token (PAT)**.

**Metode Rekomendasi: SSH Key**
1. Buat pasangan kunci SSH di terminal:
   ```bash
   ssh-keygen -t ed25519 -C "email-anda@example.com"
   ```
   *(Tekan `Enter` tiga kali untuk menerima lokasi default dan tanpa passphrase).*
2. Ambil public key yang sudah dibuat:
   - Windows (Git Bash): `cat ~/.ssh/id_ed25519.pub | clip`
   - macOS: `pbcopy < ~/.ssh/id_ed25519.pub`
   - Linux: `cat ~/.ssh/id_ed25519.pub` (lalu copy teksnya)
3. Buka GitHub → **Settings** → **SSH and GPG keys** → klik **New SSH key**.
4. Beri judul (misal: `Laptop-Pribadi`) dan paste key ke kotak yang tersedia, lalu klik **Add SSH key**.
5. Uji koneksi dari terminal:
   ```bash
   ssh -T git@github.com
   ```
   Jika muncul pesan *"Hi username! You've successfully authenticated..."*, berarti setup berhasil!

---

### 4. Siklus Kerja Git: Dari Local ke GitHub

```text
1. Modifikasi File ──► 2. git add (Stage) ──► 3. git commit (Save) ──► 4. git push (Upload)
```

#### Langkah-langkah Lengkap:
1. **Inisialisasi Repositori Lokal:**
   ```bash
   mkdir my-first-repo
   cd my-first-repo
   git init
   ```
2. **Cek Status:**
   ```bash
   git status
   ```
3. **Membuat File & Menambah ke Staging Area:**
   ```bash
   echo "# Proyek Pertamaku" > README.md
   git add README.md          # stage 1 file
   # atau: git add .          # stage semua perubahan
   ```
4. **Membuat Commit:**
   ```bash
   git commit -m "feat: inisialisasi project dengan README.md"
   ```
5. **Menghubungkan ke GitHub Remote:**
   Buat repositori baru kosong di GitHub (jangan centang "Add README" agar tidak konflik). Lalu salin URL SSH repositori tersebut:
   ```bash
   git remote add origin git@github.com:<username>/my-first-repo.git
   git branch -M main
   git push -u origin main
   ```
   *(Flag `-u` mengaitkan branch lokal `main` dengan remote `origin/main`, sehingga selanjutnya cukup ketik `git push` atau `git pull`).*

---

### 5. File `.gitignore`
Tidak semua file boleh diunggah ke GitHub. File seperti password/API key, folder dependensi (`node_modules/`, `venv/`), file build (`.exe`, `.o`), atau file log tidak boleh di-commit.

Buat file bernama `.gitignore` di root direktori project:
```gitignore
# Python virtual environment
venv/
__pycache__/

# Node.js
node_modules/

# OS specific files
.DS_Store
Thumbs.db

# Secrets & environment variables
.env
secret_key.pem
```

---

### 6. Konsep Kolaborasi: Branching & Pull Request (PR)

Di dunia nyata atau tim riset, kita tidak bekerja langsung di branch utama (`main`) agar tidak merusak kode yang sudah stabil.

```text
main           ●──────●──────────────●─────────● (merged PR)
                       \            /
feature-branch          ●──────────● (commit)
```

#### Alur Pull Request:
1. **Buat Branch Baru:**
   ```bash
   git checkout -b fitur-baru   # atau: git switch -c fitur-baru
   ```
2. **Lakukan perubahan & commit:**
   ```bash
   git add .
   git commit -m "docs: tambahkan penjelasan alur sistem"
   ```
3. **Push branch ke GitHub:**
   ```bash
   git push -u origin fitur-baru
   ```
4. **Buka Pull Request (PR) di GitHub:**
   - Masuk ke repositori Anda di web GitHub.
   - Klik tombol hijau **Compare & pull request**.
   - Berikan judul dan deskripsi perubahan yang jelas.
   - Klik **Create pull request**.
5. **Review & Merge:**
   - Teman/mentor dapat membaca baris kode yang diubah (diff), memberi komentar atau saran perbaikan.
   - Setelah disetujui, klik **Merge pull request** untuk menggabungkan kode ke branch `main`.
6. **Sinkronisasi Local:**
   ```bash
   git checkout main
   git pull origin main
   ```

## Guided Practice

Ikuti langkah-langkah hands-on berikut di terminal Anda:

**Step 1 — Verifikasi identitas git**
```bash
git config user.name
git config user.email
```

**Step 2 — Membuat repositori latihan**
```bash
mkdir ~/git-sandbox && cd ~/git-sandbox
git init
echo "# Latihan Git & GitHub" > README.md
echo "Dibuat oleh: $(git config user.name)" >> README.md
git status
```

**Step 3 — Membuat commit pertama**
```bash
git add README.md
git commit -m "Initial commit: buat README.md"
git log --oneline
```

**Step 4 — Simulasi penggunaan `.gitignore`**
```bash
echo "DATABASE_PASSWORD=rahasia123" > .env
echo "hasil log sementara" > debug.log
echo ".env" > .gitignore
echo "*.log" >> .gitignore

git status
# Perhatikan bahwa file .env dan debug.log tidak muncul di untracked files!
git add .gitignore
git commit -m "chore: tambahkan konfigurasi gitignore"
```

**Step 5 — Simulasi Branching**
```bash
git branch
git checkout -b update-biodata
echo "- Track Pilihan: COMICS Study Group 2026" >> README.md
git commit -am "docs: tambahkan informasi track di README"
git checkout main
cat README.md     # Perhatikan baris baru belum ada di branch main!
git merge update-biodata
cat README.md     # Sekarang baris baru sudah masuk ke branch main!
```

## Assignment (Referencing ke /Assignment)

Kerjakan **[Assignment 01 — Git & GitHub](../Assignment/Assignment-01-Git-GitHub.md)**.

- [ ] Task 1 — Akun GitHub & SSH Authentication Setup
- [ ] Task 2 — First Public Repository & Push
- [ ] Task 3 — Feature Branch, Pull Request, & Merge Workflow
- [ ] Task 4 — Implementasi `.gitignore`
- [ ] Task 5 — Refleksi Pembelajaran

## Self-Reflection
1. Apa konsep utama yang dipelajari?
2. Apa kesulitan yang ditemukan saat melakukan setup Git & autentikasi GitHub?
3. Mengapa pesan commit harus deskriptif dan tidak cukup hanya menulis "update" atau "fix"?
4. Mengapa kita perlu menggunakan branch terpisah saat mengerjakan fitur baru ketimbang langsung commit ke `main`?

## Further Reading
- [Pro Git Book (Resmi & Gratis)](https://git-scm.com/book/en/v2) — panduan definitif Git.
- [GitHub Docs — Connecting to GitHub with SSH](https://docs.github.com/en/authentication/connecting-to-github-with-ssh)
- [Learn Git Branching (Game Interaktif Visual)](https://learngitbranching.js.org/) — cara terbaik memahami alur branch dan merge.
- [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/) — standar penulisan pesan commit profesional.
