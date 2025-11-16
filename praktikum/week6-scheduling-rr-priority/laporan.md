
# Laporan Praktikum Minggu [6]
Topik: Penjadwalan CPU – Round Robin (RR) dan Priority Scheduling

---

## Identitas
- **Nama**  : Keysya Ayu Anggita  
- **NIM**   : 250202944  
- **Kelas** : 1IKRA

---

## Tujuan
1. Menghitung *waiting time* dan *turnaround time* pada algoritma RR dan Priority.  
2. Menyusun tabel hasil perhitungan dengan benar dan sistematis.  
3. Membandingkan performa algoritma RR dan Priority.  
4. Menjelaskan pengaruh *time quantum* dan prioritas terhadap keadilan eksekusi proses.  
5. Menarik kesimpulan mengenai efisiensi dan keadilan kedua algoritma.

---

## Dasar Teori
Dalam sistem operasi terdapat berbagai algoritma yang digunakan untuk mengatur urutan eksekusi proses agar CPU dapat bekerja secara efisien. Dua diantaranya adalah **Round Robin (RR) dan Priority Scheduling**. Kedua algoritma ini memiliki tujuan yang sama, yaitu mengoptimalkan penggunaan CPU serta meningkatkan kinerja sistem, tetapi cara kerjanya berbeda. **Round Robin (RR)** membagi waktu eksekusi secara adil antar proses menggunakan sistem waktu bergilir, sedangkan **Priority Scheduling** menentukan urutan eksekusi berdasarkan tingkat kepentingan atau prioritas dari setiap proses.
* **Round Robin (RR)**: Algoritma ini merupakan pengembangan dari FCFS yang bersifat preemptive. Setiap proses mendapatkan jatah waktu tertentu (*time quantum*) untuk dieksekusi. Jika waktu habis dan proses belum selesai, CPU akan dialihkan ke proses berikutnya, dan proses yang belum selesai dikembalikan ke antrian. RR adil untuk semua proses dan cocok untuk sistem time-sharing, namun performanya tergantung pada besar kecilnya time quantum.
* **Priority Scheduling**: Setiap proses memiliki nilai prioritas, dan CPU diberikan kepada proses dengan prioritas tertinggi. Dapat bersifat preemptive maupun non-preemptive. Algoritma ini efisien untuk menangani proses penting, tetapi dapat menyebabkan *starvation* pada proses berprioritas rendah. Masalah ini dapat diatasi dengan **teknik aging**, yaitu menaikkan prioritas proses yang menunggu terlalu lama.

---

## Langkah Praktikum
1. **Siapkan Data Proses**
   Gunakan contoh data berikut (boleh dimodifikasi sesuai kebutuhan):
   | Proses | Burst Time | Arrival Time | Priority |
   |:--:|:--:|:--:|:--:|
   | P1 | 5 | 0 | 2 |
   | P2 | 3 | 1 | 1 |
   | P3 | 8 | 2 | 4 |
   | P4 | 6 | 3 | 3 |

2. **Eksperimen 1 – Round Robin (RR)**
   - Gunakan *time quantum (q)* = 3.  
   - Hitung *waiting time* dan *turnaround time* untuk tiap proses.  
   - Simulasikan eksekusi menggunakan Gantt Chart (manual atau spreadsheet).  
     ```
     | P1 | P2 | P3 | P4 | P1 | P3 | ...
     0    3    6    9   12   15   18  ...
     ```
   - Catat sisa *burst time* tiap putaran.

3. **Eksperimen 2 – Priority Scheduling (Non-Preemptive)**
   - Urutkan proses berdasarkan nilai prioritas (angka kecil = prioritas tinggi).  
   - Lakukan perhitungan manual untuk:
     ```
     WT[i] = waktu mulai eksekusi - Arrival[i]
     TAT[i] = WT[i] + Burst[i]
     ```
   - Buat tabel perbandingan hasil RR dan Priority.

4. **Eksperimen 3 – Analisis Variasi Time Quantum (Opsional)**
   - Ubah *quantum* menjadi 2 dan 5.  
   - Amati perubahan nilai rata-rata *waiting time* dan *turnaround time*.  
   - Buat tabel perbandingan efek *quantum*.

5. **Eksperimen 4 – Dokumentasi**
   - Simpan semua hasil tabel dan screenshot ke:
     ```
     praktikum/week6-scheduling-rr-priority/screenshots/
     ```
   - Buat tabel perbandingan seperti berikut:

     | Algoritma | Avg Waiting Time | Avg Turnaround Time | Kelebihan | Kekurangan |
     |------------|------------------|----------------------|------------|-------------|
     | RR | ... | ... | Adil terhadap semua proses | Tidak efisien jika quantum tidak tepat |
     | Priority | ... | ... | Efisien untuk proses penting | Potensi *starvation* pada prioritas rendah |

6. **Commit & Push**
   ```bash
   git add .
   git commit -m "Minggu 6 - CPU Scheduling RR & Priority"
   git push origin main
   ```

---

## Kode / Perintah
Tuliskan potongan kode atau perintah utama:

     WT[i] = waktu mulai eksekusi - Arrival[i]
     TAT[i] = WT[i] + Burst[i]
     Average Waiting Time (WT) = Total WT / Jumlah Proses
     Average Turnaround Time (TAT) = Total TAT / Jumlah Proses

---

## Hasil Eksekusi
![alt text](<screenshots/rr-priorityweek6.png>)

---
### Eksperimen 1 - Round Robin (RR)
Berikut hasil perhitungan *waiting time* dan *turnaround time* dengan *time quantum (q)* 3:
							
|Proses|	Burst Time|	Arrival Time|	Finish Time (P1)|	Finish Time (P2)|	Finish Time (P3)|	WT|	TAT|
|:---|:---|:---|:---|:---|:---|:---|:---|
| P1 |	5 |	0 |	3 (sisa 2) | 14 (sisa 2) |	- | 14-5= 9 |	14-0= 14 |
| P2 |	3 |	1 |	6 (selesai) | - |	- | 5-3= 2	| 6-1= 5 |
| P3 |	8 |	2 |	9 (sisa 5) | 17 (sisa 2) |	22| 20-8= 12|	22-2= 20 |
| P4 |	6 |	3 |  12 (sisa 3) | 20 (selesai) | - | 17-6= 11 | 20-3= 17 |
| Total    |     |     |    |   ||34 | 56 |
| Average  |	  |     |    |   ||8.5|	14 |

Simulasikan eksekusi menggunakan `Gantt Chart`:
```
    | P1 | P2 | P3 | P4 | P1 | P3 | P4 | P3 |
    0    3    6    9   12   14   17   20   22
```
---
### Eksperimen 2 - Priority Scheduling (Non-Preemptive)
Proses telah diurutkan berdasarkan nilai prioritas (angka kecil = prioritas tinggi) sehingga urutan eksekusi menjadi P1 → P2 → P4 → P3. Berikut adalah hasil perhitungan nilai *Waiting Time (WT)* dan *Turnaround Time (TAT)*:

| Proses |	Arrival Time | Burst Time	| Start Time |	Priority |	WT= Start-AT | TAT= WT+BT |
|:---|:---|:---|:---|:---|:---|:---|
| P1 | 0 | 5 | 0 | 2 | 0 | 0+5= 5 |
| P2 | 1 | 3 | 5 | 1 | 5-1= 4 | 4+3= 7 |
| P3 | 3 | 6 | 8 | 3 | 8-3= 5 | 5+6= 11 | 
| P4 | 2 | 8 | 14| 4 | 14-2= 12 | 12+8= 20 |
| Total || | | | 21 | 43 |
| Average || | || 5.25 | 10.75 |

---
### Eksperimen 3 - Variasi Time Quantum 
Berikut merupakan hasil perhitungan *waiting time* dan *turnaround time* untuk masing-masing variasi *time quantum* 2 dan 5:

![alt text](<screenshots/rr-quantumweek6.png>)

**Time Quantum (q): 2**

![alt text](<screenshots/quantum2-week6.png>)

**Time Quantum (q) : 5**

![alt text](<screenshots/quantum5-week6.png>)

- `Gantt Chart` akan menghasikan sebagai berikut:
  
  **Time Quantum (q): 2**
  ```
     | P1 | P2 | P3 | P4 | P1 | P2 | P3 | P4 | P1 | P3 | P4 | P3 |
     0    2    4    6    8   10    11   13   15   16   18   20   22
  ```
  **Time Quantum (q): 5**
  ```
     | P1 | P2 | P3 | P4 | P3 | P4 |
     0    5    8   13   18   21   22
  ```
**Perbandingan Efek Quantum**
| Time Quantum | Avg WT | Avg TAT | Efek / Analisis |
|:---|:---|:---|:---|
| Q= 2 | 10.25 | 15.75 | *Waiting time* dan *Turnaround time* menjadi lebih lama karena quantum yang kecil membuat proses sering dipotong dan bergantian, sehingga antrian semakin panjang dan penyelesaiannya ikut tertunda.
| Q= 5 | 7 | 12.5 | *Waiting time* dan *Turnaround time* menjadi lebih cepat karena quantum yang lebih besar membuat proses tidak sering dipotong, sehingga proses dapat berjalan  lebih lama, antrian maju lebih cepat dan waktu penyelesaian menjadi lebih singkat. |

---
### Eksperimen 4 - Perbandingan Round Robin dan Priority Scheduling
| Algoritma | Avg Waiting Time | Avg Turnaround Time | Kelebihan | Kekurangan |
|------------|------------------|----------------------|------------|-------------|
| RR | 8.5 | 14 | Adil terhadap semua proses | Tidak efisien jika quantum tidak tepat |
| Priority | 5.25 | 10.75 | Efisien untuk proses penting | Potensi *starvation* pada prioritas rendah |

---
## Analisis

Berdasarkan hasil eksperimen, Priority Scheduling menghasilkan rata-rata *waiting time* dan *turnaround time* yang lebih rendah karena proses berprioritas tinggi langsung dijalankan. Sebaliknya, pada Round Robin proses harus menunggu beberapa giliran sesuai time quantum, sehingga waktu tunggu dan waktu eksekusi menjadi lebih lama. Pada RR dengan quantum 2, performanya paling buruk karena waktu tunggu dan waktu selesai menjadi paling lama (Avg WT = 10.25, Avg TAT = 15.75) akibat proses terlalu sering dipotong. Sementara itu, RR dengan quantum 5 menunjukkan performa lebih baik (Avg WT = 7, Avg TAT = 12.5) karena proses mendapat jatah waktu lebih panjang dan tidak terlalu sering berganti.

Pada Priority Scheduling, urutan eksekusi ditentukan oleh tingkat prioritas sehingga proses dengan prioritas tertinggi dijalankan terlebih dahulu. Cara kerja ini membuat waktu tunggu dan waktu selesai lebih rendah bagi proses berprioritas tinggi, sementara proses berprioritas rendah bisa menunggu lebih lama. Perbedaan cara eksekusi inilah yang menyebabkan performanya berbeda, dengan Round Robin cenderung menghasilkan waktu tunggu dan waktu selesai lebih besar dibandingkan Priority Scheduling.

---

## Kesimpulan
- Priority Scheduling menghasilkan *waiting time* dan *turnaround time* yang lebih rendah karena proses berprioritas    tinggi langsung dieksekusi.
- Round Robin menghasilkan waktu tunggu dan waktu selesai yang lebih besar karena proses harus menunggu giliran         sesuai time quantum.
- Semakin besar time quantum, semakin cepat proses selesai pada RR, tetapi jika quantum terlalu besar, sifat RR         mendekati FCFS.
- Priority Scheduling berpotensi menyebabkan starvation, terutama pada proses berprioritas rendah, karena tidak         mendapatkan kesempatan eksekusi jika terus ada proses dengan prioritas lebih tinggi.

---
## Quiz

**1. Apa perbedaan utama antara Round Robin dan Priority Scheduling?**
    
   Round Robin berfokus pada **pembagian waktu yang adil (fairness)** antar proses dan lebih sesuai untuk sistem         time-sharing yang membutuhkan respons cepat, sedangkan Priority SCheduling berfokus pada **tingkat kepentingan        proses (importance)** dan lebih efektif digunakan pada sistem yang menuntut penanganan cepat terhadap proses          penting.

---
**2. Apa pengaruh besar/kecilnya *time quantum* terhadap performa sistem?**
   
   Jika time quantum terlalu kecil, maka akan terjadi terlalu banyak context switch, CPU akan sering berpindah antar     proses, menyebabkan overhead meningkat dan efisiensi sistem menurun, karena lebih banyak waktu yang dihabiskan        untuk perpindahan konteks daripada eksekusi proses itu sendiri. Sebaliknya, jika time quantum terlalu besar, maka     algoritma Round Robin akan berperilaku seperti FCFS, dimana proses dengan waktu eksekusi panjang akan mendominasi     CPU dan mengurangi kemampuan sistem dalam memberikan respons cepat terhadap proses lain, terutama pada sistem         time-sharing.

---    
**3. Mengapa algoritma Priority dapat menyebabkan *starvation*?**
   
   Algoritma Priority memberikan CPU kepada proses dengan prioritas tertinggi terlebih dahulu. Ketika proses baru        dengan prioritas lebih tinggi terus datang ke ready queue, proses dengan prioritas lebih rendah akan terus            tertunda karena selalu didahului oleh proses lain yang lebih penting. Akibatnya, proses berprioritas rendah tidak     mendapatkan kesempatan untuk dieksekusi dan harus menunggu dalam waktu yang sangat lama. Kondisi inilah yang          menyebabkan sistem tidak seimbang dalam pembagian waktu eksekusi antar proses dan pada akhirnya menimbulkan           *starvation*, yaitu keadaan dimana proses prioritas rendah tidak pernah dijalankan karena selalu kalah oleh proses
   dengan prioritas lebih tinggi.
   
---

## Refleksi Diri
Tuliskan secara singkat:
- Apa bagian yang paling menantang minggu ini?
  Yang menantang pada minggu ini adalah memahami algoritma Round Robin dan cara kerja time quantum, serta membedakan    cara kerja Round Robin dengan Priority Scheduling.

- Bagaimana cara Anda mengatasinya?
  Untuk mengatasinya, saya menanyakan kepada teman yang memahami dalam perhitungan Round Robin dan mencari referensi    tambahan dari internet, serta mencoba memahami ulang dalam perhitungan tersebut. 

---

**Credit:**  
_Template laporan praktikum Sistem Operasi (SO-202501) – Universitas Putra Bangsa_
