
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
![alt text](<screenshots/week4-proses-user1.png>)
![alt text](<screenshots/week4-proses-user2.png>)
![alt text](<screenshots/week4-proses-user3.png>)

---

## Analisis
- Jelaskan makna hasil percobaan.  
  

---

## Kesimpulan
Tuliskan 2–3 poin kesimpulan dari praktikum ini.

---

## Tugas & Quiz
### Tugas
---
- Dokumentasikan hasil semua perintah dan jelaskan fungsi tiap perintah.
- Gambarkan hierarki proses dalam bentuk diagram pohon (`pstree`) di laporan.
- Jelaskan hubungan antara user management dan keamanan sistem Linux
  
### Quiz
---
1. Apa fungsi dari proses `init` atau `systemd` dalam sistem Linux?
   - Merupakan proses pertama yang dijalankan oleh kernel setelah proses booting selesai.
   - 
2. Apa perbedaan antara `kill` dan `killall`?
  - `kill` menerima nomor ID proses sebagai argumen dan hanya mematikan satu proses pada satu waktu, kecuali jika beberapa ID proses ditentukan sekaligus dalam satu perintah.
  - `killall` memungkinkan penghentian proses berdasarkan nama program (name)ndan akan mengakhiri semua proses yang memiliki nama yang sama.
   
4. Mengapa user `root` memiliki hak istimewa di sistem Linux?
   Dalam sistem operasi Linux, user root atau disebut juga superuser adalah pengguna dengan hak akses tertinggi yang memiliki kendali penuh terhadap seluruh sumber daya sistem. Sistem operasi 

---

## Refleksi Diri
Tuliskan secara singkat:
- Apa bagian yang paling menantang minggu ini?  
- Bagaimana cara Anda mengatasinya?  

---

**Credit:**  
_Template laporan praktikum Sistem Operasi (SO-202501) – Universitas Putra Bangsa_
