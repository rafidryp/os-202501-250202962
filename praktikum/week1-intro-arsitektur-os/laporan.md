
# Laporan Praktikum Minggu 1
Topik: "Arsitektur Sistem Operasi dan Kernel"

---

## Identitas
- **Nama**  : Rafid Raihan Yuda Permana
- **NIM**   : 250209262
- **Kelas** : 1IKRB

---

## Tujuan
> Mahasiswa mampu menjelaskan fungsi utama sistem operasi dan peran kernel serta system call.

---

## Dasar Teori
Mahasiswa dapat

 - Membedakan kernel mode dan user mode
 - Mempelajari system call
 - membandingkan monolithic kernel,layered approach, dan mikro kernel

 Mahasiswa akan melakukan teori tersebut berdasarkan perintah dasar linux

---

## Langkah Praktikum
1. Setup Environment

Pastikan Linux (Ubuntu/WSL) sudah terinstal.
Pastikan Git sudah dikonfigurasi dengan benar:

 git config --global user.name "Nama Anda"
 git config --global user.email "email@contoh.com"

2. Diskusi Konsep

Baca materi pengantar tentang komponen OS.
Identifikasi komponen yang ada pada Linux/Windows/Android.
3. Eksperimen Dasar

 Jalankan perintah berikut di terminal:

 uname -a
 whoami
 lsmod | head
 dmesg | head

Catat dan analisis modul kernel yang tampil.

4. Membuat Diagram Arsitektur

Buat diagram hubungan antara User → System Call → Kernel → Hardware.
Gunakan draw.io atau Mermaid.
Simpan hasilnya di:
praktikum/week1-intro-arsitektur-os/screenshots/diagram-os.png
Penulisan Laporan

5. Penulisan Laporan

Tuliskan hasil pengamatan, analisis, dan kesimpulan ke dalam laporan.md.
Tambahkan screenshot hasil terminal ke folder screenshots/.

6. Commit & Push

git add .
git commit -m "Minggu 1 - Arsitektur Sistem Operasi dan Kernel"
git push origin main
.

---

## Kode / Perintah
Tuliskan potongan kode atau perintah utama:
```bash
uname -a
whoami
lsmod | head
dmesg | head
```

---

## Hasil Eksekusi
Sertakan screenshot hasil percobaan atau diagram:
![Screenshot hasil](./screenshots/linux%20-1.png)

---

## Analisis
- Jelaskan makna hasil percobaan. 

uname -a format untuk mencetak semua informasi sistem (kernel). uname adalah singkatan dari "Unix name".
 -a adalah opsi untuk "all" (semua).

 output akan memberikan informasi seperti nama dan versi kernel,tipe prossesor,nama host, dan sistem oprasi.

 Output akan menampilkan informasi detail seperti nama kernel (e.g., Linux), versi kernel, tipe prosesor, nama host sistem, dan sistem operasi. Ini sering digunakan untuk mengetahui spesifikasi dasar sistem Anda.

whoami Perintah ini digunakan untuk mencetak nama pengguna yang saat ini gunakan . Sebenarnya, sistem ini berjalan untuk memastikan siapa anda/user yang sedang menggunakan perangkat dengan menyesuaikan email pengguna saat itu(seperti system dengan kata "wo am i").

lsmod | head Perintah ini digunakan untuk menampilkan daftar modul kernel yang saat ini dimuat. Namun,hanya menampilkan beberapa baris pertama. lsmod adalah singkatan dari "list modules" (daftar modul). Modul kernel adalah kode yang dapat dimuat secara dinamis ke dalam kernel untuk memperluas fungsionalitasnya (misalnya, driver untuk perangkat keras).

pipa/pipe mengarahkan input perintah sebelah kiri ke sebelah kanan (lsmod - pipa - head)

makna keseluruhan : menampilkan daftar modul kernel namun hanya mengambil 10 baris

dmesg | head menampilkan log buffer kernel namun hanya beberapa baris pertama

dmesg juga dapat di definisikan sebagai display massage atau menampilkan pesan. Berjalan dengan cara menampilkan kernel selama booting dan selama operasi , mencakup informasi tentang driver



- Hubungkan hasil dengan teori (fungsi kernel, system call, arsitektur OS). 
1. fungsi kernel
 berjalan dengan kurang maksimal menandakan kendala device atau media yang dalamnya kurang mencukupi yang disertai kendala koneksi

2. system call
system call mengkonfirmasi overhead saat berinteraksi dengan kernel yang disebabkan dengan tinggi nya frekuensi system call

3. arsitektur OS
dampak nya menyebabkan perbedaan kecepatan
- Apa perbedaan hasil di lingkungan OS berbeda (Linux vs Windows)?  

1. dampak kinerja linux
Kinerja I/O lebih cepat dan stabil karena semua komponen terintegrasi, sehingga overhead komunikasi internal rendah.

2. windows
Lebih stabil berkat isolasi modul, namun memiliki overhead tambahan akibat lapisan API dan komunikasi antar-proses.

---

## Kesimpulan
 -setiap pemrograman harus dilakukan dengan runtut agar proses dapat berjalan dengan baik dan sesuai dengan langkah langkah praktikum 
 -system yang termasuk sulit untuk di pelajari serta di hafalkan yang tentunya diluar nalar dan akal manusia
 -harus didorong dengan motivasi dan pengalaman serta penjelasan yang jelas
---

## Quiz
1. [Pertanyaan 1]  Apa yang didapat dari praktikum kali ini
   **Jawaban:** Sebuah kesimpulan yaitu menjalankan sebuah system harus memadai bebrapa faktor seperti device yang memadai dan koneksi yang lancar agar program dapat berjalan lancar
2. [Pertanyaan 2]  apa halangan yang bisa saja di dapat saat
    praktikum
   **Jawaban:**  halangan device dan jaringan
3. [Pertanyaan 3]  bagaimana cara praktikum dapat bekerja
   dengan lancar
   **Jawaban:**  mencari tempat dengan jaringan koneksi yang lancar

---

## Refleksi Diri
Tuliskan secara singkat:
- penerapan setiap aplikasi pada device,pencernaan atau pemahaman pada materi, dan cara eksekusi harus dibantu sesama mahasiswa serta pengumpulan niat yang matang agar praktikum dapat berjalan dengan baik
- Mengoreksi untuk persiapan pertemuan pada hari dan semester selanjutnya

---

**Credit:**  
_Template laporan praktikum Sistem Operasi (SO-202501) – Universitas Putra Bangsa_
