
# Laporan Praktikum Minggu [7]
Topik: Sinkronisasi Proses dan Masalah Deadlock 

---

## Identitas Kelompok
**Nama**  :
1. Putri Amaliya Rahmadani (250202924)
2. Rafika Rahma (250202917)
3. Keysya Ayu Anggita (250202944)

**Kelas** : 1 IKRA

---
## Pendahuluan
Dalam sistem operasi, banyak proses sering berjalan pada waktu yang hampir bersamaan. Agar semua proses dapat berfungsi dengan baik dan tidak saling mengganggu, diperlukan mekanisme sinkronisasi yang mengatur bagaimana proses berbagi dan menggunakan sumber daya. Tanpa pengaturan yang tepat, sistem dapat mengalami deadlock, yaitu keadaan ketika beberapa proses berhenti total karena saling menunggu sumber daya yang tidak pernah tersedia. Situasi seperti ini merugikan karena membuat sistem tidak dapat bekerja secara optimal.

Untuk memahami permasalahan tersebut, praktikum ini menggunakan Dining Philosophers Problem sebagai contoh. Masalah ini menjelaskan lima proses (filosof) yang harus berbagi sumber daya terbatas (fork), menjadikannya alat yang ideal untuk menganalisis deadlock dan menerapkan mekanisme pencegahan.

Pada praktikum, mahasiswa menguji dua versi implementasi: versi pertama yang membiarkan proses berjalan tanpa pencegahan deadlock, dan versi kedua yang menggunakan mekanisme sinkronisasi seperti semaphore atau monitor. Melalui perbandingan kedua versi ini, mahasiswa dapat melihat secara langsung bagaimana deadlock terjadi serta bagaimana solusi sinkronisasi dapat mencegahnya.

---

## Tujuan
Tuliskan tujuan praktikum minggu ini.  
1. Mengidentifikasi empat kondisi penyebab deadlock (*mutual exclusion, hold and wait, no preemption, circular wait*). 
2. Menjelaskan mekanisme sinkronisasi menggunakan *semaphore* atau *monitor*.  
3. Menganalisis dan memberikan solusi untuk kasus deadlock.  
4. Berkolaborasi dalam tim untuk menyusun laporan analisis.  
5. Menyajikan hasil studi kasus secara sistematis.
   
---
## Dasar Teori
Deadlock adalah keadaan dalam sistem operasi di mana dua atau lebih proses tidak dapat melanjutkan eksekusinya karena masing-masing saling menunggu sumber daya yang sedang digunakan oleh proses lain. Kondisi ini menyebabkan proses-proses tersebut terhenti secara permanen, sehingga tidak ada satupun yang dapat bergerak maju. Deadlock sering muncul pada lingkungan multitasking yang melibatkan alokasi sumber daya secara bersamaan, seperti perangkat keras, file, lock, atau variabel sinkronisasi.

Dalam sistem komputer, deadlock biasanya terjadi ketika proses membutuhkan lebih dari satu sumber daya untuk menyelesaikan pekerjaannya. Ketika sumber daya terbatas atau bersifat eksklusif, proses dapat terjebak dalam situasi saling menunggu yang tidak dapat diselesaikan tanpa intervensi dari sistem operasi. Untuk menganalisis kondisi ini, sistem umumnya menggunakan model hubungan antara proses dan sumber daya, misalnya melalui resource-allocation graph, untuk melihat pola menunggu yang berpotensi membentuk siklus.

Deadlock hanya terjadi apabila empat kondisi berikut muncul secara bersamaan.
- Mutual Exclusion - sumber daya hanya dapat digunakan oleh satu proses pada satu waktu.
- Hold and Wait - proses memegang satu sumber daya sambil menunggu sumber daya lain yang masih digunakan proses lain.
- No Preemption - tidak dapat diambil paksa oleh sistem dan hanya dilepas secara sukarela.
- Circular Wait - rantai proses yang saling menunggu sumber daya satu sama lain dalam pola melingkar.
  
---

## Langkah Pengerjaan
1. **Persiapan Tim**
   - Bentuk kelompok beranggotakan 3–4 orang.  
   - Tentukan ketua dan pembagian tugas (analisis, implementasi, dokumentasi).

2. **Eksperimen 1 – Simulasi Dining Philosophers (Deadlock Version)**
   - Implementasikan versi sederhana dari masalah *Dining Philosophers* tanpa mekanisme pencegahan deadlock.  
   - Contoh pseudocode:
     ```text
       while true:
       think()
       pick_left_fork()
       pick_right_fork()
       eat()
       put_left_fork()
       put_right_fork()
     ```
   - Jalankan simulasi atau analisis alur (boleh menggunakan pseudocode atau diagram alur).  
   - Identifikasi kapan dan mengapa deadlock terjadi.

3. **Eksperimen 2 – Versi Fixed (Menggunakan Semaphore / Monitor)**
   - Modifikasi pseudocode agar deadlock tidak terjadi, misalnya:
     - Menggunakan *semaphore (mutex)* untuk mengontrol akses.
     - Membatasi jumlah filosof yang dapat makan bersamaan (max 4).  
     - Mengatur urutan pengambilan garpu (misal, filosof terakhir mengambil secara terbalik).  
   - Analisis hasil modifikasi dan buktikan bahwa deadlock telah dihindari.

4. **Eksperimen 3 – Analisis Deadlock**
   - Jelaskan empat kondisi deadlock dari versi pertama dan bagaimana kondisi tersebut dipecahkan pada versi fixed.  
   - Sajikan hasil analisis dalam tabel seperti contoh berikut:

     | Kondisi Deadlock | Terjadi di Versi Deadlock | Solusi di Versi Fixed |
     |------------------|---------------------------|------------------------|
     | Mutual Exclusion | Ya (satu garpu hanya satu proses) | Gunakan semaphore untuk kontrol akses |
     | Hold and Wait | Ya | Hindari proses menahan lebih dari satu sumber daya |
     | No Preemption | Ya | Tidak ada mekanisme pelepasan paksa |
     | Circular Wait | Ya | Ubah urutan pengambilan sumber daya |

5. **Eksperimen 4 – Dokumentasi**
   - Simpan semua diagram, screenshot simulasi, dan hasil diskusi di:
     ```
     praktikum/week7-concurrency-deadlock/screenshots/
     ```
   - Tuliskan laporan kelompok di `laporan.md` (format IMRaD singkat: *Pendahuluan, Metode, Hasil, Analisis, Diskusi*).

6. **Commit & Push**
   ```bash
   git add .
   git commit -m "Minggu 7 - Sinkronisasi Proses & Deadlock"
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
### Eksperimen 1 – Simulasi Dining Philosophers (Deadlock Version)
![alt text](<screenshots/deadlock.png>)

**Output**
```
Filosof 0 siap...
Filosof 1 siap...
Filosof 2 siap...
Filosof 3 siap...
Filosof 4 siap...
Filosof 4 mencoba mengambil garpu kiri
Filosof 4 berhasil mengambil garpu kiri
Filosof 3 mencoba mengambil garpu kiri
Filosof 3 berhasil mengambil garpu kiri
Filosof 1 mencoba mengambil garpu kiri
Filosof 1 berhasil mengambil garpu kiri
Filosof 0 mencoba mengambil garpu kiri
Filosof 0 berhasil mengambil garpu kiri
Filosof 2 mencoba mengambil garpu kiri
Filosof 2 berhasil mengambil garpu kiri
Filosof 0 mencoba mengambil garpu kiri
Filosof 0 berhasil mengambil garpu kiri
Filosof 2 mencoba mengambil garpu kiri
Filosof 2 berhasil mengambil garpu kiri
Filosof 0 berhasil mengambil garpu kiri
Filosof 2 mencoba mengambil garpu kiri
Filosof 2 berhasil mengambil garpu kiri
Filosof 2 mencoba mengambil garpu kiri
Filosof 2 berhasil mengambil garpu kiri
Filosof 2 berhasil mengambil garpu kiri
Filosof 1 mencoba mengambil garpu kanan
Filosof 3 mencoba mengambil garpu kanan
Filosof 4 mencoba mengambil garpu kanan
Filosof 2 mencoba mengambil garpu kanan
Filosof 0 mencoba mengambil garpu kanan
Filosof 0 mencoba mengambil garpu kanan
```
#### Analisis
```
Filosof 0 siap...
Filosof 1 siap...
Filosof 2 siap...
Filosof 3 siap...
Filosof 4 siap...
```
Semua thread sudah mencapai barrier dan sedang menunggu satu sama lain untuk mulai bersamaan

1. Semua filososf berhasil mengambil garpu kiri
   ```
   Filosof 4 mencoba mengambil garpu kiri
   Filosof 4 berhasil mengambil garpu kiri
   Filosof 3 berhasil mengambil garpu kiri
   Filosof 1 berhasil mengambil garpu kiri
   Filosof 0 berhasil mengambil garpu kiri
   Filosof 2 berhasil mengambil garpu kiri
   ```
   Kepemilikan garpu kiri:
   | Filosof | Garpu kiri yang diambil |
   | :--- | :--- |
   | 0 | garpu 0 |
   | 1 | garpu 1 |
   | 2 | garpu 2 |
   | 3 | garpu 3 |
   | 4 | garpu 4 |
   
   Semua garpu kiri sedang dipegang

3. Semua filosof mencoba mengambil garpu kanan
   ```
   Filosof 1 mencoba mengambil garpu kanan
   Filosof 3 mencoba mengambil garpu kanan
   Filosof 4 mencoba mengambil garpu kanan
   Filosof 2 mencoba mengambil garpu kanan
   Filosof 0 mencoba mengambil garpu kanan
   ```
   Tetapi garpu kanan tiap filosof sudah dipegang oleh tetangganya:
   - Filosof 0 butuh garpu 1 dipegang 1
   - Filosof 1 butuh garpu 2 dipegang 2
   - Filosof 2 butuh garpu 3 dipegang 3
   - Filosof 3 butuh garpu 4 dipegang 4
   - Filosof 4 butuh garpu 0 dipegang 0
   
   Lingkaran tunggu 5 arah terbentuk dan terjadi deadlock.
   
**Kapan Deadlock Terjadi?**

  Deadlock terjadi setelah semua filosof berhasil mengambil garpu kiri dan kemudian semua mencoba mengambil garpu       kanan, tetapi garpu kanan sudah dipegang oleh filosof sebelahnya, sahingga tidak ada satu pun filosof yang dapat      melanjutkan.

**Mengapa Deadlock Terjadi?**
  Deadlock muncul karena keempat kondisi deadlock terpenuhi sekaligus:
  | Kondisi | Penjelasan | Contoh di Program |
  | :--- | :--- | :--- |
  | Mutual Exclusion | Setiap garpu hanya bisa dipegang oleh satu filosof pada satu waktu | Setiap garpu                direpresentasikan dengan `threading.Lock()`, sehingga hanya satu thread yang dapat `acquire()` garpu tersebut |
  | Hold and Wait | Filosof sudah memegang garpu kiri dan menunggu garpu kanan | Setelah mengambil garpu kiri, muncul   output seperti: “Filosof X berhasil mengambil garpu kiri” lalu “Filosof X mencoba mengambil garpu kanan” |
  | No Preemption | Garpu tidak dapat dipaksa dilepas | Tidak ada mekanisme otomatis yang memaksa seorang filosof       melepaskan garpu kiri ketika garpu kanan tidak tersedia |
  | Circular Wait | Semua filosof membentuk rantai tunggu melingkar, di mana setiap filosof menunggu garpu kanan yang   sedang dipegang filosof lain. | Pola: 0 menunggu 1, 1 menunggu 2, 2 menunggu 3, 3 menunggu 4, dan 4 menunggu 0.       Tidak ada yang bisa bergerak = deadlock |

---

### Eksperimen 2 – Versi Fixed Menggunakan Semaphore 
![alt text](<screenshots/fixed semaphore.png>)

**Output**
```
Filosof 0 siap...
Filosof 1 siap...
Filosof 2 siap...
Filosof 3 siap...
Filosof 4 siap...
Filosof 4 berpikir...
Filosof 2 berpikir...
Filosof 1 berpikir...
Filosof 3 berpikir...
Filosof 0 berpikir...
Filosof 2 mencoba mengambil garpu kiri
Filosof 4 mencoba mengambil garpu kiri
Filosof 2 mencoba mengambil garpu kanan
Filosof 2 makan...
Filosof 4 mencoba mengambil garpu kanan
Filosof 0 mencoba mengambil garpu kiri
Filosof 4 makan...
Filosof 3 mencoba mengambil garpu kiri
Filosof 2 selesai makan

Filosof 1 mencoba mengambil garpu kiri
Filosof 0 mencoba mengambil garpu kanan
Filosof 3 mencoba mengambil garpu kanan
Filosof 4 selesai makan

Filosof 3 makan...
Filosof 1 mencoba mengambil garpu kanan
Filosof 1 makan...
Filosof 3 selesai makan

Filosof 1 selesai makan
Filosof 0 makan...

Filosof 0 selesai makan
```

**Analisis hasil modifikasi**
  Pada versi ini digunakan:
   - `footman = Senaphore(N-1)` dengan `N = 5`
   - Artinya: maksimal 4 filosof boleh masuk ke bagian "mengambil garpu" secara bersamaan
   - Tujuan: mencegah circular wait (siklus saling menunggu) yang menyebabkan deadlock

**Mengapa deadlock tidak terjadi?**
  
  Deadlock klasik pada Dining Philosophers muncul ketika semua filosof memegang garpu kiri, lalu semuanya menunggu      garpu kanan masing-masing (yang tidak pernah dilepas).

Dengan Semaphore(4):
- Hanya 4 filosof yang boleh masuk ke bagian “mengambil garpu”
- 1 filosof selalu tertahan di luar (karena semaphore penuh)

Ini otomatis mencegah siklus 5-arah, karena selalu ada setidaknya 1 garpu kiri yang bebas. Tanpa 5 garpu kiri terambil, siklus deadlock tidak mungkin terjadi.

**Urutan kejadian**
1. Semua filosofi siap dan berpikir
   Mereka menunggu barrier agar start bersamaan
2. Hanya 4 filosof pertama yang boleh masuk mengambil garpu
   ```
   Filosof 2 mencoba mengambil garpu kiri
   Filosof 4 mencoba mengambil garpu kiri
   Filosof 0 mencoba mengambil garpu kiri
   Filosof 3 mencoba mengambil garpu kiri
   ```
   Filosof ke-1 tidak bisa masuk dulu karena semaphore masih penuh (4/4)
3. Filososf 2 berhasil mengambil dua garpu dulu lalu makan
   ```
   Filosof 2 mencoba mengambil garpu kanan
   Filosof 2 makan...
   ```
4. Filosof 4 makan setelah mendapat garpu
   ```
   Filosof 4 mencoba mengambil garpu kanan
   Filosof 4 makan...
   ```
5. Filosof lain juga berhasil secara berurutan
   Saat satu filosof selesai makan dan melepaskan footman, filoasof yang tertunda dapat masuk
   Contoh:
   ```
   Filosof 2 selesai makan -> footman.release()
   ...
   Filosof 1 mencoba mengambil garpu kiri
   ```
   Setelah itu tidak pernah ada 5 orang menunggu garpu sekaligus, artinya tidak ada siklus menunggu (circular wait)
6. Semua filosof berhasil makan satu per satu

**Bukti bahwa deadlock telah dihindari.**
Untuk N = 5 filosof digunakan semaphore footman = Semaphore(4).

Aturan: setiap filosof wajib memanggil footman.acquire() sebelum mengambil garpu kiri, dan footman.release() setelah meletakkan kedua garpu.
1. Bukti Teoritis
   
   Deadlock klasik pada Dining Philosophers membutuhkan empat kondisi deadlock terjadi sekaligus:
   
   - Mutual Exclusion: garpu dipakai eksklusif
   - Hold and Wait: setiap filosof memegang 1 garpu dan menunggu 1 garpu
   - No Preemption: garpu tidak dapat dicabut paksa
   - Circular Wait: terbentuk lingkaran tunggu 0→1→2→3→4→0
  
     Versi semaphore N-1 tidak menghilangkan nomor 1-3, tetapi secara pasti memutus kondisi ke-4 (Circular Wait).

2. Pembuktian
   
   - Misalkan deadlock terjadi, artinya semua 5 filosofi sudah berhasil memanggil `footman.acquire()`, mengambil garpu kiri, lalu semuanya menunggu garpu kanan
   - Jika semua sudah mengambil garpu kiri, berarti mereka semua sudah memperoleh izin dari semaphore
   - Tetapi semaphore diset ke nilai 4, artinya:
     
     - 4 filosof yang dapat masuk ke wilayah "mengambil garpu"
     - Tidak mungkin 5 filosof melewati semaphore secara bersamaan
   - Terjadi kontradiksi: Deadlock membutuhkan semua 5 filosof masuk, tetapi mekanisme semaphore melarang lebih dari 4 masuk
   - Karena keadaan yang diperlukan deadlock secara logis mustahil, maka deadlock secara deterministik tidak dapat terjadi

---

### Eksperimen 3 – Analisis Deadlock
| Kondisi Deadlock | Terjadi di Versi Deadlock | Solusi di Versi Fixed |
| :--- | :--- | :--- |
| Mutual Exclusion | Ya (Setiap garpu hanya bisa dipegang oleh satu filosof pada satu waktu) | Tetap ada. Garpu tetap eksklusif. Semaphore tidak menghilangkan mutual exclusion |
| Hold and Wait | Ya (Filosof sudah memegang garpu kiri dan menunggu garpu kanan) | Dicegah. Semaphore (N−1) membatasi jumlah filosof yang boleh mencoba mengambil garpu, sehingga tidak semua bisa berada dalam situasi “hold” sekaligus |
| No Preemption | Ya (Garpu tidak dapat dipaksa dilepas) | Tetap ada. Garpu tetap tidak dapat dipaksa dilepas. Namun tidak menimbulkan deadlock karena circular wait dihentikan |
| Circular Wait | Ya (Semua filosof membentuk rantai tunggu melingkar, di mana setiap filosof menunggu garpu kanan yang sedang dipegang filosof lain) | Dicegah. Karena maksimal hanya N−1 filosof yang boleh mengambil garpu, tidak mungkin terbentuk rantai tunggu penuh lingkaran |

---

## Kesimpulan
- Pada percobaan pertama, seluruh filosof berhasil mengambil garpu kiri secara bersamaan dan kemudian menunggu garpu    kanan yang sedang digunakan oleh filosof lain. Hal ini menyebabkan seluruh proses terhenti dan tidak ada filosof      yang dapat melanjutkan aktivitas makan.
- Situasi deadlock terjadi karena setiap filosof memegang satu garpu sambil menunggu garpu lainnya, sehingga            terbentuk kondisi saling menunggu yang tidak dapat diselesaikan.
- Pada percobaan kedua, diterapkan mekanisme semaphore dengan nilai awal empat untuk membatasi jumlah filosof yang      dapat memasuki bagian kritis secara bersamaan. Dengan pembatasan ini, setidaknya satu filosof selalu tertahan di      luar.
- Pembatasan tersebut mencegah seluruh filosof mengambil garpu kiri secara serentak, sehingga rantai tunggu melingkar   (circular wait) yang menjadi penyebab utama deadlock tidak dapat terbentuk. Dengan demikian, seluruh filosof dapat    makan secara bergiliran tanpa terjadi kebuntuan. Penggunaan semaphore terbukti efektif dalam mencegah deadlock pada   permasalahan Dining Philosophers.

---

## Quiz
**1. Sebutkan empat kondisi utama penyebab deadlock.** 
- ⁠Mutual Exclusion: Sumber daya hanya bisa dipakai satu proses.
- Hold and Wait: Proses memegang satu sumber daya sambil menunggu yang lain.
- No Preemption: Sumber daya tidak bisa direbut paksa.
- Circular Wait: Proses saling menunggu membentuk lingkaran.
    
---
**2. Mengapa sinkronisasi diperlukan dalam sistem operasi?**

   Sinkronisasi diperlukan dalam sistem operasi karena proses atau thread yang berjalan secara bersamaan dapat saling    mengganggu ketika mengakses sumber daya atau data yang sama. Tanpa mekanisme sinkronisasi, dapat terjadi race         condition yang membuat hasil eksekusi tidak dapat diprediksi, serta menimbulkan ketidakkonsistenan data, misalnya     ketika beberapa proses melakukan pembaruan pada variabel yang sama secara bersamaan. Sinkronisasi juga memastikan     penggunaan sumber daya bersama dilakukan secara aman dan bergiliran, sehingga konflik dapat dihindari. Selain itu,    sinkronisasi membantu menjaga ketepatan eksekusi paralel pada sistem multicore dan mencegah masalah seperti           deadlock atau livelock dengan mengatur urutan dan akses proses terhadap sumber daya. Secara keseluruhan,              sinkronisasi menjadi kunci agar sistem dapat berjalan stabil, benar, dan konsisten meskipun banyak proses berjalan    secara simultan.
   
---
**3. Jelaskan perbedaan antara *semaphore* dan *monitor*.**
   | Semaphore | Monitor |
   | :--- | :--- |
   | Mekanisme sinkronasisasi tingkat rendah (low-level) | Mekanisme sinkronisasi tingkat tinggi (high_level) |
   | Menggunakan counter dan operasi ⁠ wait() ⁠ dan ⁠ sigmal() ⁠ | Menggunakan condition variable dan prosedur terin          tegrasi |
   | Programmer harus mengelola sendiri kapan kunci diambil/dilepas (rawan error) | Pengelolaan kunci dilakukan            otomatis oleh monitor (lebih aman) |
   | Dapat menyebabkan deadlock jika salah penggunaan | Mengurangi resiko deadlock karena struktur lebih terkontrol |  
   
---

## Refleksi Diri
Tuliskan secara singkat:
- Apa bagian yang paling menantang minggu ini?  
- Bagaimana cara Anda mengatasinya?  

---

**Credit:**  
_Template laporan praktikum Sistem Operasi (SO-202501) – Universitas Putra Bangsa_
