
## Laporan Praktikum Minggu [7]
Topik: [Sinkronisasi Proses dan Masalah Deadlock]gu

---

## Identitas
- **Nama** **NIM** : [Rafid Raihan Yuda Permana][Ketua][250202962][Implementasi]  
- **Nama** **NIM**   [AUfa Rifaah][250202932][Dokumentasi]  
- **Nama** **NIM**   [Azid Mirza Maluana][250202933][Analisis]
- **NIM**          : [1IKRB]

---

  
> ## Tujuan
1. Mengidentifikasi empat kondisi penyebab kebuntuan ( mutual exclusion, hold and wait, no preemption,circular wait ).
2. Menjelaskan mekanisme sinkronisasi menggunakan semaphore atau monitor .
3. Menganalisis dan memberikan solusi untuk kasus kebuntuan.
4. Berkolaborasi dalam waktu untuk menyusun laporan analisis.
5. Menyajikan hasil studi kasus secara sistematis.

---

 ## Dasar Teori
- Sinkronisasi proses adalah mekanisme pengaturan jalannya beberapa proses yang berjalan secara bersamaan dalam sistem operasi agar tidak terjadi konflik dalam mengakses sumber daya atau data bersama. Sinkronisasi penting untuk menghindari inkonsistensi data yang dapat terjadi karena proses-proses tersebut dapat mengakses dan memodifikasi data secara bersamaan. Mekanisme ini menjamin bahwa proses yang bersaing untuk mengakses ke sumber daya bersama dapat melakukannya secara berurutan dan terkontrol, sehingga menghindari masalah seperti kondisi ras dan ketidakkonsistenan data.
- Masalah deadlock adalah kondisi dimana beberapa proses saling menunggu satu sama lain untuk melepaskan sumber daya yang dibutuhkan, sehingga tidak ada proses yang dapat melanjutkan eksekusinya. Deadlock terjadi bila empat kondisi utama terpenuhi sekaligus, yakni: mutualclusion (satu sumber daya hanya bisa digunakan satu proses pada suatu waktu), hold and wait (proses menahan satu sumber daya sambil menunggu sumber daya lain), no preemption (sumber daya tidak bisa diambil paksa dari proses yang memilikinya), dancircular wait (terdapat siklus menunggu sumber daya antar proses). Pemahaman dan penanganan deadlock memerlukan pengenalan kondisi ini serta penggunaan teknik sinkronisasi seperti semaphore dan monitor untuk mencegah atau mengatasi kebuntuan.
---

## Langkah Praktikum
1.  Eksperimen 1 – Simulasi Dining Philosophers (Deadlock Version)

- Implementasikan versi sederhana dari masalah Dining Philosophers tanpa mekanisme pencegahan deadlock.
Contoh pseudocode:
while true:
  think()
  pick_left_fork()
  pick_right_fork()
  eat()
  put_left_fork()
  put_right_fork()

- Jalankan simulasi atau analisis alur (boleh menggunakan pseudocode atau diagram alur).
- Identifikasi kapan dan mengapa kebuntuan terjadi.

2. Eksperimen 2 – Versi Tetap (Menggunakan Semaphore / Monitor)

*Modifikasi pseudocode agar deadlock tidak terjadi, misalnya:
-Menggunakan semaphore (mutex) untuk mengontrol akses.
-Membatasi jumlah filosof yang dapat dimakan secara bersamaan (maks 4).
-pengaturan urutan pengambilan garpu (misal, filosof terakhir mengambil secara terbalik).
*Analisis hasil modifikasi dan buktikan bahwa kebuntuan telah dihindari.

----


----
3. Eksperimen 3 – Analisis Kebuntuan
Menjelaskan empat kondisi deadlock dari versi pertama dan bagaimana kondisi tersebut menyelesaikan pada versi fixed.

Sajikan hasil analisis dalam tabel seperti contoh berikut:
----
Kondisi Deadlock	Terjadi di Versi Deadlock	Solusi di Versi Fixed
Pengecualian Bersama	Ya (satu garpu hanya satu proses)	Gunakan semaphore untuk mengontrol akses
Tahan dan Tunggu	Ya	Hindari proses menahan lebih dari satu sumber daya
Tidak Ada Pendahuluan	Ya	Tidak ada mekanisme pelepasan paksa
Menunggu Melingkar	Ya	Ubah urutan pengambilan sumber day
----


4. Eksperimen 4 – Dokumentasi

Simpan semua diagram, simulasi tangkapan layar, dan hasil diskusi di:
praktikum/week7-concurrency-deadlock/screenshots/
Tuliskan laporan kelompok di laporan.md(format IMRaD singkat: Pendahuluan, Metode, Hasil, Analisis, Diskusi ).

---

## Kode / Perintah
Tuliskan potongan kode atau perintah utama:

while true:

  think()
  pick_left_fork()
  pick_right_fork()
  eat()
  put_left_fork()
  put_right_fork()

1. think (Setiap filosofi berpikir)
2. pick_left_fork (Setelah selesai berpikir, ia mencoba mengambil garpu kiri terlebih dahulu)
3. pick_right_fork (Kemudian mencoba mengambil garpu kanan)
4. eat (Jika kedua garpu sudah dipegang, filosofi mulai makan)
5. put_left_fork, put_right_fork (Setelah makan, ia meletakkan kembali garpu kiri dan kanan)
6. Siklus berulang terus.

- identifikasi kebuntuan
Kebuntuan ketika semua filosofi mengambil garpu kiri secara bersamaan dan kemudian menunggu garpu kanan yang sedang dipegang oleh filosofi sebelahnya. Kondisi ini menyebabkan siklus penantian melingkar (circular wait), di mana tidak ada filosofi yang bisa melanjutkan makan karena masing-masing menunggu garpu

## eksperimen 2

semaphore mutex = 1;           // Kontrol akses kritis
semaphore room = 4;            // Maks 4 filosof bersamaan  
semaphore fork[5] = {1,1,1,1,1}; // 5 garpu

philosopher(i):
  while true:
    think()
    
    wait(room)                 // 1. Batasi 4 filosof
    
    wait(mutex)                // 2. Critical section
    if i == 4:                 // 3. Filosof terakhir: urutan TERBALIK
      wait(fork[4])            // ambil fork4 dulu (kanan)
      wait(fork[0])            // baru fork0 (kiri)  
    else:
      wait(fork[i])            // normal: kiri dulu
      wait(fork[(i+1)%5])      // kanan
    signal(mutex)
    
    eat()
    
    if i == 4:
      signal(fork[0])          // lepas sesuai urutan ambil
      signal(fork[4])
    else:
      signal(fork[(i+1)%5])
      signal(fork[i])
    signal(room)

- analisis 4 kondisi deadlock - bukti keamanan

| Kondisi Deadlock | Terjadi di Versi Asli        | Versi Fixed | Penjelasan Pencegahan
              
| ---------------- | ---------------------------- | ----------- | -----------------------
| Mutual Exclusion | Ya                           | Ya          | Fork tetap eksklusif 1 proses   
                   |
| Hold & Wait      | Ya                           | Dikontrol   | Mutex pastikan ambil 2 fork atomik
                   |
| No Preemption    | Ya                           | Ya          | Tetap, tapi tidak  masalah
                   |
| Circular Wait    | Ya(siklus P0→P1→P2→P3→P4→P0) | TIDAK       | Resource hierarchy putus siklus
               
----
vixed

Filosof 0: fork0 → fork1
Filosof 1: fork1 → fork2  
Filosof 2: fork2 → fork3
Filosof 3: fork3 → fork4
Filosof 4: fork4 → fork0 

analisis
Tidak circular wait karena filosof 4 selalu ambil fork 4 dulu, sedangkan yang lain ambil nomor rendah dulu. Urutan total tercipta: fork0 < fork1 < fork2 < fork3 < fork4.

---

## Hasil Eksekusi
Sertakan screenshot hasil percobaan atau diagram:
![Screenshot hasil](/screenshots/WhatsApp%20Image%202025-12-10%20at%2016.11.08.jpeg)

---

## Analisis
- Eksperimen pertama, 5 filsuf dapat mencapai deadlock permanen saat semua mengambil garpu kiri bersamaan lalu menunggu garpu kanan, memenuhi 4 kondisi Coffman secara penuh. Simulasi alur mengilustrasikan circular wait (P0→F1→P1→F2→...→P4→F0), menyebabkan sistem terkunci total tanpa kemajuan. Hasil ini membuktikan bahaya race condition dan urutan pengambilan sumber daya yang simetris dalam sistem konkuren.​

- ekperimen kedua Modifikasi dengan semaphore room=4 dan asimetri P4 
mematahkan circular wait karena selalu ada minimal 1 garpu bebas, memungkinkan progres kontinu. Simulasi menunjukkan 4 filsuf makan bergantian sementara 1 menunggu, menghindari kebuntuan sambil mempertahankan paralelisme maksimal. Teknik ini menjamin liveness (tidak ada starvation) melalui fairness semaphore FIFO.
---

## Kesimpulan
Tuliskan 2–3 poin kesimpulan dari praktikum ini.

Eksperimen Sinkronisasi & Deadlock
Eksperimen Dining Philosophers membuktikan bahwa implementasi tanpa sinkronisasi menyebabkan deadlock permanen melalui circular wait saat semua filsuf mengambil garpu kiri bersamaan, memenuhi 4 kondisi. Modifikasi dengan semaphore room=4 dan asimetri berhasil mematahkan circular wait, menjamin progres kontinu karena selalu ada minimal 1 garpu bebas.​

1. Pencegahan > Deteksi: Mengontrol akses sumber daya (semaphore) lebih efisien daripada recovery deadlock.​

2. Kondisi Kritis: Sinkronisasi esensial untuk hindari race condition di sistem konkuren seperti multi-threading dan database locks.​

3. Praktik Industri: Teknik ini diterapkan di Linux mutex, Java synchronized, dan Web3 smart contract concurrency.​


---

## Quiz
1. [anggapan empat kondisi utama menyebabkan kebuntuan]  
   **Jawaban:**  Empat kondisi utama yang menyebabkan kebuntuan (deadlock) dalam sistem operasi adalah pengecualian bersama (mutual exclusion), tahan dan tunggu (hold and wait), tidak ada preemption (no preemption), serta tunggu melingkar (circular wait). dikenal sebagai kondisi Coffman, harus terjadi secara bersamaan agar kebuntuan muncul, di mana proses saling menunggu sumber daya satu sama lain tanpa kemajuan.
2. [Mengapa sinkronisasi diperlukan dalam sistem operasi?]  
   **Jawaban:**  Sinkronisasi diperlukan dalam sistem operasi untuk mengatur akses bersamaan oleh beberapa proses terhadap sumber daya bersama, sehingga mencegah inkonsistensi data akibat race condition di mana proses saling bertabrakan saat membaca atau menulis data yang sama.​
   1. Mencegah Race Condition
   2. Menjaga Konsistensi Data
   3. Mengatur Urutan Proses
3. [Menjelaskan perbedaan antara semaphore dan monitor .]  
   **Jawaban:**  Semaphore dan monitor merupakan mekanisme sinkronisasi dalam sistem operasi untuk mengelola akses proses ke sumber daya bersama, tetapi semaphore menggunakan variabel integer dengan operasi wait (P) dan signal (V) yang low-level, sedangkan monitor adalah struktur high-level yang menyediakan mutual exclusion otomatis melalui prosedur eksklusif.

---

## Refleksi Diri
Tuliskan secara singkat:
- Apa bagian yang paling menantang minggu ini? 
terkendala hujan (pencarian koneksi yang memadai)
- Bagaimana cara Anda mengatasinya?  
mengerjakan di tempat pengerjaan sebelum hujan

---

**Credit:**  
_Template laporan praktikum Sistem Operasi (SO-202501) – Universitas Putra Bangsa_
