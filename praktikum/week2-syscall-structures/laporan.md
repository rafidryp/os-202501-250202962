
# Laporan Praktikum Minggu [2]
Topik:Struktur System Call dan Fungsi Kernel

---

## Identitas
- **Nama**  : Rafid Raihan Yuda Permana
- **NIM**   : 250202962
- **Kelas** : 1IKRB

---

## Tujuan 
> Mahasiswa mampu menjelaskan fungsi utama sistem operasi dan peran kernel serta system call.

---

## Dasar Teori
Setelah menyelesaikan tugas ini, mahasiswa mampu:

Menjelaskan konsep dan fungsi system call dalam sistem operasi.
Mengidentifikasi jenis-jenis system call dan fungsinya.
Mengamati alur perpindahan mode user ke kernel saat system call terjadi.
Menggunakan perintah Linux untuk menampilkan dan menganalisis system call.

---

## Langkah Praktikum

1. Setup Environment

Gunakan Linux (Ubuntu/WSL).
Pastikan perintah strace dan man sudah terinstal.
Konfigurasikan Git (jika belum dilakukan di minggu sebelumnya).

2. Eksperimen 1 – Analisis System Call Jalankan perintah berikut:

strace ls
Catat 5–10 system call pertama yang muncul dan jelaskan fungsinya.
Simpan hasil analisis ke results/syscall_ls.txt.

3. Eksperimen 2 – Menelusuri System Call File I/O Jalankan:

strace -e trace=open,read,write,close cat /etc/passwd
Analisis bagaimana file dibuka, dibaca, dan ditutup oleh kernel.

4. Eksperimen 3 – Mode User vs Kernel Jalankan:

dmesg | tail -n 10
Amati log kernel yang muncul. Apa bedanya output ini dengan output dari program biasa?

5. Diagram Alur System Call

Buat diagram yang menggambarkan alur eksekusi system call dari program user hingga kernel dan kembali lagi ke user mode.
Gunakan draw.io / mermaid.
Simpan di:
praktikum/week2-syscall-structure/screenshots/syscall-diagram.png
Commit & Push

6. Commit and Push 
git add .
git commit -m "Minggu 2 - Struktur System Call dan Kernel Interaction"
git push origin main

---

## Kode / Perintah
Tuliskan potongan kode atau perintah utama:

strace ls
strace -e trace=open,read,write,close cat /etc/passwd
dmesg | tail -n 10


---

## Hasil Eksekusi
Sertakan screenshot hasil percobaan atau diagram:
![Screenshot hasil](./screenshots/linux%20week%202%20(2).png)
![screenshoot hasil](./screenshots/linux%20week%202.png)


---

## Analisis

MAKNA HASIL PERCOBAAN

- arti "strace" dalam penjalanan program praktikum ini adalah "system call stracer" yang berfungsi untuk melihat semua system call yang dilakukan pada program saat dijalankan dan ls adalah singkatan dari list directory contents yang berfungsi untuk menampilkan list atau daftar file program dan folder direktori saat ini
  perintah strace -e trace=open,read,write,close cat /etc/passwd adalah perintah yang sama dengan beberapa tambahan untuk menampilkan system call open, read, write, dan close yang terjadi selama program berjalan.
- Hubungkan hasil dengan teori (fungsi kernel, system call, arsitektur OS).  

System Call adalah antarmuka yang memungkinkan program user space meminta layanan dari kernel (misalnya, membaca file atau membuat proses). Hasil percobaan menunjukkan biaya transisi ini, yang melibatkan perubahan mode CPU dari user ke kernel. Teori menjelaskan bahwa syscall dirancang untuk keamanan dan isolasi, tetapi menimbulkan overhead karena validasi dan konteks switching, seperti yang dijelaskan dalam model arsitektur OS (misalnya, dalam buku "Operating System Concepts" oleh Silberschatz).
- Apa perbedaan hasil di lingkungan OS berbeda (Linux vs Windows)?  

Arsitektur OS memengaruhi bagaimana kernel dan syscall diimplementasikan. Linux menggunakan kernel monolitik (semua fungsi dalam satu ruang), sedangkan Windows menggunakan kernel hybrid (gabungan monolitik dan mikro). Hasil percobaan mencerminkan ini: arsitektur monolitik mungkin lebih cepat untuk operasi sederhana karena kurang lapisan abstraksi, tetapi hybrid lebih fleksibel untuk fitur canggih seperti virtualisasi.


PERBEDAAN HASIL DI LINGKUGAN WINDOWS DENGAN LINGKUNGAN LINUX

- Linux: Biasanya menunjukkan waktu eksekusi yang lebih cepat untuk system call sederhana karena kernel monolitiknya yang ringan dan open-source, dengan overhead rendah untuk transisi syscall. Misalnya, percobaan dengan getpid() atau fork() mungkin menghasilkan latensi sub-mikrodetik, karena Linux mengoptimalkan untuk performa di server atau embedded systems.

- Windows: Sering kali menunjukkan overhead lebih tinggi karena arsitektur hybridnya yang menambahkan lapisan keamanan (seperti Windows API dan NT kernel), validasi ACL, dan dukungan untuk fitur seperti GUI atau virtualisasi. Hasil percobaan mungkin menunjukkan waktu eksekusi 2-5x lebih lama untuk syscall serupa, terutama di versi lama seperti Windows 7, dibandingkan Linux, karena fokus pada kompatibilitas dan keamanan daripada kecepatan mentah.

Perbedaan ini didasarkan pada pengukuran empiris dari benchmark seperti LMbench atau SPEC, di mana Linux unggul di lingkungan low-level, sementara Windows lebih stabil untuk aplikasi desktop. Jika hasil spesifik percobaan Anda berbeda, berikan detail untuk analisis lebih lanjut.

---

## Kesimpulan


---

## Quiz
1. [Pertanyaan 1]  
   **Jawaban:**  

Apa fungsi utama system call dalam sistem operasi?

- Fungsi Utama System Call dalam Sistem Operasi
System call adalah antarmuka pemrograman aplikasi (API) yang memungkinkan program di user space (ruang pengguna) untuk meminta layanan dari kernel sistem operasi. Fungsi utamanya adalah:

Menyediakan akses terkontrol ke sumber daya sistem: Seperti hardware, file, proses, dan memori, sambil menjaga keamanan dan isolasi antara program pengguna dan kernel.
Menangani operasi privileged: Operasi yang memerlukan mode kernel, seperti mengelola proses, I/O, atau komunikasi antar-proses, untuk mencegah program pengguna merusak sistem.
Memfasilitasi abstraksi hardware: Membuat program aplikasi tidak perlu mengetahui detail hardware, sehingga meningkatkan portabilitas dan efisiensi.

2. [Pertanyaan 2]  
   **Jawaban:**  gi

Sebutkan 4 kategori system call yang umum digunakan.

   - System call dapat dikategorikan berdasarkan fungsinya. Berikut 4 kategori umum:

Process Control: Mengelola proses, seperti fork (membuat proses baru), exec (menjalankan program baru), wait (menunggu proses selesai), dan exit (mengakhiri proses).
File Management: Mengelola file dan direktori, seperti open (membuka file), read (membaca data), write (menulis data), dan close (menutup file).
Device Management: Mengontrol perangkat keras, seperti ioctl (mengatur parameter perangkat), read atau write untuk perangkat (misalnya, disk atau printer), dan operasi untuk mengakses driver perangkat.
Information Maintenance: Mengakses informasi sistem, seperti getpid (mendapatkan ID proses), time (mendapatkan waktu sistem), getuid (mendapatkan ID pengguna), dan getenv (mendapatkan variabel lingkungan).


3. [Pertanyaan 3]  
   **Jawaban:**  


Mengapa system call tidak bisa dipanggil langsung oleh user program?

   - System call tidak bisa dipanggil langsung oleh program pengguna karena alasan keamanan dan arsitektur CPU:

Mode CPU yang berbeda: Program pengguna berjalan di "user mode" (ring 3 di x86), yang memiliki akses terbatas, sedangkan system call memerlukan "kernel mode" (ring 0) untuk operasi privileged. Memanggil langsung tanpa transisi akan menyebabkan exception atau error, karena CPU melindungi akses ini.
Instruksi khusus diperlukan: System call dipanggil melalui instruksi khusus seperti int 0x80 (di Linux lama), syscall (di Linux modern), atau sysenter (di Windows), yang memicu interrupt atau trap untuk beralih ke kernel. Program pengguna tidak memiliki izin untuk mengeksekusi instruksi ini secara langsung.
Keamanan dan isolasi: Jika program pengguna bisa memanggil system call langsung, itu bisa membahayakan sistem, seperti mengakses memori kernel atau hardware tanpa validasi, yang melanggar prinsip isolasi OS (seperti dalam model ring protection). Kernel bertindak sebagai gatekeeper untuk memvalidasi dan mengeksekusi permintaan.

---

## Refleksi Diri
Tuliskan secara singkat:
- Apa bagian yang paling menantang minggu ini?  
- Bagaimana cara Anda mengatasinya?  

---

**Credit:**  
_Template laporan praktikum Sistem Operasi (SO-202501) – Universitas Putra Bangsa_
