
# Laporan Praktikum Minggu [3]
Topik: Manajemen File dan Permission di Linux 

---

## Identitas
- **Nama**  : Keysya Ayu Anggita 
- **NIM**   : 250202944
- **Kelas** : 1IKRA

---

## Tujuan
1. Menggunakan perintah `ls`, `pwd`, `cd`, `cat` untuk navigasi file dan direktori.
2. Menggunakan `chmod` dan `chown` untuk manajemen hak akses file.
3. Menjelaskan hasil output dari perintah Linux dasar.
4. Menyusun laporan praktikum dengan struktur yang benar.
5. Mengunggah dokumentasi hasil ke Git Repository tepat waktu.

---

## Dasar Teori
Sistem operasi Linux memiliki manajemen file yang berfungsi untuk mengatur penyimpanan, pengambilan, dan pengelola data di komputer. Struktur sistem file Linux berbentuk hierarkis, yang mulai dari direktori utama yaitu **root(/)** dan bercabang ke berbagai folder lain seperti `/home`, `/bin`, dan `/etc`. Setiap file di Linux disimpan dalam bentuk **inode**, yaitu struktur data yang berisi informasi penting seperti ukuran file, lokasi penyimpanan, waktu modifikasi, serta hak atas pengguna. Sistem file yang umum digunakan seperti **ext3** dan **ext4**  mendukung fitur **journaling**, yang berguna untuk menjaga agar data tetap aman ketika terjadi gangguan seperti mati listrik atau sistem crash. Selain itu, Linux juga menggunakan proses **mounting** untuk menghubungkan perangkat penyimpanan ke sistem agar bisa diakses melalui direktori.

Dalam Linux, setiap file dan direktori memiliki **permission** (izin akses) yang berfungsi untuk melindungi file dari perubahan atau perubahan yang tidak sah. Izin akses ini dibagi menjadi tiga jenis pengguna, yaitu **owner(pemilik)**, **grup(kelompok)**, dan **others(pengguna lain)**, dengan tipe hak akses utama: *read(r)* untuk membaca, *write(w)* untuk mengubah, dan *execute(x)* unutk menjalankan file. Pengaturan izin ini dilakukan dengan perintah `chmod`, yang bisa menggunakan simbol huruf atau angka, misalnya `chmod 755 file.sh` untuk memberikan akses penuh ke pemilik dan akses baca-jalankan ke pengguna lain. Sistem izin ini membantu menjaga keamanan dan proteksi data, agar hanya pengguna yang berhak mengakses atau mengubah file tertentu.     

---

## Langkah Praktikum
1. **Setup Environment**
   - Gunakan Linux (Ubuntu/WSL).
   - Pastikan folder kerja berada di dalam direktori repositori Git praktikum:
     ```
     praktikum/week3-linux-fs-permission/
     ```

2. **Eksperimen 1 – Navigasi Sistem File**
   Jalankan perintah berikut:
   ```bash
   pwd
   ls -l
   cd /tmp
   ls -a
   ```
   - Jelaskan hasil tiap perintah.
   - Catat direktori aktif, isi folder, dan file tersembunyi (jika ada).

3. **Eksperimen 2 – Membaca File**
   Jalankan perintah:
   ```bash
   cat /etc/passwd | head -n 5
   ```
   - Jelaskan isi file dan struktur barisnya (user, UID, GID, home, shell).

4. **Eksperimen 3 – Permission & Ownership**
   Buat file baru:
   ```bash
   echo "Hello <NAME><NIM>" > percobaan.txt
   ls -l percobaan.txt
   chmod 600 percobaan.txt
   ls -l percobaan.txt
   ```
   - Analisis perbedaan sebelum dan sesudah chmod.  
   - Ubah pemilik file (jika memiliki izin sudo):
   ```bash
   sudo chown root percobaan.txt
   ls -l percobaan.txt
   ```
   - Catat hasilnya.

5. **Eksperimen 4 – Dokumentasi**
   - Ambil screenshot hasil terminal dan simpan di:
     ```
     praktikum/week3-linux-fs-permission/screenshots/
     ```
   - Tambahkan analisis hasil pada `laporan.md`.

6. **Commit & Push**
   ```bash
   git add .
   git commit -m "Minggu 3 - Linux File System & Permission"
   git push origin main
   ```


---

## Kode / Perintah
Tuliskan potongan kode atau perintah utama:
 ```bash
   pwd
   ls -l
   cd /tmp
   ls -a
   ```
 ```bash
   cd
   cat /etc/passwd | head -n 5
   ```
  ```bash
   echo "Hello Keysya Ayu Anggita - 250202944" > percobaan.txt
   ls -l percobaan.txt
   chmod 600 percobaan.txt
   ls -l percobaan.txt
   cat percobaan.txt
   ```

---

## Hasil Eksekusi

![alt text](<screenshots/linux week3.png>)

### Eksperimen 1 
| Perintah | Hasil Output | Keterangan |
| :--- | :--- | :--- |
| `pwd` | `/home/keysyagita` | Perintah `pwd` digunakan untuk menampilkan direktori aktif. Hasil tersebut menunjukkan bahwa direktori kerja yang digunakan oleh `/home/keysyagita`, yaitu direktori home milik pengguna `keysyagita`. |
| `ls -l` | `-rw------- 1 keysyagita keysyagita 33 Oct 22 23:00 percobaan.txt` | Perintah `ls -l` berfungsi menampilkan isi direktori dalam format panjang. Hasil menunjukkan file bernama `percobaan.txt` dengan izin `-rw------- `, artinya adalah pemilik file yang memiliki izin membaca(r), dan menulis(w). Grup dan pengguna lain tidak memiliki akses terhadap file tersebut. |  
| `cd /tmp` | Tidak menampilkan output | Perintah `cd` digunakan untuk berpindah ke direktori lain. Pada perintah tersebut, direktori aktif berpindah ke `/tmp`, yaitu direktori sementara yang digunakan oleh sistem untuk menyimpan file sementara. |
| `ls -a` | ` .XIM-unix`, `.font-unix`, `.ICE-unix`, `.Test-unix`, `.X11-unix`, `| Perintah `ls -l` menampilkan seluruh file dan direktori. Direktori `/tmp` berisi beberapa file sementara yang digunakan oleh sistem. Untuk melihat seluruh file termasuk file tersembunyi, digunakan perintah `ls -a`. |

---
### Eksperimen 2
| Nama Kolom | Contoh | Keterangan |
| :--- | :--- | :--- |
| username | `root`, `daemon`, `bin`, `sys`, `sync` | Nama akun pengguna sistem. |
| x | `x` | Menunjukkan bahwa password disimpan di file `/etc/shadow`. |
| UID (User ID) | `0`,`1`,`2`,`3`,`4` | Nomor identitas unik untuk setiap pengguna. `UID 0` milik pengguna root. |
| GID (Group ID) | `0`,`1`,`2`,`3`,`65534`| Nomor identitas grup yang sesuai dengan setiap pengguna. |
| comment | `root`, `daemon`, `bin`, `sys`, `sync` | Deskripsi tambahan atau nama lengkap pengguna. |
| home directory | `/root`,`/usr/sbin`,`/bin`,`/dev`| Menunjukkan direktori utama(home) pengguna saat login. |
| shell | `/bin/bash`,`/usr/sbin/nologin`,`/bin/sync`| Menunjukkan shell atau program yang dijalankan setelah login. `/bin/bash`shell interaktif, sedangkan `/usr/sbin/nologin` berarti akun tidak dapat login|

---
### Eksperimen 3
| Kondisi File | Perintah yang dijalankan | Hasil | Perbedaan |
| :--- | :--- | :--- | :--- |
| Sebelum `chmod` | ` ls -s percobaan.txt` | `-rw-r--r--` | File baru yang dibuat oleh pengguna memiliki izin read dan write untuk owner. |
| Sesudah `chmod 600 percobaan.txt` | `chmod 600 percobaan.txt`, `ls -l percobaan.txt` | `-rw-------` | Setelah dijalankan, izin file berubah menjadi hanya pemilik(owner) yang dapat membaca dan menulis file. Group dan others tidak memiliki akses sama sekali. |

| Kode izin | Owner | Group | Others | Keterangan |
|:---|:---|:---|:---|:---|
| Sebelum `rw-r--r--` | `rw-` (read,write) | `r--`(read only) | `r--`(read only) | File dapat dibaca oleh semua pengguna, tetapi hanya pemilik yang dapat mengedit.|
| Sesudah `rw-------` | `rw-`(read,write) | `---`(no access) | `---`(no access) | File hanya dapat dibaca dan ditulis oleh pemilik, pengguna lain tidak bisa membuka atau melihat isi file. |

---

## Analisis
**Eksperimen 1** Perintah `pwd`, `ls -l` dan `ls -a` digunakan untuk mengenal dasar navigasi di Linux. Perintah `pwd` menampilan direktori aktif, `ls -l` menampilkan daftar isi lengkap dengan izin file, sedangkan `cd /tmp` berpindah ke direktori sementara. Perintah `ls -a` menampilkan seluruh isi folder termasuk file tersembunyi. Dari percobaan tersebut dapat dipahami bahwa Linux memiliki struktur direktori yang teratur dan mendukung pengelolaan file secara detail.

**Eksperimen 2** Perintah cat/etc/passwd | head -n 5 digunakan untuk menampilkan 5 barisan pertama dari file `/etc/passwd`. File ini menyimpan informasi akun pengguna seperti nama user, UID, GID, direktori home dan shell. Izin file `/etc/passwd` adalah `-rw-r--r--`, artinya adalah root yang dapat menulis , sementara pengguna lain hanya bisa membaca. Hal ini menunjukkan bahwa sistem Linux memiliki pengaturan izin file yang ketat untuk menjaga keamanan data pengguna.

**Eksperimen 3** Dilakukan pembuatan dan pengaturan izin file menggunakan perintah `chmod`. Perintah `echo "Hello Keysya Ayu Anggita - 250202944" > percobaan.txt` digunakan untuk membuat file baru bernama `percobaan.txt` dan menuliskan teks di dalamnya. Setelah itu, perintah `chmod 600 percobaan.txt` dijalankan untuk mengubah izin file menjadi `-rw-------`, yang berarti hanya pemilik file yang dapat membaca dan menulis, sedangkan pengguna lain tidak memiliki akses sama sekali. Hasilnya diperiksa menggunakan `ls -l`, dan isi file ditampilkan kembali dengan `cat percobaan.txt` untuk memastikan file masih dapat diakses oleh pemilik. Percobaan ini membuktikan bahwa perintah `chmod` berfungsi penting dalam menjaga keamanan file agar tidak dapat diakses oleh pengguna lain.

---

## Kesimpulan
Berdasarkan hasil percobaan tersebut, maka dapat disimpulkan hal-hal berikut: 
- Sistem operasi Linux memiliki struktur direktori yang teratur dan mudah dipahami melalui pemerintahan dasar seperti `pwd`, `ls` dan `cd`.
- Perintah `pwd` digunakan untuk melihat direktori aktif, sedangkan `ls -l` dan `ls -a` membantu menampilkan isi folder secara lengkap termasuk file tersembunyi.
- File `/etc/passwd` menyimpan informasi semua akun pengguna seperti username, UID, GID, home directory dan shell yang digunakan.
- Secara keseluruhan, ketiga eksperimen menunjukkan bahwa Linux memberikan kontrol penuh kepada pengguna dalam mengelola file, direktori dan hak akses untuk menjaga keamanan sistem.

---

## Tugas & Quiz
### Tugas
---
Jelaskan fungsi tiap perintah dan arti kolom permission (`rwxr-xr--`). 

Fungsi tiap perintah.
| Perintah | Fungsi | Penjelasan |
| :--- | :--- | :--- |
| `pwd` | Print Working Directory | Menampilkan lokasi direktori aktif saat ini.|
| `la -l` | List (long format) | Menampilkan daftar file beserta detailnya seperti permission (`rwxr-xr--`) pemilik, grup, ukuran, dan tanggal. |
| `cd /tmp` | Change Directory | Berpindah ke direktori `/tmp`, yaitu direktori sementara di sistem Linux tempat file sementara biasanya disimpan.|
| `cat/etc/passwd` | `head -n 5` | Menampilkan 5 baris pertama dari file `/etc/passwd`, yang berisi daftar akun penguna sistem seperti `root`, `daemon`, `bin`. |
|`echo "Hello Keysya Ayu Anggita - 250202944" > percobaan.txt `| Menulis teks ke dalam file bernama `percobaan.txt`. Jika file belum ada, file baru akan dibuat.| - |
| `chmod 600 percobaan.txt` | Mengubah izin akses file `percobaan.txt` menjadi hanya dibaca dan ditulis oleh pemilik. Grup dan pengguna lain tidak punya akses | - |
| `cat percobaan.txt` | Menampilkan isi file `percobaan.txt` ke layar.| - |

Arti kolom permission (`rwxr-xr--`)
| Simbol | Keterangan | Arti |
| :--- | :--- | :--- |
| `-` | Jenis file | `-` berarti file biasa, `d` berarti direktori. |
| `rwx` | Hak akses pemilik(owner) | Pemilik file dapat membaca(`r`), menulis(`w`) dan mengeksekusi(`x`). |
| `r-x` | Hak akses grup(group) | Grup dapat membaca(`r`) dan mengeksekusi (`x`). |
| `r--` | Hak akses pengguna lain(others) | Hanya dapat membaca(`r`), tidak dapat menulis atau menjalankan. |

---
Analisis peran `chmod` dan `chown` dalam keamanan sistem Linux.
| Aspek | `chmod` | `chown` |
| :--- | :--- | :--- |
| Fungsi | Mengubah izin akses file atau direktori (`read`,`write`,`execute`)| Mengubah kepemilikan file atau direktori (user dan group) |
| Tujuan keamanan| Mengontrol siapa yang dapat membaca, menulis atau mengeksekusi file | Menentukan siapa yang memiliki kendali penuh terhadap file |
| Jenis kontrol | Bagian dari Discretionary Access Control (DAC) pengaturan hak akses | Bagian dari Discretionary Access Control (DAC) pengaturan kepemilikan |
| Penerapan | Dilakukan oleh pemilik file atau administrator untuk mengatur izin akses | Hanya dapat dilakukan oleh administrator (root) untuk mengganti pemilik file|

---

### Quiz
---
1. Apa fungsi dari perintah `chmod`?
   
   Perintah `chmod` (change mode) digunakan untuk mengatur atau mengubah hak akses (permission) pada file dan            direktori di sistem UNIX/Linux. Hak akses ini termasuk izin membaca(r), menulis(w), dan menjalankan(x) file untuk     tiga jenis pengguna, yaitu pemilik file, kelompok pengguna, dan pengguna lain.  
---
   
2. Apa arti dari kode permission `rwxr-xr--`?
   
   Kode `rwrxr-xr--` adalah bentuk izin akses (permission) pada sistem operasi UNIX/Linux yang menunjukkan hak akses     terhadap sebuah file atau direktori.
   | Kode | Keterangan |
   | :--- | :--- |
   | `-` | Jenis file tanda `-` mengartikan file data atau program biasa. |
   | `rwx`| Owner(pemilik) memiliki izin penuh read(r), write(w), dan execute(x). |
   | `r-x` | Kelompok pengguna hanya bisa  membaca dan menjalankan file, tetapi tidak bisa mengubah atau menghapusnya.|
   | `r--` | Pengguna lain hanya bisa membaca(r) file, tidak dapat menjalankan(x) atau mengeditnya(w). |
---  
3. Jelaskan perbedaan antara `chown` dan `chmod`.
   - `chown` digunakan untuk mengubah kepemilikan file atau direktori, yaitu siapa pemilik (owner) dan kelompok             (group) dari file tersebut. `chown` hanya bisa dijalankan oleh root atau pengguna dengan hak superuser, karena        mengubah kepemilikan file.
   - `chmod` digunakan untuk mengubah izin akses(permission) terhadap file atau direktori, seperti hak membaca,             menulis dan menjalankan. `chmod` dapat dijalankan oleh pemilik file itu sendiri, tanpa perlu hak administrator        dan bertujuan untuk menentukan tingkat akses yang diperbolehkan bagi masing-masing pengguna (owner, group,            others).

---

## Refleksi Diri
Tuliskan secara singkat:
- Apa bagian yang paling menantang minggu ini?
  Hal yang paling menantang minggu ini adalah memahami cara kerja izin file(permission) di Linux, terutama dalam        membedakan akses owner, group, dan others serta memahami arti kode `rw-r--r--` dan `rw-------`. Hal tersebut          membingungkan karena setiap kombinasi angka atau huruf memiliki makna tertentu terhadap akses file. 
- Bagaimana cara Anda mengatasinya?
  Mencoba langsung diterminal menggunakan perintah `chmod`, `ls -l` dan `cat`. Serta mencatat perubahan yang terjadi    sebelum dan sesudah perintah dijalankan.

---

**Credit:**  
_Template laporan praktikum Sistem Operasi (SO-202501) – Universitas Putra Bangsa_
