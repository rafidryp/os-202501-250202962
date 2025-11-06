
# Laporan Praktikum Minggu [5]
Topik:  algoritma penjadwalan CPU (CPU Scheduling)

---

## Identitas
- **Nama**  : Rafid Raihan Yuda Permana
- **NIM**   : 250202962
- **Kelas** : 1IKRB

---

## Tujuan

> Mahasiswa akan melakukan simulasi dan perbandingan hasil perhitungan kedua algoritma ini menggunakan tabel observasi manual atau spreadsheet (Excel/Google Sheets) — tanpa perlu melakukan instalasi atau pemrograman tambahan.

---

## Dasar Teori
Tuliskan ringkasan teori (3–5 poin) yang mendasari percobaan.

---

## Langkah Praktikum
1. Menyiapkan tabel proses  
2. 1. Mengurutkan dan menghitung nilai proses berdasarkan Arrival Time
   2. Menghitung rata-rata Waiting Time dan Turnaround Time dan membuat Gantt Chart     sederhana
   3. Mengurutkan sekaligus melakukan penghitungan WT TAT seperti langkah sebelumnya dan membandingkan hasil FCFS dan SJF
3. File
   1.  Arrival, Burst, Start, Waiting, Turnaround, Finish.
   2. Gunakan formula dasar penjumlahan/substraksi

   Kode Perintah
Waiting Time (WT) = waktu mulai eksekusi - Arrival Time
Turnaround Time (TAT) = WT + Burst Time

| P1 | P2 | P3 | P4 |
0    6    14   21   24

4. git add .
   git commit -m "Minggu 5 - CPU Scheduling FCFS & SJF"
   git push origin main

---

## Kode / Perintah
Tuliskan potongan kode atau perintah utama:
```bash

Waiting Time (WT) = waktu mulai eksekusi - Arrival Time
Turnaround Time (TAT) = WT + Burst Time

```

---

## Hasil Eksekusi
Sertakan screenshot hasil percobaan atau diagram:
![Screenshot hasil](./screenshots/Gantt%20Chart.png)

---

## Analisis
A. Jelaskan makna hasil percobaan.  

Makna Hasil Percobaan Simulasi Penjadwalan CPU
Ketika kamu menjalankan simulasi (misalnya FCFS atau SJF), kamu akan mendapatkan:
- 	Urutan eksekusi proses (Gantt Chart)
- 	Waktu tunggu (Waiting Time)
- 	Waktu penyelesaian (Turnaround Time)

Makna dari hasil ini:

- 	Menunjukkan efisiensi dan responsivitas sistem terhadap proses yang datang.
- 	Menggambarkan keadilan atau prioritas yang diberikan ke proses tertentu.
- 	Memberi wawasan tentang trade-off antara throughput, latency, dan fairness.

B. Hubungkan hasil dengan teori (fungsi kernel, system call, arsitektur OS). 

1. Fungsi Kernel
- Kernel bertanggung jawab atas penjadwalan proses, manajemen memori, dan interupsi.
- Algoritma penjadwalan (FCFS, SJF, dll.) diimplementasikan dalam scheduler yang merupakan bagian dari kernel.

2. System Call
- Proses berinteraksi dengan kernel melalui system call, seperti:
- fork() untuk membuat proses baru
- exec() untuk menjalankan program
- wait() untuk menunggu proses selesai
- System call memungkinkan proses meminta layanan dari kernel, termasuk penjadwalan.

3. Arsitektur OS
• 	OS modern seperti Linux dan Windows memiliki multitasking, preemptive scheduling, dan prioritas proses.
• 	Arsitektur menentukan bagaimana scheduler bekerja:
• 	Linux menggunakan Completely Fair Scheduler (CFS).
• 	Windows menggunakan Multilevel Feedback Queue (MLFQ).

C. Apa perbedaan hasil di lingkungan OS berbeda (Linux vs Windows)?  

Linux

  hasil simulasi penjadwalan CPU cenderung menunjukkan pola yang lebih adil dan stabil karena Linux menggunakan algoritma "Completely Fair Scheduler" atau "CFS". "CFS" berusaha membagi waktu CPU secara merata di antara proses, sehingga proses dengan burst time pendek maupun panjang tetap mendapat giliran. Dalam simulasi seperti "SJF" atau "FCFS", Linux bisa lebih konsisten dalam mengeksekusi proses sesuai urutan atau durasi karena kernel-nya dirancang untuk efisiensi dan kestabilan, terutama dalam lingkungan server atau multitasking berat.

Windows

  Sebaliknya di windowshasil simulasi bisa menunjukkan perbedaan karena Windows menggunakan pendekatan "Multilevel Feedback Queue" atau "MLFQ". Algoritma ini lebih agresif dan adaptif terhadap proses interaktif. Proses yang sering melakukan I/O atau berperilaku ringan akan diprioritaskan, sementara proses berat bisa diturunkan ke prioritas lebih rendah. Akibatnya, dalam simulasi "SJF" atau "FCFS", urutan eksekusi bisa berubah tergantung pada bagaimana Windows menilai prioritas dan responsivitas proses. Ini membuat Windows lebih cocok untuk aplikasi desktop yang butuh respons cepat, tapi bisa menghasilkan hasil simulasi yang tampak "tidak konsisten" jika dibandingkan dengan Linux.





---

## Kesimpulan
- SJF (Shortest Job First) rata-rata waiting time nya dan juga Waktu Penyelesaiannya (Turnaround Time) rata-rata lebih rendah dibandingkan FCFS (First Come First Served).

-FCFS lebih sederhana tetapi tidak efisien untuk proses dengan burst time panjang. Sedangkan SJF akan mengeksekusi proses-proses kecil terlebih dahulu, sehingga waktu tunggu rata-rata menjadi sangat rendah.
- FCFS cocok digunakan untuk sistem yang tidak memerlukan efisiensi tinggi dan prosesnya sederhana, sedangkan SJF lebih cocok untuk sistem proses dengan burst pendek yang dapat di prediksi.

---

## Quiz
1. Apa perbedaan utama antara FCFS dan SJF?

   **Jawaban:**  

   Sangat efisien dalam meminimalkan waktu tunggu rata-rata

- Prinsip penjadwalan : Proses dijalankan sesuai urutan kedatangan => Proses dengan waktu eksekusi (burst time) paling pendek dijalankan lebih dulu

Sifat Algoritma : Non-preemptive => Bisa non-preemptive (SRTF)

- Keadilan (Fairness) = Lebih adil secara waktu kedatangan =>  Tidak adil bagi proses panjang atau lambat

- Efisiensi Waktu Tunggu : Kurang efisien jika proses panjang datang lebih dahulu => Sangat efisien dalam meminimalkan waktu tunggu rata-rata

- Implementasi : Mudah dan Sederhana => Butuh estimasi waktu eksekusi tiap proses

2. Mengapa SJF dapat menghasilkan rata-rata waktu tunggu minimum?

   **Jawaban:**  

   Mengapa SJF Menghasilkan Waktu Tunggu Rata-rata Minimum?
SJF memprioritaskan proses dengan waktu eksekusi paling pendek. Ini membuat proses-proses cepat selesai duluan, sehingga:
> 	Proses-proses berikutnya tidak perlu menunggu lama.
> 	Waktu tunggu total dari semua proses jadi lebih kecil.
> 	Secara matematis, ini terbukti optimal untuk meminimalkan average waiting time dalam kondisi ideal.
Contoh sederhana:
> 	Proses A: 2 detik
> 	Proses B: 4 detik
> 	Proses C: 8 detik
Jika dijalankan dengan FCFS (urutan A-B-C), waktu tunggu rata-rata = (0 + 2 + 6) / 3 = 2.67 detik
Jika dijalankan dengan urutan SJF (A-B-C, sama urutan karena A paling pendek), hasilnya sama. Tapi jika urutan awalnya C-B-A, FCFS akan jauh lebih buruk.


3. Apa kelemahan SJF jika diterapkan pada sistem interaktif?

   **Jawaban:**  

Kelemahan SJF di Sistem Interaktif
SJF punya beberapa kelemahan serius jika diterapkan di sistem interaktif seperti OS modern:
- 	Tidak Responsif terhadap Proses Pendek yang Baru Datang
Proses interaktif (misalnya input keyboard) bisa tertunda jika proses panjang sedang berjalan dan SJF bersifat non-preemptive.
- 	Estimasi Waktu Eksekusi Sulit
Sistem interaktif sulit memprediksi burst time secara akurat, karena proses bisa sangat dinamis.
- 	Starvation (Kelaparan Proses)
Proses dengan waktu eksekusi panjang bisa terus tertunda jika selalu ada proses pendek yang datang.
- 	Kurang Adil
Pengguna dengan proses berat (misalnya rendering video) bisa merasa sistem lambat karena prosesnya terus ditunda.

---

## Refleksi Diri
Tuliskan secara singkat:
- Apa bagian yang paling menantang minggu ini?  
memahami tugas
- Bagaimana cara Anda mengatasinya?  
bertanya teman

---

**Credit:**  
_Template laporan praktikum Sistem Operasi (SO-202501) – Universitas Putra Bangsa_
