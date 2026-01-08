
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
> Setelah menyelesaikan tugas ini, mahasiswa mampu:

1. Menghitung waiting time dan turnaround time pada algoritma RR dan  Priority.
2. Menyusun tabel hasil perhitungan dengan benar dan sistematis.
3. Membandingkan performa algoritma RR dan Priority.
4. Menjelaskan pengaruh time quantum dan prioritas terhadap keadilan eksekusi proses.
5. Menarik kesimpulan mengenai efisiensi dan keadilan kedua algoritma.

---

## Dasar Teori
Tuliskan ringkasan teori (3–5 poin) yang mendasari percobaan.

1. Waiting Time dan Turnaround Time
2. Penyusunan Tabel Hasil Perhitungan
3. Perbandingan Performa RR dan Priority
4. Pengaruh Time Quantum dan Prioritas
5. Kesimpulan Efisiensi dan Keadilan

---

## Langkah Praktikum
1. Menghitung waiting time dan turnaround time pada algoritma RR dan Priority.
2. Menyusun tabel hasil perhitungan dengan benar dan sistematis.
3. Membandingkan performa algoritma RR dan Priority.
4. Menjelaskan pengaruh time quantum dan prioritas terhadap keadilan eksekusi proses.
5. Menarik kesimpulan mengenai efisiensi dan keadilan kedua algoritma.

---

## Kode / Perintah
Tuliskan potongan kode atau perintah utama:

WT[i] = waktu mulai eksekusi - Arrival[i]
TAT[i] = WT[i] + Burst[i]


---

## Hasil Eksekusi
Sertakan screenshot hasil percobaan atau diagram:

TABEL ROUND ROBIN (RR) DAN PRIORITY SCHEDULING
1. ![Screenshot hasil](./screenshots/Screenshot%202026-01-08%20015856.png)

EKSPERIMEN 1
2. ![Screenshot hasil](./screenshots/Screenshot%202026-01-08%20015903.png)

ghant chart FCFS

0 3 6 9 12 13 15 18 21 24 25 26
|P1|P2|P3|P1|P4|P5|P2|P3|P5|P2|


EKSPERIMEN 2
3. ![Screenshot hasil](./screenshots/Screenshot%202026-01-08%20015911.png)

ghant chart FCFS

0   4        13      19      24    26
| P1 |   P2   |  P5  |  P3  | P4 |


| Algoritma                     | Avg Waiting Time | Avg Turnaround Time | Kelebihan                                                                                                      | Kekurangan                                                                                                          |
| ----------------------------- | ---------------- | ------------------- | -------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------- |
| **FCFS**                      | 7.2              | 12.4                | - Algoritma paling sederhana<br>- Mudah diimplementasikan<br>- Overhead kecil                                  | - Tidak mempertimbangkan burst time<br>- Bisa terjadi *convoy effect*<br>- Kurang efisien untuk sistem multitasking |
| **Round Robin (q = 3)**       | 11.6             | 16.8                | - Adil untuk semua proses<br>- Cocok untuk *time-sharing system*<br>- Tidak ada starvation                     | - Waiting time relatif besar<br>- Bergantung pada ukuran time quantum<br>- Overhead context switching tinggi        |
| **Priority (Non-Preemptive)** | 8.2              | 13.4                | - Proses penting dieksekusi lebih cepat<br>- Lebih efisien dari RR<br>- Cocok untuk sistem real-time sederhana | - Bisa terjadi starvation<br>- Penentuan priority harus tepat<br>- Kurang adil untuk proses prioritas rendah        |


---

## Analisis
-Analisis

Berdasarkan hasil pengujian tiga algoritma penjadwalan CPU yaitu FCFS, Round Robin, dan Priority Scheduling menggunakan dataset yang sama, diperoleh perbedaan kinerja yang cukup signifikan pada nilai waiting time dan turnaround time.

Algoritma FCFS (First Come First Serve) mengeksekusi proses berdasarkan urutan kedatangan tanpa mempertimbangkan lama waktu eksekusi maupun tingkat prioritas. Dari hasil perhitungan, FCFS menghasilkan rata-rata waiting time sebesar 7.2 dan rata-rata turnaround time sebesar 12.4. Nilai ini relatif rendah dibandingkan algoritma lainnya karena proses awal memiliki burst time yang kecil, sehingga tidak menimbulkan antrean panjang di awal eksekusi. Namun, FCFS berpotensi menimbulkan convoy effect apabila proses pertama memiliki burst time besar.


---

## Kesimpulan
Kesimpulan

Dari hasil analisis dapat disimpulkan bahwa:

1. FCFS memiliki implementasi paling sederhana dan menghasilkan nilai waiting time yang rendah pada dataset ini, tetapi kurang fleksibel untuk sistem dengan beban kerja tinggi.

2. Round Robin memberikan keadilan bagi semua proses, namun memiliki waiting time dan turnaround time paling besar akibat banyaknya pergantian konteks.

3. Priority Scheduling memberikan keseimbangan antara efisiensi dan kecepatan eksekusi proses penting, tetapi berisiko menimbulkan starvation.

Pemilihan algoritma penjadwalan CPU sebaiknya disesuaikan dengan kebutuhan sistem. Untuk sistem sederhana, FCFS sudah memadai; untuk sistem interaktif, Round Robin lebih sesuai; sedangkan untuk sistem yang membutuhkan penanganan proses penting secara cepat, Priority Scheduling menjadi pilihan yang lebih efektif.

---

## Quiz
1. [Pertanyaan 1]  
   **Jawaban:** 
Perbedaan utama antara Round Robin (RR) dan Priority Scheduling terletak pada dasar pemilihan proses yang dieksekusi oleh CPU.

Round Robin menjadwalkan proses secara bergiliran dengan jatah waktu yang sama (time quantum) untuk setiap proses. Semua proses memiliki kesempatan yang adil untuk menggunakan CPU tanpa memperhatikan prioritas atau lama eksekusi.

Priority Scheduling menjadwalkan proses berdasarkan tingkat prioritas. Proses dengan prioritas tertinggi akan dieksekusi lebih dahulu, sedangkan proses dengan prioritas rendah harus menunggu.

Kesimpulan perbedaan utama:

RR menekankan keadilan (fairness)

Priority menekankan kepentingan proses (importance)

2. [Pertanyaan 2]  
   **Jawaban:**  
   2. Pengaruh Besar/Kecilnya Time Quantum terhadap Performa Sistem
   
Ukuran time quantum pada algoritma Round Robin sangat berpengaruh terhadap performa sistem.

Time Quantum Terlalu Kecil

1. Terjadi context switching terlalu sering
2. Overhead sistem meningkat
3. CPU lebih banyak digunakan untuk berpindah proses daripada mengeksekusi proses

Time Quantum Terlalu Besar

1. Round Robin mendekati FCFS
2. Respons sistem menjadi lambat
3. Proses interaktif kehilangan keunggulan respons cepat

Time Quantum Ideal

1. Memberikan keseimbangan antara:
2. Respons cepat
3. Overhead context switching yang rendah

Umumnya dipilih sedikit lebih besar dari waktu context switch


Tinggal bilang 👍
3. [Pertanyaan 3]  
   **Jawaban:**  
   3. Mengapa Algoritma Priority Dapat Menyebabkan Starvation

Starvation terjadi ketika suatu proses tidak pernah mendapatkan CPU karena selalu dikalahkan oleh proses lain.

Pada Priority Scheduling, starvation dapat terjadi karena:

1. Proses dengan prioritas rendah terus-menerus dikalahkan
2. Proses prioritas tinggi terus datang ke sistem
3. CPU selalu sibuk mengeksekusi proses prioritas tinggi

Akibatnya:

1. Proses prioritas rendah menunggu sangat lama atau tidak pernah dieksekusi
Solusi Umum
2. Menggunakan aging (menaikkan prioritas proses secara bertahap)
3. Mengombinasikan priority dengan RR

---

## Refleksi Diri
Tuliskan secara singkat:
- Apa bagian yang paling menantang minggu ini?
mengatur waktu antar tugas setiap matkul
- Bagaimana cara Anda mengatasinya?
membagi waktu kosong untuk pengerjaan tugas

---

**Credit:**  
_Template laporan praktikum Sistem Operasi (SO-202501) – Universitas Putra Bangsa_
