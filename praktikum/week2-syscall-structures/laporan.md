
# Laporan Praktikum Minggu [2]
Topik: Struktur System Call dan Fungsi Kernel 

---

## Identitas
- **Nama**  : Keysya Ayu Anggita  
- **NIM**   : 250202944
- **Kelas** : 1IKRA

---

## Tujuan
Tuliskan tujuan praktikum minggu ini.  
1. Menjelaskan konsep dan fungsi system call dalam sistem operasi.
2. Mengidentifikasi jenis-jenis system call dan fungsinya.
3. Mengamati alur perpindahan mode user ke kernel saat system call terjadi.
4. Menggunakan perintah Linux untuk menampilkan dan menganalisis system call.
---

## Dasar Teori
System call adalah metode yang digunakan oleh program aplikasi untuk berkomunikasi dengan sistem operasi. Melalui system call, program pengguna dapat meminta layanan yang disediakan kernel, seperti membaca atau menulis berkas, membuat proses baru, mengalokasikan memori, hingga berinteraksi dengan perangkat keras. Biasanya, system disediakan dalam bentuk fungsi yang ditulis menggunakan bahasa C atau C++, sedangkan operasi yang memerlukan akses langsung ke perangkat keras dapat menggunakan bahasa assembly. Panggilan sistem memungkinkan sistem operasi menjalankan tugas-tugas penting dengan cara yang aman dan terkontrol, tanpa memberikan akses langsung kepada program pengguna terhadap sumber daya perangkat keras.

Sebagai contoh, pada perintah UNIX ```cp masuk.txt keluar.txt,``` sistem operasi menjalankan serangkaian panggilan sistem seperti membuka berkas masukan, membaca isinya, membuat berkas keluaran, menulis data ke berkas tersebut, dan kemudian menutup keduanya. Setiap proses ini melibatkan perpindahan mode dari *user mode* ke *kernel mode* agar sistem dapat mengatur hak akses dan melindungi sumber daya dari kesalahan atau gangguan. Dengan demikian, system call memiliki peran penting sebagai jembatan antara perangkat lunak aplikasi dan kernel sistem operasi dalam pengelola sumber daya komputer. 

---

## Langkah Praktikum
1. **Setup Environment**
   - Gunakan Linux (Ubuntu/WSL).
   - Pastikan perintah `strace` dan `man` sudah terinstal.
   - Konfigurasikan Git (jika belum dilakukan di minggu sebelumnya).

2. **Eksperimen 1 – Analisis System Call**
   Jalankan perintah berikut:
   ```bash
   strace ls
   ```
   > Catat 5–10 system call pertama yang muncul dan jelaskan fungsinya.  
   Simpan hasil analisis ke `results/syscall_ls.txt`.

3. **Eksperimen 2 – Menelusuri System Call File I/O**
   Jalankan:
   ```bash
   strace -e trace=open,read,write,close cat /etc/passwd
   ```
   > Analisis bagaimana file dibuka, dibaca, dan ditutup oleh kernel.

4. **Eksperimen 3 – Mode User vs Kernel**
   Jalankan:
   ```bash
   dmesg | tail -n 10
   ```
   > Amati log kernel yang muncul. Apa bedanya output ini dengan output dari program biasa?

5. **Diagram Alur System Call**
   - Buat diagram yang menggambarkan alur eksekusi system call dari program user hingga kernel dan kembali lagi ke user mode.
   - Gunakan draw.io / mermaid.
   - Simpan di:
     ```
     praktikum/week2-syscall-structure/screenshots/syscall-diagram.png
     ```

6. **Commit & Push**
   ```bash
   git add .
   git commit -m "Minggu 2 - Struktur System Call dan Kernel Interaction"
   git push origin main
   ```

---

## Kode / Perintah
Tuliskan potongan kode atau perintah utama:
```bash
strace ls
```

```bash
strace -e trace=open,read,write,close cat /etc/passwd
```

```bash
dmesg | tail -n 10
```


---

## Hasil Eksekusi
Sertakan screenshot hasil percobaan atau diagram:
![alt text](<screenshots/stracels.png>)
![alt text](<screenshots/stracels01.png>)
![alt text](<screenshots/strace -e.png>)
**Tabel Observasi `strace ls` `strace -e trace=open,read,write,close cat /etc/passwd`**
| No | Nama System Call | Fungsi Utama | Keterangan |
| :--- | :--- | :--- | :--- |
| 1. | `execve()` | Menjalankan program baru | Kernel memulai eksekusi program `ls` dari `/usr/bin/ls`, ini adalah langkah pertama saat program dijalankan |
| 2. | `mmap()` |Memetakan file ke ruang memori proses | Banyak digunakan untuk memuat pustaka dinamis (seperti libs, ld-linux) |
| 3. | `mprotect()` | Mengubah izin pada area memori | Digunakan untuk mengatur bagian memori mana yang boleh dibaca, ditulis, atau dieksekusi oleh proses `ls` |
| 4. | `access()` | Mengecek izin atau keberadaan file | Mengecek file konfigurasi seperti `/etc/ld.so.preload` sebelum menjalankan pustaka dinamis |
| 5. | `statfs()` | Mengambil informasi tentang file system | Digunakan untuk mendapatkan info system file (misal: kapasitas, tipe file system) tempat direktori berada|
| 6. | `openat()` | Membuka file atau direktori relatif terhadap path tertentu | Membuka file librarysistem dan direktori target `ls`|
| 7. | `read()` | Membaca data dari file | Membaca isi library atau konfigurasi yang diperlukan oleh `ls`|
| 8. | `fstat()` | Mengambil informasi status file | Mengecek ukuran dan jenis file library atau file yang sedang diakses |
| 9. | `ioctl()`| Mengirim perintah kontrol ke perangkat | Mengecek jenis terminal agar output dapat diformat (misalnya berwarna)|
| 10.| `close()`| Menutup file descriptor | Menutup file yang tidak lagi digunakan untuk efisiensi memori |
| 11.| `write()` | Menulis data ke file | Setelah data `/etc/passwd` dalam blok tertentu (contohnya 832 byte). Data ini dimuat ke dalam buffer di memori proses pengguna |

**Tabel Observasi dmesg** 
![alt text](<screenshots/dmesg tail -nweek2.png>)
| No | Nama System Call | Fungsi Utama | Keterangan |
| :--- | :--- | :--- | :--- |
| 1. | `mount EXT4 filesystem` | Untuk memasang sistem file ke direktori agar bisa diakses |  `mounted filesystem b9f0e455... type EXT4` artinya sistem berhasil memasang partisi EXT4|
| 2. |`open() dan read()` pada `/lin/modules/...` | Digunakan untuk membaca file modul `.ko` sebelum dimuat| Kernel membuka file modul seperti `/lib/modules/6.6.105+/kernel/net/ipv4/netfilter/ipt_set.ko.` |
| 3. | `modprobe` (load module)| Memanggil system call `init_module()` untuk memuat modul kernel ke dalam memori | Terlihat dari baris `cmdline="/sbin/modprobe -q...` yang berarti modul kernel seperti `iptable_nat_ip_set,xt_set` dimuat |
| 4. | `LoadPin: kernel-module-pinning-excluded`| Mekanisme keamanan yang memverifikasi modul kernel berasal dari sumber daya terpercaya | Menunjukkan bahwa sistem keamanan LoadPin mengecualikan modul tertentu agar bisa dimuat tanpa verifikasi tambahan |

---

## Analisis
Sistem operasi berfungsi sebagai perantara antara pengguna dan perangkat keras komputer. Melalui system call, program pengguna dapat meminta layanan seperti manajemen file, proses, atau perangkat I/O tanpa harus mengakses langsung perangkat keras. Proses ini dijalankan oleh kernel, yaitu bagian inti dari sistem operasi yang memiliki kendali penuh terhadap sumber daya sistem. Kernel bekerja dalam mode khusus untuk melindungi sistem dari kesalahan atau akses yang tidak sah. Arsitektur ini menggambarkan konsep dual-mode operation, dimana user mode digunakan untuk program biasa dan kernel mode untuk eksekusi fungsi sistem. Dengan demikian, sistem operasi memastikan keamanan, stabilitas, dan efisiensi melalui pengaturan akses yang terkontrol antara pengguna, system call, dan kernel. 

---

## Kesimpulan
Dari praktik tersebuat dapat disimpulkan:
- System call digunakan sebagai penghubung antara user mode dan kernel mode.
- Saat perintah dijalankan (misalnya `sudo dmesg` atau `modprobe`), sistem melakukan pemanggilan system call ke kernel.
- Kernel memproses perintah untuk memuat modul, seperti `iptable_nat, netlink_diag,ip_set` dan `xt_set`.
- Proses ini melibatkan system call seperti `init_module(), open(), read(), mount(),` dan `statfs()` untuk mengatur file system dan modul kernel.
- Hasil menunjukkan bahwa kernel bertanggung jawab langsung terhadap manajemen perangkat, jaringan, dan keamanan sistem.

---

## Tugas  
Buat diagram alur system call dari aplikasi → kernel → hardware → kembali ke aplikasi.
   ![alt text](<screenshots/diagramweek2.png>)
   
---
**Mengapa system call penting untuk keamanan OS?**

System call merupakan metode penting dalam sistem operasi karena berfungsi sebagai penghubung antara program pengguna (user mode) dengan kernel (kernel mode). Melalui system call, program pengguna dapat meminta layanan dari sistem operasi tanpa perlu mengakses langsung sumber daya perangkat keras. Proses ini memastikan setiap permintaan pengguna harus melalui prosedur resmi dan terkontrol oleh sistem operasi. Dengan demikian, system call berperan sebagai batas pelindung yang mencegah program biasa atau berbahaya untuk menjalankan intruksi yang dapat merusak sistem atau mengambil alih kendali kernel.

Selain sebagai pintu masuk menuju kernel, system call juga berperan dalam menjaga integritas sistem melalui metode penyaringan. Setiap upaya untuk mengakses sumber daya kernel harus diperiksa dan diverifikasi, sementara yang mencurigakan akan ditolak. Contohnya pada sistem Linux terdapat fitur *SECCOMP-BPF* yang dapat membatasi jenis system call yang boleh digunakan oleh suatu program. Metode ini membantu mencegah terjadinya eksploitasi atau penyalahgunaan akses terhadap kernel. Karena itu, system call berperan penting dalam menjaga integritas dan perlindungan sistem operasi agar tetap stabildan aman dari serangan (Abraham Silberschatz, Peter Baer Galvin, Greg Gagne. Operating System Concepts, 10th Edition, Wiley, 2018 hal. 26-27, 688-689).

---
**Bagaimana OS memastikan transisi user–kernel berjalan aman?**

Sistem operasi menjaga agar perpindahan dari mode pengguna ke mode kernel berlangsung aman dengan membatasi akses pengguna melalui system call. Ketika sebuah program membutuhkan layanan dari sistem, permintaan tersebut tidak dijalankan langsung, tetapi diteruskan melalui metode trap atau interupsi perangkat lunak yang memindahkan kendali ke rutin layanan kernel. Di sana, sistem operasi akan memeriksa terlebih dahulu apakah permintaan itu sah atau tidak berpotensi membahayakan sistem sebelum mengeksekusinya. Setelah proses selesai, kendali dikembalikan dengan aman ke program pengguna. Dengan cara ini, sistem operasi memastikan bahwa tidak ada aplikasi yang dapat langsung mengubah atau mengakses sumber daya penting, sehingga keamanan dan stabilitas tetap terjaga.

---
**Sebutkan contoh system call yang sering digunakan di Linux.**
- `fork()` Membuat proses baru.
- `exec()` Menjalankan program baru.
- `exit()` Mengakhiri proses.
- `wait()` Menunggu proses anak selesai sebelum melanjutkan eksekusi.
- `open()` Membuka file untuk dibaca atau ditulis.
- `read()` Membaca data dari file atau perangkat I/O.
- `write()` Menulis data ke file atau perangkat I/O.
- `close()` Menutup file yang telah digunakan.
- `chmod()` Mengubah izin akses suatu file.
- `getpid()` Mengambil ID (identitas) proses yang sedang jalan.

---
## Quiz
1. Apa fungsi utama system call dalam sistem operasi?
   
   Fungsi utama system call adalah menghubungkan program pengguna dengan sistem operasi agar dapat meminta layanan       seperti membuka file, membuat proses, atau  membaca data tanpa mengakses perangkat keras. System call juga            memastikan setiap permintaan pengguna dijalankan melalui prosedur yang aman di kernel sehingga     mencegah           kesalahan atau gangguan pada sistem. Dengan cara ini, system call menjaga agar interaksi antara pengguna dan          sumber daya komputer tetap teratur, aman, dan efisien.
---
2. Sebutkan 4 kategori system call yang umum digunakan.
   | Kategori system call | Fungsi Utama | Contoh di Linux/UNIX |
   | :--- | :--- | :--- |
   | Process Control | Mengatur dan mengelola proses seperti membuat, menjalankan, atau mengakhiri proses.| `fork()` `ecex()` `exit()` `wait()`|
   | File Management | Melakukan operasi terhadap file seperti membuka, membaca, munulis, dan menutup file.| `open()` `read()` `write()` `close()`|
   | Pengelolaan Perangkat | Mengtur dan mengontrol penggunaan perangkat I/O | `ioctl()` `read()` `write()`|
   | Pemeliharaan Informasi | Mengambil atau memperbarui informasi tentang sistem dan proses | `getpid()` `alarm()` `sleep()`|

---
3. Mengapa system call tidak bisa dipanggil langsung oleh user program?
   
   System call tidak bisa dipanggil lansung oleh program pengguna kerena intruksi yang dijalankan bersifat khusus dan    hanya boleh dilakukan oleh kernel. Jika pengguna diizinkan menjalankan instruksi tersebut langsung, maka bisa         terjadi, kerusakan sistem atau pelanggaran keamanan. Oleh karena itu, setiap permintaan dari program pengguna         harus melalui metode system call agar dapat terverifikasi dan dijalankan dengan aman oleh kernel. 

---

## Refleksi Diri
Tuliskan secara singkat:
- Apa bagian yang paling menantang minggu ini? Memahami makna setiap system call yang muncul selama proses eksekusi.
- Bagaimana cara Anda mengatasinya? Untuk mengatasi kesulitan dalam memahami saya mencari referensi dari berbagai sumber di internet.

---

**Credit:**  
_Template laporan praktikum Sistem Operasi (SO-202501) – Universitas Putra Bangsa_
