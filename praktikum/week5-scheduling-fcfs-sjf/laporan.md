
# Laporan Praktikum Minggu [5]
Topik: Penjadwalan CPU FCFS dan SJF

---

## Identitas
- **Nama**  : Keysya Ayu Anggita 
- **NIM**   : 250202944
- **Kelas** : 1IKRA

---

## Tujuan
1. Menghitung *waiting time* dan *turnaround time* untuk algoritma FCFS dan SJF.  
2. Menyajikan hasil perhitungan dalam tabel yang rapi dan mudah dibaca.  
3. Membandingkan performa FCFS dan SJF berdasarkan hasil analisis.  
4. Menjelaskan kelebihan dan kekurangan masing-masing algoritma.  
5. Menyimpulkan kapan algoritma FCFS atau SJF lebih sesuai digunakan.

---

## Dasar Teori
Algoritma First Come First Served (FCFS) merupakan metode penjadwalan CPU paling sederhana yang bekerja berdasarkan urutan kedatangan proses. Proses yang datang terlebih dahulu hingga selesai, tanpa memperhatikan lama waktu eksekusi proses tersebut. FCFS bersifat non-preemptive, artinya proses yang sedang berjalan tidak dapat dihentikan sebelum selesai. Mekanisme ini mudah diterapkan karena hanya menggunakan antrian FIFO (First In First Out). Namun, kelemahannya adalah dapat menyebabkan *convoy effect* yaitu kondisi ketika proses dengan waktu eksekusi singkat harus menunggu dengan waktu eksekusi panjang, sehingga menurunkan efisiensi sistem.

Sementara itu, algoritma Shortest Job First (SJF) memiliki proses dengan waktu eksekusi CPU (CPU burst) paling pendek untuk meminimalkan rata-rata waktu tunggu (average waiting time) seluruh proses dalam sistem. SJF dapat bersifat non-preemptive maupun preemptive (disebut Shortest Remaining Time First), dimana pada versi preemptive, proses baru dengan waktu eksekusi lebih pendek dapat menggantikan proses yang sedang berjalan. Secara teori, SJF merupakan algoritma yang paling optimal secara matematis, karena menghasilkan waktu tunggu rata-rata paling kecil dibandingkan algoritma lainnya. Namun, penerapan algoritma ini sulit dilakukan karena sistem harus dapat memperkirakan lama waktu eksekusi proses berikutnya, dan dapat menimbulkan masalah *starvation* jika proses panjang terus tertunda oleh proses-proses yang lebih pendek.

---

## Langkah Praktikum
1. **Siapkan Data Proses**
   Gunakan tabel proses berikut sebagai contoh (boleh dimodifikasi dengan data baru):
   | Proses | Burst Time | Arrival Time |
   |:--:|:--:|:--:|
   | P1 | 6 | 0 |
   | P2 | 8 | 1 |
   | P3 | 7 | 2 |
   | P4 | 3 | 3 |

2. **Eksperimen 1 – FCFS (First Come First Served)**
   - Urutkan proses berdasarkan *Arrival Time*.  
   - Hitung nilai berikut untuk tiap proses:
     ```
     Waiting Time (WT) = waktu mulai eksekusi - Arrival Time
     Turnaround Time (TAT) = WT + Burst Time
     ```
   - Hitung rata-rata Waiting Time dan Turnaround Time.  
   - Buat Gantt Chart sederhana:  
     ```
     | P1 | P2 | P3 | P4 |
     0    6    14   21   24
     ```

3. **Eksperimen 2 – SJF (Shortest Job First)**
   - Urutkan proses berdasarkan *Burst Time* terpendek (dengan memperhatikan waktu kedatangan).  
   - Lakukan perhitungan WT dan TAT seperti langkah sebelumnya.  
   - Bandingkan hasil FCFS dan SJF pada tabel berikut:

     | Algoritma | Avg Waiting Time | Avg Turnaround Time | Kelebihan | Kekurangan |
     |------------|------------------|----------------------|------------|-------------|
     | FCFS | ... | ... | Sederhana dan mudah diterapkan | Tidak efisien untuk proses panjang |
     | SJF | ... | ... | Optimal untuk job pendek | Menyebabkan *starvation* pada job panjang |

4. **Eksperimen 3 – Visualisasi Spreadsheet (Opsional)**
   - Gunakan Excel/Google Sheets untuk membuat perhitungan otomatis:
     - Kolom: Arrival, Burst, Start, Waiting, Turnaround, Finish.
     - Gunakan formula dasar penjumlahan/subtraksi.
   - Screenshot hasil perhitungan dan simpan di:
     ```
     praktikum/week5-scheduling-fcfs-sjf/screenshots/
     ```

5. **Analisis**
   - Bandingkan hasil rata-rata WT dan TAT antara FCFS & SJF.  
   - Jelaskan kondisi kapan SJF lebih unggul dari FCFS dan sebaliknya.  
   - Tambahkan kesimpulan singkat di akhir laporan.

6. **Commit & Push**
   ```bash
   git add .
   git commit -m "Minggu 5 - CPU Scheduling FCFS & SJF"
   git push origin main
   ```

---

## Kode / Perintah

```bash
Waiting Time (WT) = waktu mulai eksekusi - Arrival Time
Turnaround Time (TAT) = WT + Burst Time

Average Waiting Time (WT) = Total WT / Jumlah Proses
Average Turnaround Time (TAT) = Total TAT / Jumlah Proses
```

---

## Hasil Eksekusi
Sertakan screenshot hasil percobaan atau diagram:
![alt text](<screenshots/fcfs-sjf.png>)

### Eksperimen 1 - FCFS (First Come First Served)
Proses diurutkan berdasarkan waktu kedatangan (*Arrival Time*), yaitu P1 (0), P2 (1), P3 (2), dan P4(3), sehingga urutan eksekusinya adalah  P1 → P2 → P3 → P4.

Berdasarkan hasil perhitungan algoritma **First Come First Served (FCFS)**, diperoleh total waktu tunggu (*Waiting Time*) sebesar **35** dengan rata-rata waktu tunggu sebesar **8,75**. Sementara itu, total waktu penyelesaian (*Turnaround Time*) adalah **59** dengan rata-rata waktu penyelesaian sebesar **14,75**. Nilai tersebut menunjukkan bahwa pada algoritma FCFS, proses yang datang lebih awal akan dilayani terlebih dahulu tanpa memperhatikan lama waktu eksekusi, sehingga waktu tunggu rata-rata cenderung lebih tinggi terutama ketika terdapat proses dengan durasi eksekusi yang panjang.

 | Algoritma | Avg Waiting Time | Avg Turnaround Time | Kelebihan | Kekurangan |
 |------------|------------------|----------------------|------------|-------------|
 | FCFS | 8.75 | 14.75 | Sederhana dan mudah diterapkan | Tidak efisien untuk proses panjang |
 | SJF | 6.25 | 12.25 | Optimal untuk job pendek | Menyebabkan *starvation* pada job panjang |
 
---
### Eksperimen 2 -  SJF (Shortest Job First)
Pada Algoritma SJF, proses diurutkan berdasarkan waktu *Burst Time* dari yang paling pendek hingga yang paling panjang. Dengan demikian, proses yang memiliki waktu eksekusi paling singkat akan dijalankan terlebih dahulu sebelum proses lainnya.
			
| Proses |	Arrival Time |	Burst Time |	Start Time |	Finish Time |	Waiting Time | Turnaround Time |
| :---|:---|:---|:---|:---|:---|:---|
| P1| 0 |	6 |	0 |	6 |	0 |	6 |
| P2 | 3 | 3 | 6 | 9 | 3 | 6 |
| P3 |	2 |	7	| 9 |	16 | 7 | 14 |
| P4 |	1 |	8	| 16 | 24 |	15 | 23 |
| Total |||||					25 |	49 |
| Average	|||||				6.25 |	12.25 |

---
### Eksperimen 3 – Visualisasi Spreadsheet (Opsional)
  Perbandingan waktu FCFS dan SJF :
 | Algoritma | Avg Waiting Time | Avg Turnaround Time | Kelebihan | Kekurangan |
 |------------|------------------|----------------------|------------|-------------|
 | FCFS | 8.75 | 14.75 | Sederhana dan mudah diterapkan | Tidak efisien untuk proses panjang |
 | SJF | 6.25 | 12.25 | Optimal untuk job pendek | Menyebabkan *starvation* pada job panjang |

---
### Kondisi kapan SJF lebih unggul dari FCFS dan sebaliknya.

**Shortest Job First (SJF)** akan lebih unggul dari **First Come First Served (FCFS)** dalam hal efisiensi waktu karena dirancang untuk meminimalkan rata-rata *Waiting Time* dan *Turnaround Time*. Keunggulan SJF terutama terlihat ketika terdapat campuran antara proses pendek dan panjang, karena SJF memilih proses terpendek dahulu, secara efektif menghindari *convoy effect* di mana proses singkat harus menunggu lama di belakang proses yang sangat panjang. Sebaliknya, FCFS menjadi unggul dalam hal kesederhanaan dan keadilan. FCFS sangat mudah diimplementasikan dan memiliki *overhead* penjadwalan yang minimal. FCFS menjamin bahwa setiap proses akan selesai karena dieksekusi berdasarkan urutan kedatangan, sehingga tidak memiliki risiko *starvation*, sebuah kelemahan  yang melekat pada SJF. Selain itu, FCFS tidak perlu memperkirakan waktu eksekusi proses terlebih dahulu, sehingga lebih mudah dan praktis digunakan dalam sistem operasi nyata.

---

## Analisis
Berikut ini hasil pehitungan *waiting time* dan *turnaround time* dari dua skenario menggunakan algoritma FCFS dan SJF. Pada setiap skenario, diperoleh hasil perbandingan waktu tunggu dan waktu penyelesaian proses sehingga dapat dilihat perbedaan efisien antara kedua algoritma tersebut.

### Skenario 1 - FCFS (First Come First Served)							
| Proses |	Burst Time |	Arrival Time |	Start Time	| Finish Time |	Waiting Time |	Turnaround Time |
| :---|:---|:---|:---|:---|:---|:---|
| P1 |	8 |	0 |	0 |	8 |	0 |	8 |	
| P2 | 6 | 1 | 8 | 14 |	7 |	13 |	
| P3 | 7 | 2 | 14 |	21 | 12 |	19 |	
| P4 | 5 | 3 | 21 |	26 | 18 |	23 |	
| Total |||||					37 |	63	|
| Average	|||||				9.25 | 15.75 |


### Skenario 1 - SJF (Shortest Job First)						
| Proses |	Arrival Time |	Burst Time |	Start Time |	Finish Time | 	Waiting Time |	Turnaround Time |
| :---|:---|:---|:---|:---|:---|:---|
| P1 |	0 |	8	| 0	| 8	| 0	| 8 |
| P2 | 3 | 5 | 8 | 13 |	5 |	10 |
| P3 | 2 | 7 | 13 |	20 | 11	| | 18 |
| P4 |	1 |	6	| 20 |	26 | 19	| 25 |
| Total |||||			    	35 |	61 |
| Average	|||||	        8.75 |	15.25 |


### Skenario 2 - FCFS (First Come First Served)							
| Proses |	Arrival Time |	Burst Time |	Start Time |	Finish Time | 	Waiting Time |	Turnaround Time |
| :---|:---|:---|:---|:---|:---|:---|
| P1	| 6	| 0	| 0	| 6	| 0	| 6 |	
| P2	| 9	| 1	| 6	| 15 |	5	| 14 |	
| P3	| 3	| 2	| 15	| 18	| 13	| 16	|
| P4	| 7 |	3	| 18	| 25 | 15	| 22	|
| Total			|||||		           	33	| 58	|
| Average			|||||		        8.25	| 14.5	|

### Skenario 2 - SJF (Shortest Job First)						
| Proses |	Arrival Time |	Burst Time |	Start Time |	Finish Time | 	Waiting Time |	Turnaround Time |
| :---|:---|:---|:---|:---|:---|:---|
| P1	| 0	| 6	| 0	| 6	| 0	| 6 | 
| P2	| 3	| 7	| 6	| 13 | 3 |	10 |
| P3	| 2	| 3	| 13 | 16	| 11 |	14 |
| P4	| 1	| 9	| 16 |	25 | 15	| 24 |
| Total 		|||||				29	| 54 |
| Average 	|||||					7.25 | 13.5 |

---

### Kelebihan dan kelemahan tiap algoritma

Berdasarkan hasil percobaan, algoritma FCFS (First Come First Served) memiliki kelebihan yaitu mudah diterapkan karena proses dijalankan sesuai urutan kedatangan tanpa perhitungan yang rumit. Algoritma ini juga bersifat adil terhadap urutan waktu kedatangan proses, sehingga cocok digunakan pada sistem batch atau antrian sederhana. Namun, FCFS memiliki kelemahan yaitu kurang efisien ketika terdapat proses dengan *burst time* yang panjang, karena proses lain harus menunggu hingga proses tersebut selesai (*convoy effect*). Hal ini menyebabkan rata-rata waktu tunggu menjadi tinggi dan membuat algoritma ini kurang sesuai untuk sistem interaktif atau real-time yang membutuhkan respon cepat.

Sementara itu, algoritma SJF (Shortest Job First) memiliki kelebihan karena mampu menghasilkan rata-rata waktu tunggu (*waiting time*) dan waktu penyelesaian (*turnaround time*) yang lebih kecil dibandingkan FCFS. Dengan mengeksekusi proses yang memiliki *burst time* paling pendek terlebih dahulu, SJF dapat meningkatkan efisiensi dan *throughput* sistem. Meskipun demikian, algoritma ini juga memiliki kelemahan, yaitu sulit diterapkan di dunia nyata karena waktu burst setiap proses tidak selalu diketahui sebelumnya. Selain itu, proses dengan waktu eksekusi panjang dapat tertunda terus-menerus apabila proses pendek terus berdatangan, sehingga menimbulkan masalah *starvation*.
  
---

## Kesimpulan
- Algoritma FCFS menjalankan proses berdasarkan urutan kedatangan, sehingga mudah diterapkan dan adil terhadap semua    proses. Dan kekurangan FCFS adalah waktu tunggu bisa menjadi lama jika proses pertama memiliki *burst time* besar     (*convoy effect*). 
- Algoritma SJF lebih efisien karena menjalankan proses dengan waktu eksekusi paling pendek terlebih dahulu.
- Hasil praktikum menunjukkan bahwa SJF menghasilkan rata-rata waktu tunggu dan *turnaround time* yang lebih kecil      dibanding FCFS.
- SJF lebih optimal dalam efisiensi waktu, sedangkan FCFS lebih mudah diterapkan dalam sistem sederhana.

---

## Quiz
**1. Apa perbedaan utama antara FCFS dan SJF?**
   
   FCFS (First Come First Served) mengeksekusi proses berdasarkan urutan kedatangan dan bersifat non-preemptive,         namun   dapat menimbulkan *convoy effect* karena proses pendek menunggu proses panjang. Sedangkan SJF (Shortest       Job First)    memiliki proses dengan waktu eksekusi terpendek untuk dijalankan lebih dulu sehingga lebih efisien      dan menghasilkan   waktu tunggu rata-rata paling kecil, tetapi sulit diterapkan karena memerlukan perkiraan lama      waktu eksekusi secara   akurat.

---
**2. Mengapa SJF dapat menghasilkan rata-rata waktu tunggu minimum?**

  Algoritma **Shortest Job First (SJF)** menghasilkan rata-rata waktu tunggu yang paling kecil karena proses            dengan waktu eksekusi (*CPU burst*) paling pendek dijalankan terlebih dahulu. Ketika proses-proses singkat            dikerjakan lebih awal, waktu tunggu total sistem menjadi lebih efisien. Pengurangan waktu tunggu pada proses          singkat lebih besar dibandingkan peningkatan waktu tunggu pada proses panjang. Oleh karena itu, urutan eksekusi       berdasarkan durasi *burst time* yang paling pendek membuat rata-rata waktu tunggu seluruh proses menjadi minimum.

---
**3. Apa kelemahan SJF jika diterapkan pada sistem interaktif?**

  Salah satu kelemahan dari algoritma **Shortest Job First (SJF)** saat digunakan di sistem interaktif adalah sulit     untuk menentukan berapa lama proses akan berjalan. Dalam sistem seperti ini, pengguna bisa menjalankan berbagai       aktivitas dengan durasi yang tidak bisa diprediksi dan bisa berubah sewaktu-waktu, jadi perkiraan waktu eksekusi      (CPU burst) sering tidak tepat. Selain itu, SJF juga bisa membuat proses yang butuh waktu lebih lama tertunda terus   karena selalu didahului oleh proses yang lebih singkat. Hal tersebut membuat sistem terasa kurang adil dan bisa       menurunkan kinerja sistem. 

---

## Refleksi Diri
Tuliskan secara singkat:
- Apa bagian yang paling menantang minggu ini?
  Saya merasa bingung dalam menentukan *Start Time* dan *Finish Time* pada setiap proses, karena harus memperhatikan    urutan kedatangan dan waktu eksekusi proses sebelumnya. Setelah dicoba beberapa kali, saya memahami pola              perhitungannya dan bisa menentukan waktu eksekusi dengan benar.
- Bagaimana cara Anda mengatasinya?
  Untuk mengatasi kebingungan tersebut saya mulai mengurutkan proses berdasarkan *Arrival Time*, lalu menghitung        waktu mulai setiap proses berdasarkan waktu selesai proses sebelumnya. Selain itu, saya juga mencari referensi        tambahan dan contoh penyelesaian algoritma FCFS dari internet untuk memperdalam pemahaman tentang alur perhitungan    *Start Time* dan *Finish Time*.

---

**Credit:**  
_Template laporan praktikum Sistem Operasi (SO-202501) – Universitas Putra Bangsa_
