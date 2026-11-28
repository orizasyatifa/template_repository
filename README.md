# Quarto Template

Repositori sumber terbuka untuk pengembangan buku **Quarto Template** menggunakan **Quarto Book** dan R.

README ini menjelaskan struktur proyek, cara menjalankan buku secara lokal, serta langkah publikasi melalui GitHub Pages dari branch `main` folder `/docs`.

## 1. Struktur folder

```text
ebook-template-quarto/
├── assets/
│   ├── style.css
│   └── preamble.tex
├── chapters/
│   ├── bab-1.qmd
│   ├── bab-2.qmd
│   └── bab-3.qmd
├── references/
│   ├── book.bib
│   ├── packages.bib
│   └── referensi.qmd
├── images/
│   ├── Cover_Matematika_Tambang.png
│   ├── Logo_Dsciencelabs_v1.png
│   ├── author/
│   └── chapters/
├── data/
├── R/
├── index.qmd
├── _quarto.yml
├── .nojekyll
├── docs/                 # Hasil render HTML; unggah ke GitHub
├── README.md
├── LICENSE
└── .gitignore
```

### Fungsi folder dan file

| Folder/File | Fungsi |
|---|---|
| `index.qmd` | Halaman awal buku, termasuk informasi dan pengantar penulis |
| `chapters/` | Menyimpan setiap bab buku dalam format `.qmd` |
| `references/` | Menyimpan daftar pustaka BibTeX dan halaman referensi |
| `images/` | Menyimpan sampul, logo, foto penulis, dan gambar pendukung bab |
| `assets/` | Menyimpan CSS dan konfigurasi LaTeX |
| `data/` | Menyimpan dataset pendukung buku |
| `R/` | Menyimpan skrip R pendukung |
| `docs/` | Hasil render HTML yang diterbitkan GitHub Pages dari branch `main` |
| `.nojekyll` | Memastikan GitHub Pages menyajikan berkas hasil Quarto tanpa pemrosesan Jekyll |
| `_quarto.yml` | Konfigurasi utama Quarto Book, urutan bab, format keluaran, dan folder hasil render |
| `.gitignore` | Menentukan file lokal/hasil render yang tidak perlu diunggah ke Git |

## 2. Persiapan perangkat lunak

Pastikan perangkat berikut sudah tersedia:

1. **Quarto**: https://quarto.org/docs/get-started/
2. **R**: https://cran.r-project.org/
3. **Git** (opsional, jika mengunggah melalui Terminal): https://git-scm.com/
4. **LaTeX** untuk menghasilkan PDF, misalnya TinyTeX.

Pasang paket R yang diperlukan:

```r
install.packages(c("knitr", "rmarkdown"))
```

## 3. Menjalankan buku secara lokal

Buka Terminal pada direktori utama proyek, yaitu folder yang berisi `_quarto.yml`.

Render situs HTML untuk GitHub Pages:

```bash
quarto render --to html
```

Hasil render HTML disimpan di folder:

```text
docs/
```

Folder `docs/` berisi keluaran yang akan diterbitkan. Folder ini harus ikut diunggah ke GitHub. Untuk menghasilkan PDF atau EPUB secara terpisah, jalankan:

```bash
quarto render --to pdf --no-clean
quarto render --to epub --no-clean
```

Bagian `sidebar.tools` pada `_quarto.yml` menambahkan tombol **Pratinjau PDF** dan **Pratinjau EPUB** secara terpisah di sidebar. Tombol EPUB membuka pembaca online dengan tampilan lembar buku, animasi membalik halaman, dan mode satu halaman untuk ponsel; file EPUB juga dapat diunduh dari halaman pembaca. Agar tombol berfungsi di GitHub Pages, sertakan `docs/Quarto-Template.pdf`, `docs/Quarto-Template.epub`, dan `docs/epub-reader.html` saat mengunggah hasil render.

Pada situs HTML, arahkan kursor ke tautan web untuk melihat alamatnya. Tautan silang Quarto untuk gambar, tabel, dan rumus menampilkan pratinjau target; gunakan caption dan label seperti `fig-...`, `tbl-...`, atau `eq-...`, lalu rujuk dengan `@fig-...`, `@tbl-...`, atau `@eq-...`. Klik tautan silang untuk menuju target.

Cover PDF diatur melalui `assets/preamble.tex` dan memakai `images/cover.png`; sesuaikan path tersebut jika mengganti gambar cover. Foto penulis menggunakan gambar Quarto agar tampil di HTML dan PDF.

Tanggal di halaman depan diambil dari `date: today` pada `_quarto.yml`, sehingga diperbarui setiap kali situs dirender.

Untuk menghasilkan PDF, instal TinyTeX melalui R jika LaTeX belum tersedia:

```r
install.packages("tinytex")
tinytex::install_tinytex()
```

Setelah instalasi selesai, jalankan kembali:

```bash
quarto render --to pdf
```

## 4. Mengatur identitas repositori

Sebelum publikasi, buka file `_quarto.yml` dan ganti alamat berikut:

```yaml
repo-url: https://github.com/orizasyatifa?tab=repositories
```

Contoh:

```yaml
repo-url: https://github.com/orizasyatifa/template_repository.git
```

Ganti `USERNAME` dengan nama akun GitHub dan `REPOSITORY` dengan nama repositori yang digunakan.

## 5. Membuat GitHub Public Repository

1. Masuk ke https://github.com/.
2. Klik **New repository**.
3. Isi nama repositori, misalnya `matematika-teknik-pertambangan`.
4. Pada bagian **Visibility**, pilih **Public**.
5. Klik **Create repository**.
6. Ekstrak ZIP proyek Quarto.
7. Unggah seluruh isi folder proyek ke repositori pada branch `main`.

**Penting:** Unggah isi folder proyek, termasuk file tersembunyi `.github`, bukan file ZIP sebagai satu berkas. Pastikan `_quarto.yml` berada di direktori utama repositori.

### Alternatif mengunggah melalui Terminal

Jalankan perintah berikut dari direktori proyek setelah membuat repository kosong di GitHub:

```bash
git init
git add .
git commit -m "Initial Quarto book project"
git branch -M main
git remote add origin https://github.com/orizasyatifa/template_repository.git
git push -u origin main
```

Ganti alamat remote dengan URL repositori Anda.

## 6. Mengaktifkan GitHub Pages dari branch

Render situs HTML terlebih dahulu:

```bash
quarto render --to html
```

Pastikan folder `docs/` sudah terbentuk, lalu unggah folder tersebut beserta sumber proyek ke branch `main`. Setelah itu:

1. Buka repositori GitHub.
2. Pilih **Settings**.
3. Pilih **Pages** pada menu samping.
4. Pada bagian **Build and deployment**, pilih **Deploy from a branch** sebagai source.
5. Pilih branch **main** dan folder **/docs**, lalu klik **Save**.

Jika publikasi berhasil, alamat buku biasanya berbentuk:

```text
https://github.com/orizasyatifa/template_repository.git
```

Alamat final dapat dilihat pada **Settings → Pages**.

## 7. Menambah atau mengubah bab

Untuk menambahkan bab baru:

1. Buat file Quarto baru di folder `chapters/`, misalnya `bab-4.qmd`.
2. Tulis isi bab menggunakan Markdown dan code chunk Quarto.
3. Buka `_quarto.yml`.
4. Tambahkan file tersebut pada daftar `book.chapters`.

Contoh:

```yaml
book:
  chapters:
    - index.qmd
    - chapters/bab-1.qmd
    - chapters/bab-2.qmd
    - chapters/bab-3.qmd
    - chapters/bab-4.qmd
    - references/referensi.qmd
```

Urutan file dalam daftar tersebut menentukan urutan bab pada buku.

## 8. Menambahkan gambar dan sitasi

### Gambar

Simpan gambar di folder `images/` atau subfolder yang sesuai. Gunakan path relatif dari direktori utama proyek.

Contoh:

```markdown
![Contoh ilustrasi](images/chapters/bab-1/ilustrasi.png)
```

### Sitasi

Simpan entri bibliografi dalam file BibTeX di folder `references/`, misalnya `book.bib`.

Contoh sitasi di dalam naskah:

```markdown
Menurut penelitian sebelumnya [@nama-kunci], ...
```

Pastikan kunci sitasi `nama-kunci` tersedia di salah satu file `.bib` yang didaftarkan pada `_quarto.yml`.

Gaya IEEE diatur melalui `references/ieee.csl`; sitasi tampil sebagai nomor dan dapat diklik menuju entri pada halaman Referensi.

## 9. Memperbarui buku di GitHub

Setelah mengedit naskah, gambar, atau kode, render ulang situs agar isi `docs/` ikut diperbarui:

Jika menggunakan Git:

```bash
quarto render --to pdf --no-clean
quarto render --to epub --no-clean
quarto render --to html
git add .
git commit -m "Update book content"
git push origin main
```

GitHub Pages akan menerbitkan ulang situs dari folder `docs/` pada branch `main`.

## 10. Catatan sebelum repositori dibuat publik

- Periksa kembali isi bab, persamaan, gambar, tautan, dan sitasi.
- Pastikan semua gambar, teks, dataset, dan materi pihak ketiga boleh dipublikasikan.
- Jangan mengunggah kata sandi, token akses, API key, kredensial, atau data pribadi.
- Periksa lisensi pada file `LICENSE` dan pastikan lisensi tersebut sesuai dengan hak atas seluruh materi buku.
- Uji hasil `quarto render` secara lokal sebelum publikasi.
- Konversi dari R Markdown/Bookdown ke Quarto perlu diperiksa kembali karena beberapa sintaks atau fitur khusus Bookdown mungkin memerlukan penyesuaian.

## 11. Referensi dokumentasi

- Quarto Books: https://quarto.org/docs/books/
- Quarto Publishing: https://quarto.org/docs/publishing/
- GitHub Pages: https://docs.github.com/pages
- GitHub Actions: https://docs.github.com/actions

---

**Catatan proyek:** File bab dan materi yang disertakan merupakan isi yang dipertahankan dari template sumber. README ini menjelaskan penggunaan dan publikasinya; pemeriksaan akhir terhadap seluruh isi dan keberhasilan render tetap perlu dilakukan sebelum buku diumumkan sebagai publikasi final.
