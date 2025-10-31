
# Laporan Praktikum Minggu [4]
Topik: Manajemen Proses dan User di Linux

---

## Identitas
- **Nama**  : Keysya Ayu Anggita 
- **NIM**   : 250202944
- **Kelas** : 1IKRA

---

## Tujuan
1. Menjelaskan konsep proses dan user dalam sistem operasi Linux.  
2. Menampilkan daftar proses yang sedang berjalan dan statusnya.  
3. Menggunakan perintah untuk membuat dan mengelola user.  
4. Menghentikan atau mengontrol proses tertentu menggunakan PID.  
5. Menjelaskan kaitan antara manajemen user dan keamanan sistem.

---

## Dasar Teori
Manajemen proses merupakan salah satu fungsi utama sistem operasi Linux yang bertugas mengatur pembuatan, eksekusi, dan penghentian proses. Proses merupakan program yang sedang dijalankan dan menjadi unit dasar kerja sistem operasi. Setiap proses memiliki identitas unik yang disebut **Process ID (PID)** serta dapat membentuk hubungan hierarkis antara proses induk dan proses anak melalui sistem panggilan `fork()` dan `exec()`. Struktur proses di Linux membentuk process tree yang berawal dari proses utama seperti init atau systemd. Kernel bertanggung jawab dalam penjadwalan proses berdasarkan prioritas dan kebijakan tertentu, seperti time sharing, sedangkan pemantauan dan pengendalian proses dapat dilakukan menggunakan perintah seperti `ps`, `top`, `kill`, dan `nice`.

Selain manajemen proses, Linux juga memiliki sistem manajemen pengguna yang berfungsi mengatur hak akses dan keamanan sistem. Pengelolaan pengguna (user management) memastikan sistem multiuser dapat berjalan dengan aman dan efisien. Setiap pengguna diidentifikasi melalui User ID (UID) dan Group ID (GID) yang menentukan hak akses terhadap file, direktori, dan proses. Terdapat tiga jenis pengguna utama, yaitu **root user (superuser)** dengan hak penuh, regular user dengan hak terbatas, dan system user yang digunakan untuk menjalankan layanan sistem. Pengelolaan pengguna dilakukan melalui berkas konfigurasi seperti `/etc/passwd`, `/etc/shadow`, dan `/etc/group`, serta menggunakan perintah seperti `adduser`, `usermod`, dan `passwd`.

---

## Langkah Praktikum
1. **Setup Environment**
   - Gunakan Linux (Ubuntu/WSL).  
   - Pastikan Anda sudah login sebagai user non-root.  
   - Siapkan folder kerja:
     ```
     praktikum/week4-proses-user/
     ```

2. **Eksperimen 1 – Identitas User**
   Jalankan perintah berikut:
   ```bash
   whoami
   id
   groups
   ```
   - Jelaskan setiap output dan fungsinya.  
   - Buat user baru (jika memiliki izin sudo):
     ```bash
     sudo adduser praktikan
     sudo passwd praktikan
     ```
   - Uji login ke user baru.

3. **Eksperimen 2 – Monitoring Proses**
   Jalankan:
   ```bash
   ps aux | head -10
   top -n 1
   ```
   - Jelaskan kolom penting seperti PID, USER, %CPU, %MEM, COMMAND.  
   - Simpan tangkapan layar `top` ke:
     ```
     praktikum/week4-proses-user/screenshots/top.png
     ```

4. **Eksperimen 3 – Kontrol Proses**
   - Jalankan program latar belakang:
     ```bash
     sleep 1000 &
     ps aux | grep sleep
     ```
   - Catat PID proses `sleep`.  
   - Hentikan proses:
     ```bash
     kill <PID>
     ```
   - Pastikan proses telah berhenti dengan `ps aux | grep sleep`.

5. **Eksperimen 4 – Analisis Hierarki Proses**
   Jalankan:
   ```bash
   pstree -p | head -20
   ```
   - Amati hierarki proses dan identifikasi proses induk (`init`/`systemd`).  
   - Catat hasilnya dalam laporan.

6. **Commit & Push**
   ```bash
   git add .
   git commit -m "Minggu 4 - Manajemen Proses & User"
   git push origin main
   ```

---

---

## Kode / Perintah
Tuliskan potongan kode atau perintah utama:
```bash
whoami
id
groups
```
```bash
sudo adduser praktikan
sudo passwd praktikan
```
```bash
ps aux | head -10
top -n 1
```
```bash
sleep 1000 &
ps aux | grep sleep
```
```bash
kill 1048
```
```bash
pstree -p | head -20
```

---

## Hasil Eksekusi

### Eksperimen 1 - Identitas User
![alt text](<screenshots/user-week4.png>)
| Perintah | Fungsi Utama | Hasil Output|
| :--- | :--- | :--- |
| `whoami` | Menampilkan nama user yang sedang aktif atau login di shell. | `keysyagita` |
| `id`| Menampilkan UID, GID dan grup user | `uid=1000(keysyagita) gid=1000(keysyagita) groups=1000(keysyagita),4(adm),24(cdrom),27(sudo),30(dip),46(plugdev),110(lxd)`|
| `groups` | Menampilkan daftar grup tempat user saat ini bergabung. | `keysyagita adm cdrom sudo dip plugdev lxd` |
| `sudo adduser praktikan` | Membuat user baru bernama `praktikan` | `Adding user` `praktikan |
| `su - praktikan` | Berpindh dari user `keysyagita` ke `praktikan` | `praktikan@keysyagita`|
| `whoami` | Verifikasi user saat ini setelah berpindah | `praktikan`|

---
### Eksperimen 2 - Monitoring Proses
```
praktikan@keysyagita:~$ ps aux | head -10
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root           1  0.0  0.5 100716 11676 ?        Ss   11:21   0:02 /sbin/init
root           2  0.0  0.0      0     0 ?        S    11:21   0:00 [kthreadd]
root           3  0.0  0.0      0     0 ?        I<   11:21   0:00 [rcu_gp]
root           4  0.0  0.0      0     0 ?        I<   11:21   0:00 [rcu_par_gp]
root           5  0.0  0.0      0     0 ?        I<   11:21   0:00 [slub_flushwq]
root           6  0.0  0.0      0     0 ?        I<   11:21   0:00 [netns]
root           8  0.0  0.0      0     0 ?        I<   11:21   0:00 [kworker/0:0H-events_highpri]
root          10  0.0  0.0      0     0 ?        I<   11:21   0:00 [mm_percpu_wq]
root          11  0.0  0.0      0     0 ?        S    11:21   0:00 [rcu_tasks_rude_]

```
![alt text](<screenshots/top-week4.png>)
Kolom penting pada `ps aux` dan `top`
| Kolom | Fungsi |
| :--- | :--- |
| `PID` | Nomor unik digunakan untuk setiap proses di sistem. Digunakan untuk mengontrol proses, misalnya untuk menhentikan dengan `kill PID` |
| `USER` | Menunjukkan siapa pemilik proses|
| `%CPU` | Presentase penggunaan CPU oleh proses tersebut|
| `%MEM` | Presentase penggunaan RAM oleh proses tersebut dibanding total RAM sistem. |
| `VSZ`(ps aux) | Jumlah total memori virtual yang digunakan proses (dalam KB).|
| `RSS` (ps aux) | Jumlah RAM fisik yang sedang benar-benar dipakai oleh proses. |
| `TTY` (ps aux) | Menunjukkan terminal tempat proses dijalankan. |
| `COMMAND` | Nama program atau perintah yang dijalankan oleh proses tersebut. |

- Perintah `ps aux` menampilkan daftar proses sekali saja, sedangkan `top` memantau proses secara terus menerus. 

---
### Eksperimen 3 - Kontrol Proses
![alt text](<screenshots/sleep-week4.png>)
1. `sleep 1000 &` : Menjalankan proses `sleep` selama 1000 detik di background dengan simbol (`&`), sehingga terminal tetap bisa digunakan. Hasil `[1] 1764` menunjukkan job nomor 1 dengan PID `1764`, yaitu identitas proses tersebut.
2. `ps aux | grep sleep` : Menampilkan semua proses aktif dan menyaring yang mengandung kata `sleep`. Hasil menunjukkan proses `sleep 1000` dengan PID `1764` masih berjalan.
3. `kill 1764` : Menghentikan proses dengan PID `1764`. Setelah dijalankan, muncul pesan `[1]+  Terminated sleep 1000`, menandakan proses berhasil terhentikan.
4. `ps aux | grep sleep` (pengecekan ulang): Memastikan proses `sleep` sudah berhenti. Hasilnya hanya menampilkan `grep sleep`, artinya proses dengan PID `1764` sudah tidak aktif lagi. 

---
### Eksperimen 4 - Analisis Hierarki Proses
```
praktikan@keysyagita:~$ pstree -p | head -20
systemd(1)-+-ModemManager(705)-+-{ModemManager}(714)
           |                   `-{ModemManager}(717)
           |-agetty(674)
           |-cron(650)
           |-dbus-daemon(651)
           |-multipathd(410)-+-{multipathd}(415)
           |                 |-{multipathd}(416)
           |                 |-{multipathd}(417)
           |                 |-{multipathd}(418)
           |                 |-{multipathd}(419)
           |                 `-{multipathd}(420)
           |-networkd-dispat(658)
           |-packagekitd(1542)-+-{packagekitd}(1543)
           |                   `-{packagekitd}(1544)
           |-polkitd(659)-+-{polkitd}(680)
           |              `-{polkitd}(702)
           |-rsyslogd(660)-+-{rsyslogd}(687)
           |               |-{rsyslogd}(688)
           |               `-{rsyslogd}(692)
           |-snapd(663)-+-{snapd}(739)
```
* Perintah `pstree -p | head -20` menampilkan struktur proses Linux dalam bentuk pohon beserta PID masing-masing dan hanya menampilkan 20 baris pertama. Hasilnya menunjukkan `systemd(1)` sebagai proses induk utama yang menjalankan proses lain seperti `dbus-daemon`, `ModemManager` dan `cron`. Perintah ini berguna untuk melihat hubungan induk-anak antarproses di sistem.
  
---

## Analisis
1. **Eksperimen 1:** Pada eksperimen ini dilakukan pembuatan user baru bernama praktikan menggunakan perintah `sudo adduser praktikan`, lalu masuk ke user tersebut dengan `su - praktikan`. Hasilnya menunjukkan bahwa sistem berhasil membuat dan mengganti sesi ke user baru. Ini menunjukkan bahwa manajemen user di Linux berjalan dengan baik dan perintah `whoami` dapat digunakan untuk memastikan identitas user aktif.
2. **Eksperimen 2:** Perintah `top` digunakan untuk memantau proses yang sedang berjalan secara real time. Hasil menampilkan kolom penting seperti **PID, USER, %CPU, %MEM dan COMMAND** yang menunjukkan identitas proses, pemiliknya, serta konsumsi sumber daya CPU dan memori. Eksperimen ini memperlihatkan bagaimana sistem Linux menangani banyak proses sekaligus dan memungkinkan pengguna memantau kinerja sistem.
3. **Eksperimen 3:** Perintah `sleep 1000 &` digunakan untuk menjalankan proses di background, lalu di periksa menggunakan `ps aux | grep sleep`. Setelah itu, proses dihentikan dengan `kill`. Hasil menunjukkan bagaimana proses dapat dijalankan, dipantau dan dihentikan menggunakan PID. Hal tersebut membuktikan pemahaman dasar tentang manajemen proses di Linux, yaitu membuat, memantau dan menghentikan proses.
4. **Eksperimen 4:** Perintah `pstree -p` digunakan untuk menampilkan struktur hierarki proses dalam bentuk pohon. Dari hasil terlihat bahwa `systemd(1)` adalah proses induk utama yang menjalankan seluruh proses lain di sistem. Eksperimen ini menunjukkan hubungan antara proses induk dan proses anak, serta bagaimana sistem Linux mengatur proses secara terstruktur sejak sistem dijalankan.
   
---
**Hubungan antara user management dan keamanan sistem Linux** 

Manajemen user berperan penting dalam keamanan Linux karena mengatur akses pengguna terhadap sumber daya sistem. Dengan UID, GID dan prinsip *least privilage*, setiap user hanya mendapat hak sesuai kebutuhannya. Penggunaan `sudo` menggantikan akses langsung ke `root` untuk mencegah penyalahgunaan, sementara izin file (`read`, `write`, `execute`), `setuid`/`setgid`, dan role-based access control (RBAC) menjaga agar hanya pengguna berwenang yang dapat melakukan tindakan tertentu. 

---

## Kesimpulan
- Kombinasi penggunaan `whoami`, `id` dan `sudo` menunjukkan bagaimana Linux menjaga keamanan sistem melalui kontrol akses berbasis identitas pengguna.
- Setiap proses memiliki identitas unik (PID) dan USER yang membantu dalam identifikasi serta pengelola sumber daya sistem.
- Proses di Linux dapat dijalankan, dipantau dan dihentikan menggunakan perintah seperti `ps`, `top` dan `kill`.
- Manajemen user dan proses membantu menjaga stabilitas serta efisiensi kerja sistem Linux.

---

## Quiz

**1. Apa fungsi dari proses `init` atau `systemd` dalam sistem Linux?**

   Proses `init` atau `systemd` dalam sistem Linux yang berfungsi sebagai proses pertama yang dijalankan oleh kernel     setelah sistem booting dan menjadi induk dari semua proses lain. Proses ini bertanggung jawab untuk                   menginisialisasi lingkungan sistem, menjalankan layanan dan daemon penting, serta mengelola siklus hidup proses       selama sistem berjalan. Pada versi Linux modern, `systemd` menggantikan fungsi `init` dengan manajemen layanan        yang lebih efisien dan memastikan seluruh komponen sistem berjalan teratur sejak boot hingga shutdown.

---
     
**2. Apa perbedaan antara `kill` dan `killall`?**
  - `kill` menerima nomor ID proses sebagai argumen dan hanya mematikan satu proses pada satu waktu, kecuali jika          beberapa ID proses ditentukan sekaligus dalam satu perintah.
  - `killall` memungkinkan penghentian proses berdasarkan nama program (name)ndan akan mengakhiri semua proses yang        memiliki nama yang sama.
---

**3. Mengapa user `root` memiliki hak istimewa di sistem Linux?**

Dalam sistem operasi Linux, user root atau disebut juga superuser adalah pengguna dengan hak akses tertinggi yang memiliki kendali penuh terhadap seluruh sumber daya sistem. Sistem operasi memberikan kontrol akses yang ketat agar hanya pengguna tertentu yang dapat melakukan tindakan kritis seperti mengubah konfigurasi, menginstal perangkat lunak atau mengelola pengguna lain. Oleh karena itu, `root` diberikan hak istimewa untuk melakukan semua operasi tanpa batasan demi menjaga pengelolaan dan pemeliharaan sistem, termasuk memperbaiki kesalahan, mengatur keamanan, dan mengendalikan seluruh proses sistem.

---

## Refleksi Diri
Tuliskan secara singkat:
- Apa bagian yang paling menantang minggu ini?  
- Bagaimana cara Anda mengatasinya?  

---

**Credit:**  
_Template laporan praktikum Sistem Operasi (SO-202501) – Universitas Putra Bangsa_
