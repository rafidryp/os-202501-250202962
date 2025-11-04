
# Laporan Praktikum Minggu [4]
Topik: [Tuliskan judul topik, misalnya "Arsitektur Sistem Operasi dan Kernel"]

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
Dalam sistem operasi multi-user seperti Linux, manajemen proses dan manajemen user adalah dua konsep fundamental.

Proses adalah sebuah program yang sedang dieksekusi. Setiap kali Anda menjalankan perintah atau aplikasi, sistem operasi akan membuat satu atau lebih proses. Setiap proses memiliki ID unik yang disebut Process ID (PID), informasi mengenai pengguna yang menjalankannya , serta sumber daya yang digunakannya . Proses induk parent process dapat membuat proses turunan child process, membentuk sebuah hierarki yang diawali oleh proses init atau systemd .

Manajemen User adalah cara sistem operasi mengelola siapa saja yang boleh mengakses sistem dan apa saja yang boleh mereka lakukan. Setiap pengguna memiliki User ID (UID) dan tergabung dalam satu atau lebih Group (GID).

---

## Langkah Praktikum
1. Langkah-langkah yang dilakukan.  

 - Setup Environment

  Gunakan Linux (Ubuntu/WSL).
  Pastikan Anda sudah login sebagai user non-root.
  Siapkan folder kerja:
2. Perintah yang dijalankan

praktikum/week4-proses-user/

  - Eksperimen 1 – Identitas User Jalankan perintah berikut:

  whoami
  id
  groups

  Jelaskan setiap output dan fungsinya.
  Buat user baru (jika memiliki izin sudo):

  sudo adduser praktikan
  sudo passwd praktikan

  Uji login ke user baru.

  - Eksperimen 2 – Monitoring Proses Jalankan:

  ps aux | head -10
  top -n 1

  Jelaskan kolom penting seperti PID, USER, %CPU, %MEM, COMMAND.
  Simpan tangkapan layar top ke :

  praktikum/week4-proses-user/screenshots/top.png

  - Eksperimen 3 – Kontrol Proses

  Jalankan program latar belakang:
  sleep 1000 &
  ps aux | grep sleep

  - Catat PID proses sleep.
    Hentikan proses:

    kill <PID>

    Pastikan proses telah berhenti dengan ps aux | grep sleep.

  - Eksperimen 4 – Analisis Hierarki Proses Jalankan:

    pstree -p | head -20

    Amati hierarki proses dan identifikasi proses induk (init/systemd).
    Catat hasilnya dalam laporan.


3. File dan kode yang dibuat.  

Eksperimen dilakukan melalui penggunaan perintah dasar seperti ps, top, kill, adduser, passwd, id, dan groups.

4. Commit message yang digunakan.

- Commit & Push

   git add .
   git commit -m "Minggu 4 - Manajemen Proses & User"
   git push origin main

---

## Kode / Perintah
Tuliskan potongan kode atau perintah utama:
```bash
whoami
id
groups
ps aux | head -10
top -n 1
sleep 1000 &
ps aux | grep sleep
kill <PID>
pstree -p | head -20
```

---

## Hasil Eksekusi
Sertakan screenshot hasil percobaan atau diagram:
![Screenshot hasil](screenshots/example.png)

---

## Analisis
- Jelaskan makna hasil percobaan.  

Eksperimen ini menunjukkan bagaimana Linux mengelola identitas pengguna dan proses sistem. Pengguna dapat dikenali melalui UID, GID, dan grup yang menentukan hak akses. Proses sistem dapat dimonitor, dikendalikan, dan dianalisis melalui perintah seperti ps, top, kill, dan pstree. Dengan memahami struktur proses dan hak akses pengguna, kita dapat mengelola sistem secara efisien dan aman.

- Hubungkan hasil dengan teori (fungsi kernel, system call, arsitektur OS).  

Hubungkan hasil dengan teori (fungsi kernel, system call, arsitektur OS).
Hasil eksperimen menunjukkan bahwa sistem operasi Linux mengelola identitas pengguna dan proses melalui interaksi antara user space dan kernel. Ketika perintah dijalankan, seperti ps, top, atau kill, sistem menggunakan system call untuk meminta layanan dari kernel, yang bertanggung jawab atas pengelolaan memori, proses, dan perangkat. Struktur proses yang ditampilkan dengan pstree mmemberikan arsitektur sistem operasi yang hierarkis, di mana proses induk seperti systemd menginisialisasi dan mengatur proses lainnya.

- Apa perbedaan hasil di lingkungan OS berbeda (Linux vs Windows)?  

Apa perbedaan hasil di lingkungan OS berbeda (Linux vs Windows)?
Di Linux, manajemen user dan proses dilakukan melalui perintah berbasis teks yang langsung berinteraksi dengan kernel melalui system call dan Struktur proses ditampilkan secara hierarkis.



---

## Kesimpulan
Tuliskan 2–3 poin kesimpulan dari praktikum ini.

1. Hierarki proses menunjukkan struktur sistem yang dikendalikan oleh systemd sebagai proses induk
2. Proses sistem dapat dimonitor, dikendalikan, dan dianalisis melalui perintah seperti ps, top, kill, dan pstree.
3. Eksperimen ini menunjukkan bagaimana Linux mengelola identitas pengguna dan proses sistem.

---

## Quiz
1. [Pertanyaan 1]  
   **Jawaban:**  

   Apa fungsi dari proses init atau systemd dalam sistem Linux?

   Proses init adalah program pertama yang dijalankan oleh kernel Linux setelah booting sistem. Fungsinya utama adalah menginisialisasi sistem, mengelola proses-proses sistem, dan memastikan layanan-layanan penting berjalan. Pada sistem lama (seperti SysV init), init membaca file /etc/inittab untuk menentukan level run (misalnya, single-user atau multi-user mode) dan menjalankan skrip startup.

2. [Pertanyaan 2]  
   **Jawaban:**  

   Apa perbedaan antara kill dan killall?

   Kill: Perintah ini mengirim sinyal (biasanya untuk menghentikan proses) ke satu atau lebih proses berdasarkan Process ID (PID) mereka. Contoh: kill 1234 menghentikan proses dengan PID 1234. Ia lebih presisi karena menargetkan PID spesifik, tetapi memerlukan pengetahuan PID (dapat diperoleh dari ps atau top).

   Killall: Perintah ini mengirim sinyal ke semua proses yang cocok dengan nama tertentu, tanpa perlu PID. Contoh: killall firefox menghentikan semua instance proses bernama "firefox". Lebih mudah untuk menghentikan beberapa proses sekaligus, tetapi berpotensi berbahaya jika nama proses tidak unik, karena bisa menghentikan proses yang tidak diinginkan.

3. [Pertanyaan 3]  
   **Jawaban:**  

   Mengapa user root memiliki hak istimewa di sistem Linux?

   User root adalah superuser dengan User ID (UID) 0, yang memberikan akses penuh dan tidak terbatas ke seluruh sistem. Hak istimewa ini dirancang untuk administrasi sistem, seperti menginstal perangkat lunak, mengubah konfigurasi kernel, atau mengelola akun pengguna lainnya. Root dapat:

   -  Mengakses dan memodifikasi semua file, termasuk yang dimiliki oleh pengguna lain.
   - Menjalankan perintah apa pun tanpa batasan izin.
   - Mengubah pengaturan sistemik, seperti firewall atau jaringan.
   
   Ini penting untuk tugas-tugas kritis, tetapi berbahaya jika disalahgunakan (misalnya, risiko keamanan dari malware). Untuk alasan keamanan, pengguna biasa disarankan menggunakan sudo untuk menjalankan perintah sebagai root secara sementara, bukan login sebagai root penuh waktu. Model ini mencegah kesalahan yang tidak disengaja dan serangan privilege escalation.
---

## Refleksi Diri
Tuliskan secara singkat:
- Apa bagian yang paling menantang minggu ini? 

WSL saya tiba tiba eror

- Bagaimana cara Anda mengatasinya?  

mencoba membetulkan

---

**Credit:**  
_Template laporan praktikum Sistem Operasi (SO-202501) – Universitas Putra Bangsa_
