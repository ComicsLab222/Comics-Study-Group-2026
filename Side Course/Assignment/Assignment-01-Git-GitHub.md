# Assignment 01 — Git & GitHub

> 📚 **Materi terkait:** [Lesson 01 — Git & GitHub](../Resource/Lesson-01-Git-GitHub.md)

## Tujuan
Assignment ini memastikan Anda telah memiliki environment Git yang terkonfigurasi dengan benar di komputer lokal, akun GitHub aktif dengan autentikasi aman (SSH/PAT), serta menguasai siklus kerja dasar Git mulai dari inisialisasi repositori, commit, push, hingga alur Pull Request (PR).

## Deliverables

Kumpulkan file laporan Markdown `answers.md` yang berisi jawaban pertanyaan, tangkapan layar (screenshot), dan link repositori GitHub publik yang telah Anda buat.

```text
assignment-01/
├── answers.md          ← laporan tugas, penjelasan langkah, dan link repo
└── screenshots/        ← folder screenshot bukti pengerjaan
    ├── task1-ssh.png
    ├── task2-repo.png
    ├── task3-pr.png
    └── task4-gitignore.png
```

---

## Task 1 — Akun GitHub & SSH Authentication Setup

1. Siapkan akun GitHub Anda (jika belum punya, buat di [github.com](https://github.com)).
2. Konfigurasikan `user.name` dan `user.email` di terminal lokal Anda.
3. Buat pasangan kunci SSH (`ssh-keygen -t ed25519`) dan daftarkan public key tersebut ke akun GitHub Anda.
4. Jalankan perintah verifikasi koneksi berikut di terminal:
   ```bash
   ssh -T git@github.com
   ```
5. **Bukti yang dikumpulkan:**
   - Screenshot terminal yang memperlihatkan output `git config user.name`, `git config user.email`, dan pesan sukses dari `ssh -T git@github.com` (simpan di `screenshots/task1-ssh.png`).
   - Tuliskan username GitHub dan link profil Anda di `answers.md`.

---

## Task 2 — First Public Repository & Push

1. Buat repositori baru di GitHub dengan nama: `comics-sidecourse-practice` dengan visibilitas **Public** (jangan buat file README dari web).
2. Di komputer lokal, buat folder dengan nama yang sama, lakukan `git init`.
3. Buat file `README.md` yang memuat:
   - Judul repositori
   - Nama lengkap dan username GitHub
   - Track utama yang Anda ikuti di COMICS Study Group 2026 (Quantum Physics / Computer Cluster / Web Dev)
   - Motivasi mengikuti study group
4. Lakukan staging (`git add`) dan commit (`git commit -m "..."`).
5. Hubungkan remote repository dengan SSH (`git remote add origin ...`) dan lakukan `git push -u origin main`.
6. **Bukti yang dikumpulkan:**
   - Masukkan link URL repositori publik GitHub Anda ke dalam `answers.md`.
   - Screenshot halaman repositori GitHub Anda yang sudah berisi file `README.md` (`screenshots/task2-repo.png`).

---

## Task 3 — Feature Branch, Pull Request, & Merge Workflow

Terapkan alur kerja kolaboratif menggunakan branch dan Pull Request pada repositori `comics-sidecourse-practice`:

1. Buat branch baru bernama `add-profile`:
   ```bash
   git checkout -b add-profile
   ```
2. Buat file baru bernama `PROFILE.md` berisi biodata singkat, hobi, dan tools/software yang sering Anda gunakan.
3. Lakukan commit pada branch `add-profile`:
   ```bash
   git add PROFILE.md
   git commit -m "feat: tambahkan halaman profil peserta"
   ```
4. Push branch tersebut ke GitHub:
   ```bash
   git push -u origin add-profile
   ```
5. Buka repositori Anda di browser GitHub, buat **Pull Request (PR)** dari branch `add-profile` ke `main`.
6. Beri judul PR yang informatif dan deskripsi ringkas tentang perubahan yang dibuat.
7. Lakukan **Merge Pull Request** di GitHub.
8. Kembali ke terminal lokal, pindah ke branch `main`, dan tarik perubahan terbaru dengan `git pull origin main`.
9. **Bukti yang dikumpulkan:**
   - Link URL halaman Pull Request yang berstatus **Merged**.
   - Screenshot halaman PR di GitHub dengan label ungu **Merged** (`screenshots/task3-pr.png`).
   - Tampilkan output terminal `git log --oneline -n 5` di `answers.md`.

---

## Task 4 — Implementasi `.gitignore`

1. Buat file bernama `.env` di folder repositori lokal Anda, isi dengan:
   ```text
   SECRET_TOKEN=ini_kunci_rahasia_tidak_boleh_diupload
   ```
2. Buat file `.gitignore`, lalu tambahkan baris berikut di dalamnya:
   ```gitignore
   .env
   *.log
   ```
3. Buat file dummy `error.log`.
4. Jalankan `git status`. Pastikan `.env` dan `error.log` **tidak terdeteksi** oleh Git!
5. Lakukan commit pada file `.gitignore` saja:
   ```bash
   git add .gitignore
   git commit -m "chore: konfigurasi gitignore untuk abaikan file sensitif dan log"
   git push
   ```
6. **Bukti yang dikumpulkan:**
   - Output dari perintah `git status` yang membuktikan `.env` dan `error.log` diabaikan oleh Git.
   - Screenshot isi repositori di GitHub yang membuktikan file `.env` tidak pernah terunggah (`screenshots/task4-gitignore.png`).

---

## Task 5 — Refleksi Pembelajaran

Jawab 4 pertanyaan refleksi dari [Lesson 01](../Resource/Lesson-01-Git-GitHub.md#self-reflection) pada file `answers.md` Anda secara terstruktur dan jujur.

---

## Bonus (Opsional)

1. **GitHub Profile README**: Buat repositori khusus dengan nama yang sama persis dengan username GitHub Anda (misal: `github.com/<username>/<username>`). Isi file `README.md` repositori tersebut untuk menampilkan profil GitHub yang menarik (bio, skills badge, GitHub stats card).
2. Tambahkan personalisasi pesan commit menggunakan konvensi [Conventional Commits](https://www.conventionalcommits.org/) (seperti `feat:`, `fix:`, `docs:`, `chore:`).

---

## Rubrik Penilaian

| Komponen | Bobot |
| -------- | ----- |
| Task 1 — Akun & SSH Authentication | 20% |
| Task 2 — First Public Repo & Initial Push | 25% |
| Task 3 — Branching, Pull Request, & Merge Flow | 25% |
| Task 4 — Implementasi `.gitignore` | 15% |
| Task 5 — Refleksi Pembelajaran | 15% |
| Bonus | +10% |
