
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
     ```
     WT[i] = waktu mulai eksekusi - Arrival[i]
     TAT[i] = WT[i] + Burst[i]
     ```

---

## Hasil Eksekusi
Sertakan screenshot hasil percobaan atau diagram:
![Screenshot hasil](screenshots/example.png)

---

## Analisis
- Jelaskan makna hasil percobaan.  
- Hubungkan hasil dengan teori (fungsi kernel, system call, arsitektur OS).  
- Apa perbedaan hasil di lingkungan OS berbeda (Linux vs Windows)?  

---

## Kesimpulan
Tuliskan 2–3 poin kesimpulan dari praktikum ini.

---
## Tugas
1. Hitung *waiting time* dan *turnaround time* untuk algoritma RR dan Priority.  
2. Sajikan hasil perhitungan dan Gantt Chart dalam `laporan.md`.  
3. Bandingkan performa dan jelaskan pengaruh *time quantum* serta prioritas.  
4. Simpan semua bukti (tabel, grafik, atau gambar) ke folder `screenshots/`.
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
- Bagaimana cara Anda mengatasinya?  

---

**Credit:**  
_Template laporan praktikum Sistem Operasi (SO-202501) – Universitas Putra Bangsa_
