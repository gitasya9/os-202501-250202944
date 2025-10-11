
# Laporan Praktikum Minggu [X]
Topik: [Tuliskan judul topik, misalnya "Arsitektur Sistem Operasi dan Kernel"]

---

## Identitas
- **Nama**  : Keysya Ayu Anggita
- **NIM**   : 250202944
- **Kelas** : 1IKRA

---

## Tujuan
Tuliskan tujuan praktikum minggu ini.  
1. 

---

## Dasar Teori
Tuliskan ringkasan teori (3–5 poin) yang mendasari percobaan.

---

## Langkah Praktikum
1. Langkah-langkah yang dilakukan.  
2. Perintah yang dijalankan.  
3. File dan kode yang dibuat.  
4. Commit message yang digunakan.

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

---

## Analisis
- Jelaskan makna hasil percobaan.  
- Hubungkan hasil dengan teori (fungsi kernel, system call, arsitektur OS).  
- Apa perbedaan hasil di lingkungan OS berbeda (Linux vs Windows)?  

---

## Kesimpulan
Tuliskan 2–3 poin kesimpulan dari praktikum ini.

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
- Bagaimana cara Anda mengatasinya?  

---

**Credit:**  
_Template laporan praktikum Sistem Operasi (SO-202501) – Universitas Putra Bangsa_
