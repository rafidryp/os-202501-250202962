
# Laporan Praktikum Minggu [6]
Topik: [Tuliskan judul topik, misalnya "Arsitektur Sistem Operasi dan Kernel"]

---

## Identitas
- **Nama**  : Rafid Raihan Yuda Permana  
- **NIM**   : 250202962  
- **Kelas** : 1IKRB

---

## Tujuan
Tuliskan tujuan praktikum minggu ini.  
Contoh:  
> Mahasiswa mampu menjelaskan fungsi utama sistem operasi dan peran kernel serta system call.

Setelah menyelesaikan tugas ini, mahasiswa mampu:

1. Menghitung waiting time dan turnaround time pada algoritma RR dan Priority.
2. Menyusun tabel hasil perhitungan dengan benar dan sistematis.
3. Membandingkan performa algoritma RR dan Priority.
4. Menjelaskan pengaruh time quantum dan prioritas terhadap keadilan eksekusi proses.
5. Menarik kesimpulan mengenai efisiensi dan keadilan kedua algoritma.


---

## Dasar Teori
Tuliskan ringkasan teori (3–5 poin) yang mendasari percobaan.

* Konsep Penjadwalan CPU

Penjadwalan CPU adalah proses menentukan urutan eksekusi proses-proses dalam antrian siap (ready queue).
1. Tujuannya adalah untuk:
2.	Memaksimalkan utilisasi CPU (CPU tidak menganggur).
3. Meningkatkan throughput (jumlah proses selesai per satuan waktu).
4. Meminimalkan waiting time (waktu tunggu) dan turnaround time (waktu penyelesaian).
5.	Menjamin fairness (keadilan) antar proses.
---

## Langkah Praktikum

1. Siapkan Data Proses Gunakan contoh data berikut (boleh dimodifikasi sesuai kebutuhan):

Contoh:

Proses	Burst Time	Arrival Time	Priority

| Proses | Burst Time | Arrival Time | Priority |
|--------|------------|--------------|----------|
| P1     | 5          | 0            | 2        |
| P2     | 3          | 1            | 1        |
| P3     | 8          | 2            | 4        |
| P4     | 6          | 3            | 3        |

2. Eksperimen 1 – Round Robin (RR)

Gunakan time quantum (q) = 3.
Hitung waiting time dan turnaround time untuk tiap proses.
Simulasikan eksekusi menggunakan Gantt Chart (manual atau spreadsheet).
| P1 | P2 | P3 | P4 | P1 | P3 | ...
0    3    6    9   12   15   18  ...
Catat sisa burst time tiap putaran.

3. Eksperimen 2 – Priority Scheduling (Non-Preemptive)

Urutkan proses berdasarkan nilai prioritas (angka kecil = prioritas tinggi).
Lakukan perhitungan manual untuk:

WT[i] = waktu mulai eksekusi - Arrival[i]
TAT[i] = WT[i] + Burst[i]

Buat tabel perbandingan hasil RR dan Priority.

4. Eksperimen 3 – Analisis Variasi Time Quantum (Opsional)

Ubah quantum menjadi 2 dan 5.
Amati perubahan nilai rata-rata waiting time dan turnaround time.
Buat tabel perbandingan efek quantum.

5. Eksperimen 4 – Dokumentasi

Simpan semua hasil tabel dan screenshot ke:

praktikum/week6-scheduling-rr-priority/screenshots/

Buat tabel perbandingan seperti berikut:

| Algoritma | Avg Waiting Time | Avg Turnaround Time | Kelebihan                        | Kekurangan                                |
|-----------|------------------|---------------------|----------------------------------|-------------------------------------------|
| RR        | ...              | ...                 | Adil terhadap semua proses       | Tidak efisien jika quantum tidak tepat     |
| Priority  | ...              | ...                 | Efisien untuk proses penting     | Potensi starvation pada prioritas rendah   |

Commit & Push

git add .
git commit -m "Minggu 6 - CPU Scheduling RR & Priority"
git push origin main

---

## Kode / Perintah
Tuliskan potongan kode atau perintah utama:
```bash

WT[i] = waktu mulai eksekusi - Arrival[i]
TAT[i] = WT[i] + Burst[i]

```

---

## Hasil Eksekusi
Sertakan screenshot hasil percobaan atau diagram:
![Screenshot hasil](./screenshots/Screenshot%202026-01-08%20015856.png)

![Screenshot hasil](./screenshots/Screenshot%202026-01-08%20015903.png)

ghanchart FCFS

0   3   6   9   12  13  15  18  21  24  25  26
| P1 | P2 | P1 | P3 | P4 | P5 | P2 | P3 | P5 | P2 |


![Screenshot hasil](./screenshots/Screenshot%202026-01-08%20015911.png)

ghanchart FCFS

0    4    13   19   24   26
| P1 | P2 | P5 | P3 | P4 |

## Tabel Perbandingan Algoritma Penjadwalan CPU

| Aspek Perbandingan | Round Robin | Priority Scheduling |
|--------------------|------------|---------------------|
| Jenis Penjadwalan | Preemptive | Non-Preemptive |
| Dasar Penjadwalan | Time Quantum (q) | Nilai Prioritas |
| Keadilan (Fairness) | Sangat adil, semua proses mendapat giliran | Kurang adil, prioritas rendah bisa lama menunggu |
| Responsivitas | Tinggi, cocok untuk sistem time-sharing | Rendah untuk proses prioritas rendah |
| Kompleksitas Gantt Chart | Kompleks (banyak potongan proses) | Sederhana (proses berjalan penuh) |
| Total Waiting Time | **58** | **41** |
| Rata-rata Waiting Time | **11.6** | **8.2** |
| Total Turnaround Time | **84** | **67** |
| Rata-rata Turnaround Time | **16.8** | **13.4** |
| Risiko Starvation | Tidak ada | Ada (prioritas rendah) |
| Cocok untuk | Sistem interaktif, multi-user | Sistem batch / real-time |
| Contoh Sistem | Time-sharing OS | Embedded / sistem kontrol |

---

## Analisis
- Jelaskan makna hasil percobaan.  

Berdasarkan hasil percobaan penjadwalan CPU menggunakan Round Robin dan Priority Scheduling, diperoleh bahwa:

1. Priority Scheduling menghasilkan waiting time dan turnaround time yang lebih kecil dibandingkan Round Robin.

2. Round Robin memberikan keadilan (fairness) yang lebih baik karena setiap proses mendapat jatah CPU secara bergiliran.

3. Perbedaan nilai waiting time dan turnaround time menunjukkan bahwa strategi penjadwalan sangat memengaruhi performa sistem, terutama pada waktu tunggu prose
- Hubungkan hasil dengan teori (fungsi kernel, system call, arsitektur OS).  

- Apa perbedaan hasil di lingkungan OS berbeda (Linux vs Windows)?  

---

## Kesimpulan

Percobaan ini menunjukkan bahwa:

1. Tidak ada algoritma penjadwalan yang paling sempurna.

2. Round Robin unggul dalam keadilan, sedangkan Priority Scheduling unggul dalam efisiensi waktu.

3. Implementasi nyata di OS (Linux dan Windows) merupakan kombinasi teori scheduling, arsitektur kernel, dan system call untuk mencapai performa optimal.

---

## Quiz
1. Apa perbedaan utama antara Round Robin dan Priority Scheduling?

   **Jawaban:**  
   
   Round Robin dan Priority Scheduling memiliki perbedaan utama pada cara menentukan proses yang memperoleh jatah CPU. Round Robin membagi waktu CPU secara merata kepada setiap proses menggunakan time quantum, sehingga semua proses mendapatkan giliran eksekusi secara adil. Sebaliknya, Priority Scheduling menentukan urutan eksekusi berdasarkan tingkat prioritas, di mana proses dengan prioritas lebih tinggi akan dijalankan lebih dahulu, meskipun proses lain telah menunggu lebih lama.

2. Apa pengaruh besar/kecilnya time quantum terhadap performa sistem?

   **Jawaban:**  

   Besar atau kecilnya time quantum pada Round Robin sangat berpengaruh terhadap performa sistem. Jika time quantum terlalu kecil, sistem akan sering melakukan context switching, yang menyebabkan overhead kernel meningkat dan efisiensi CPU menurun. Namun, jika time quantum terlalu besar, perilaku Round Robin akan mendekati FCFS, sehingga responsivitas sistem menurun karena proses dengan burst time besar dapat mendominasi CPU. Oleh karena itu, pemilihan time quantum yang tepat diperlukan untuk menyeimbangkan efisiensi dan responsivitas sistem.

3. Mengapa algoritma Priority dapat menyebabkan starvation?

   **Jawaban:**  

Algoritma Priority Scheduling dapat menyebabkan starvation karena proses dengan prioritas rendah terus-menerus ditunda eksekusinya apabila selalu ada proses dengan prioritas lebih tinggi yang masuk ke sistem. Akibatnya, proses berprioritas rendah dapat menunggu sangat lama atau bahkan tidak pernah dieksekusi. Kondisi ini umum terjadi pada sistem yang tidak menerapkan mekanisme penyeimbang seperti aging, yang berfungsi menaikkan prioritas proses yang telah lama menunggu

---

## Refleksi Diri
Tuliskan secara singkat:
- Apa bagian yang paling menantang minggu ini? 
Menghandle tugas yang tertinggal dengan tugas terbaru
- Bagaimana cara Anda mengatasinya?  
Mengerjakannya satu persatu

---

**Credit:**  
_Template laporan praktikum Sistem Operasi (SO-202501) – Universitas Putra Bangsa_
