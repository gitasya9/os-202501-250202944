
# Laporan Praktikum Minggu [1]
Topik: Arsitektur Sistem Operasi dan Kernel

---

## Identitas
- **Nama**  : Keysya Ayu Anggita
- **NIM**   : 250202944
- **Kelas** : 1IKRA

---

## Tujuan
Tuliskan tujuan praktikum minggu ini.  
1. Menggambarkan diagram sederhana arsitektur OS dengan menggunakan draw.io/mermaid.
2. Mempelajari perbedaan monolithic kernel, microkernel dan layered architecture.
3. Mengidentifikasi komponen utama  OS (kernel, system call, device driver, file system).
4. Menjelaskan peran sistem operasi dalam arsitektur komputer.

---

## Dasar Teori
Sistem operasi adalah perangkat lunak sistem yang menjadi perantara antara pengguna dan perangkat keras komputer. Sistem operasi memiliki tiga tujuan utama, yaitu kenyamanan bagi pengguna, efisiensi sumber daya, dan kemampuan untuk berkembang (evolusi) sesuai dengan kemajuan teknologi. Sistem operasi dirancang dengan beberapa modul yang berfungsi bersama dalam mengatur keseluruhan sistem komputer, seperti manajemen proses, manajemen memori, manajemen file, manajemen I/O, command interpreter.

---

## Langkah Praktikum
1. **Setup Environment**
   - Pastikan Linux (Ubuntu/WSL) sudah terinstal.
   - Pastikan Git sudah dikonfigurasi dengan benar:
     ```bash
     git config --global user.name "Nama Anda"
     git config --global user.email "email@contoh.com"
     ```

2. **Diskusi Konsep**
   - Baca materi pengantar tentang komponen OS.
   - Identifikasi komponen yang ada pada Linux/Windows/Android.

3. **Eksperimen Dasar**
   Jalankan perintah berikut di terminal:
   ```bash
   uname -a
   whoami
   lsmod | head
   dmesg | head
   ```
   Catat dan analisis modul kernel yang tampil.

4. **Membuat Diagram Arsitektur**
   - Buat diagram hubungan antara *User → System Call → Kernel → Hardware.*
   - Gunakan **draw.io** atau **Mermaid**.
   - Simpan hasilnya di:
     ```
     praktikum/week1-intro-arsitektur-os/screenshots/diagram-os.png
     ```

5. **Penulisan Laporan**
   - Tuliskan hasil pengamatan, analisis, dan kesimpulan ke dalam `laporan.md`.
   - Tambahkan screenshot hasil terminal ke folder `screenshots/`.

6. **Commit & Push**
   ```bash
   git add .
   git commit -m "Minggu 1 - Arsitektur Sistem Operasi dan Kernel"
   git push origin main
   ```

---

## Kode / Perintah
Tuliskan potongan kode atau perintah utama:
```bash
uname -a
lsmod | head
dmesg | head
```

---

## Hasil Eksekusi
Sertakan screenshot hasil percobaan atau diagram:
![alt text](<screenshots/ss eca.png>)
![alt text](<screenshots/ss diagram.png>)

---

## Analisis
- Jelaskan makna hasil percobaan.
  
  Diagram arsitektur OS menggambarkan bagaimana sistem operasi menjadi penghubung antara aplikasi pengguna dan          perangkat keras, dan bagaimana struktur modular (layered) membuat sistem lebih mudah dikendalikan dan dikembangkan.
```
   Linux cs-841469559957-default 6.6.105+ #1 SMP PREEMPT_DYNAMIC Sat Sep 27 08:48:45 UTC 2025 x86_64 x86_64 x86_64 GNU/Linux
 ```
Menunjukan bahwa kernel yang digunakan adalah Linux kernel dengan menggunakan sistem kernel Linux 6.6.105+ dengan dukungan multi-core (SMP) dan preemptive dynamic, cocok untuk yang membutuhkan responsivitas tinggi. Kernel ini berjalan pada arsitektur 64-bit (x86_64) dan menggunakan siste operasi berbasis GNU/Linux. Hostname menunjukan sistem ini kemungkinanberjalan di lingkungan virtual atau cloud, seperti AWS, GCP, atau WSL.
 ```
Module                  Size  Used by
ip6table_nat           12288  1
xt_set                 20480  0
ip_set                 53248  1 xt_set
netlink_diag           12288  0
iptable_nat            12288  1
xt_nat                 12288  6
xt_mark                12288  1
veth                   36864  0
nft_limit              16384  1
 ```
Menunjukan modul (driver) apa saja yang dimuat ke dalam kernel dan memberikan gambaran bahwa kernel Linux bersifat modular, artinya fitur-fitur kernel dapat dimuat/dilepas tanpa reboot.
```
[    0.000000] Linux version 6.6.105+ (builder@2832f747b46d) (Chromium OS 17.0_pre498229-r33 clang version 17.0.0 (/var/cache/chromeos-cache/distfiles/egit-src/external/github.com/llvm/llvm-project 14f0776550b5a49e1c42f49a00213f7f3fa047bf), LLD 17.0.0) #1 SMP PREEMPT_DYNAMIC Sat Sep 27 08:48:45 UTC 2025
[    0.000000] Command line: BOOT_IMAGE=/syslinux/vmlinuz.A init=/usr/lib/systemd/systemd rootwait ro noresume loglevel=7 console=tty1 console=ttyS0,115200 security=apparmor virtio_net.napi_tx=1 nmi_watchdog=0 csm.disabled=1 loadpin.exclude=kernel-module,firmware modules-load=loadpin_trigger firmware_class.path=/var/lib/nvidia/firmware module.sig_enforce=1 dm_verity.error_behavior=3 dm_verity.max_bios=-1 dm_verity.dev_wait=1 i915.modeset=1 cros_efi root=/dev/dm-0 "dm-mod.create=vroot,,,ro,0 4077568 verity 0 PARTUUID=7BCC9916-089B-5741-BDB4-BBF2531D61CC PARTUUID=7BCC9916-089B-5741-BDB4-BBF2531D61CC 4096 4096 509696 509696 sha256 cd005c970a2f850726894bf85289300eaf8bb857b72888c81584d6c76887edb1 495a0ee73578f50cbe5c9e99905ea2149e061977f71182962a65c0e169274c5b"
[    0.000000] BIOS-provided physical RAM map:
[    0.000000] BIOS-e820: [mem 0x0000000000000000-0x0000000000000fff] reserved
[    0.000000] BIOS-e820: [mem 0x0000000000001000-0x0000000000054fff] usable
[    0.000000] BIOS-e820: [mem 0x0000000000055000-0x000000000005ffff] reserved
[    0.000000] BIOS-e820: [mem 0x0000000000060000-0x0000000000097fff] usable
[    0.000000] BIOS-e820: [mem 0x0000000000098000-0x000000000009ffff] reserved
[    0.000000] BIOS-e820: [mem 0x0000000000100000-0x00000000bd221fff] usable
[    0.000000] BIOS-e820: [mem 0x00000000bd222000-0x00000000bd223fff] ACPI data
```
```dmesg``` memberikan wawasan langsung ke dalam proses booting dan interaksi kernel dengan perangkat keras 
- Hubungkan hasil dengan teori (fungsi kernel, system call, arsitektur OS).

  Kernel berperan menjadi penghubung utama antara perangkat keras dan perangkat lunak, serta bertanggung jawab          terhadap manajemen sumber daya sistem. Hasil percobaan mendukung teori bahwa system call adalah jembatan penting      bagi program pengguna untuk berinteraksi dengan layanan yang disediakan oleh kernel, memastikan bahwa sistem dapat    berjalan dengan aman dan terkontrol. Arsitektur OS sebagai kerangka utama yang mengatur bagaimana komponen-komponen   dalam komputer (perangkat lunak dan perangkat keras) saling berinteraksi secara efisien dan aman. 
- Apa perbedaan hasil di lingkungan OS berbeda (Linux vs Windows)?
  
  Linux :  menggunakan kernel monolithic (semua fungsi utama OS berjalan di dalam kernel), dengan akses sistem          melalui terminal/command line pengguna bisa langsung melihat informasi kernel dan modul.
  
  Windows : menggunakan kernel hybrid (gabungan antara monolithic dan microkernel), lebih membatasi akses ke level      keamanan sistem dan kemudahan penggunaan.

---

## Kesimpulan
- Dari hasil percobaan, bahwa kernel adalah bagian utama dari sistem operasi yang menghubungkan antara aplikasi dan     perangkat keras, serta mengatur semua aktivitas di dalam komputer.
- Linux dengan kernel Monolithic lebih transparan dan fleksibel, sedangkan Windows dengan kernel Hybrid lebih           berorientasi pada keamanan dan kemudahan pengguna.  

---

## Tugas & Quiz 
## Tugas
1. Perbedaan monolithic kernel, microkernel, dan layered architecture

    **Jawaban:**
   
   **a. Monolithic Kernel**
   
   Struktur paling sederhana untuk mengorganisir sistem operasi adalah tanpa struktur sama sekali. Semua fungsi inti dari sistem operasi seperti penjadwalan CPU, sistem file, manajemen waktu, dan driver perangkat keras digabungkan ke dalam satu program besar yang berjalan dalam satu ruang alamat. Kinerja Monolithic kernel umumnya lebih cepat, karena tidak ada overhead yang terkait dengan pemindahan data antar ruang kernel dan ruang pengguna. Namun, Monolithic kernel lebih rentan terhadap masalah keamanan karena semua berada dalam satu komponen crash. Contoh sistem operasi dengan model ini adalah UNIX, Linux, dan Windows.
   
   **b. Microkernel**
   
   Sistem operasi yang menghapus semua komponen yang tidak penting dari kernel dan menerapkannya sebagai program tingkat pengguna (user-level) yang berada di ruang alamat kecil. Namun, tidak ada persetujuan yang jelas mengenai layanan mana yang harus tetap berada di dalam kernel dan mana yang harus diterapkan di ruang pengguna. Mikrokernel umumnya hanya menyediakan manajemen proses dan memori secara minimal, serta fasilitas komunikasi. Keuntungan dari mikrokernel adalah membuat sistem operasi lebih mudah dikembangkan. Semua layanan baru ditambahkan ke ruang pengguna, sehingga tidak perlu mengubah kernel. Jika kernel perlu diubah, perubahan yang dilakukan cenderung sedikit karena ukurannya kecil. Sistem operasi yang dihasilkan lebih mudah dipindahkan (porting) ke desain perangkat keras yang berbeda. Selain itu, mikrokernel memberikan keamanan dan keandalan yang lebih tinggi, karena sebagian besar layanan berjalan sebagai proses pengguna, bukan proses kernel. Jika sebuah layanan mengalami kegagalan, bagian sistem operasi lainnya tidak akan terpengaruh. Contoh sistem operasi dengan model ini adalah Minix, QNX, Amoeba.
   
   **c. Layered Architecture**
   
   Sistem operasi yang dipecah menjadi sejumlah lapisan (tingkatan). Lapisan paling bawah adalah perangkat keras (hardware), lapisan paling atas adalah antarmuka pengguna (user interface). Sebuah lapisan sistem operasi adalah penerapan dari objek abstrak yang terdiri atas struktur data dan operasi yang dapat memanipulasi data tersebut. Keuntungan utama dari pendekatan bertingkat adalah kesederhanaan dalam pembangunan dan debugging. Lapisan-lapisan dipilih sedemikian rupa sehingga masing-masing hanya menggunakan fungsi dan layanan dari lapisan yang lebih rendah. Pendekatan tersebut dapat menyederhanakan proses debugging dan verifikasi sistem. Contoh sistem operasi dengan model ini adalah THE Operating system, MULTICS.
   
2. Contoh OS yang menerapkan tiap model.  
   **Jawaban:**
 
   **a. Monolithic kernel**
   
   UNIX : sistem operasi multitasking, multiuser (mengakses sistem secara bersamaan)
   
   Linux : bebas, terbuka, dan dapat dimodifikasi oleh siapa saja
   
   Windows : sistem operasi berbasis antarmuka grafis yang mrmudahkan pengguna untuk menjalankan aplikasi dan
   mengelola perangkat keras komputer

   **b. Microkernel**

   Minix : diciptakan untuk pendidikan dan pengembangan perangkat lunak

   QNX : dikembangkan untuk aplikasi industri, otomotif, alat medis, dan perangkat lunak yang aman dan andal

   Amoeba : membuat sekelompok komputer tampak seperti satu sistem tunggal bagi pengguna

   **c. Layered Architecture**

   THE Operating system : kejelaan struktur, bukan peforma

   MULTICS : sistem operasi berbasis time-sharing
   
3. Analisis: model mana yang paling relevan untuk sistem modern.  
   **Jawaban:**
   Model yang lebih relevan untuk masa modern ini adalah Monolithic kernel. Karena dari performa yang tinggi semua       komponen inti sistem (manajemen memori, device driver, file system, dll) berjalan di satu ruang kernel, tidak ada     pemisahan proses antar modul menjadikan sistem berjalan lebih cepat dan efisien. Hal tersebut membuat proses          komunikasi internal menjadi lebih cepat dan ringan. Contohnya adalah aplikasi Adobe Premiere Pro, Adobe Premiere      Pro adalah salah satu software penyunting video yang sangat fleksibel, memungkinkan pengguna untuk mengedit video     dengan kualitas yang tinggi. Adobe Premiere Pro dapat dipasang di Windows dan macOS. Kedua sistem operasi tersebut    di bangun di atas arsitektur monolithic kernel, yang memungkinkan pengelola sumber daya sistem secara tepat dan       mendukung performa tinggi saat menjalankan aplikasi berat seperti video editing.
   
## Quiz
1. Sebutkan tiga fungsi utama sistem operasi.
   
   **Jawaban:**
   - Manajemen sumber daya
   - Manajemen proses dan file
   - Penyediaan antarmuka pengguna (user interface)
2. Jelaskan perbedaan antara kernel mode dan user mode.
   
   **Jawaban:**
   
   Kernel mode mempunyai akses penuh ke seluruh sistem dan perangkat keras, sedangkan user mode memiliki akses           terbatas tidak bisa langsung mengakses hardware. Perbedaan tersebut yaitu untuk melindungi sistem operasi dari        gangguan atau kesalahan yang dilakukan oleh aplikasi pengguna.  
3. Sebutkan contoh OS dengan arsitektur monolithic dan microkernel.
   
   **Jawaban:**
   - Monolithic: UNIX, Linux, Windows
   - Microkernel: Minix, QNX, Amoeba

---

## Refleksi Diri
Tuliskan secara singkat:
- Apa bagian yang paling menantang minggu ini?
  Hal yang menantang pada minggu ini adalah memahami konsep arsitektur OS (monolithic kernel, microkernel dan layered   architecture) dan menganalisis hasil dari perintah seperti lsmod, dmesg, dan uname -a, karena memebutuhkan            pemahaman tentang cara kerja kernel serta modul-modul sistem.
- Bagaimana cara Anda mengatasinya?
  Cara mengatasinya tantangan tersebut, saya mencari referensi tambahan dari internet seperti google ataupun youtube    dan referensi tambahan dari buku *Operating System Concepts* karya Abraham Silberschatz. Saya juga berdiskusi dan     menanyakan hal-hal yang belum saya pahami kepada teman agar mendapatkan sudut pandang lain dan memperkuat pemahaman   saya terhadap materi yang di praktikkan.

---

**Credit:**  
_Template laporan praktikum Sistem Operasi (SO-202501) – Universitas Putra Bangsa_
