
# Laporan Praktikum Minggu [X]
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
Tuliskan ringkasan teori (3–5 poin) yang mendasari percobaan.

Pada praktikum minggu ini, mahasiswa akan mempelajari mekanisme system call dan struktur sistem operasi. System call adalah antarmuka antara program aplikasi dan kernel yang memungkinkan aplikasi berinteraksi dengan perangkat keras secara aman melalui layanan OS.

Mahasiswa akan melakukan eksplorasi terhadap:

Jenis-jenis system call yang umum digunakan (file, process, device, communication). Alur eksekusi system call dari mode user menuju mode kernel. Cara melihat daftar system call yang aktif di sistem Linux.



---

## Langkah Praktikum
1. Langkah-langkah yang dilakukan.  
2. Perintah yang dijalankan.  
3. File dan kode yang dibuat.  
4. Commit message yang digunakan.

---

## Kode / Perintah
Tuliskan potongan kode atau perintah utama:
```bash

pwd
ls -l
cd /tmp
ls -a

cat /etc/passwd | head -n 5

echo "Hello <NAME><NIM>" > percobaan.txt
ls -l percobaan.txt
chmod 600 percobaan.txt
ls -l percobaan.txt


```

---

## Hasil Eksekusi
Sertakan screenshot hasil percobaan atau diagram:
![Screenshot hasil](./screenshots/Screenshot%202025-10-21%20203337.png)

---

## Analisis
- Jelaskan makna hasil percobaan.  
- Hubungkan hasil dengan teori (fungsi kernel, system call, arsitektur OS).  

Perintah seperti chmod dan chown di sistem Unix/Linux berinteraksi langsung dengan komponen inti sistem operasi, yang dapat dihubungkan dengan teori arsitektur OS sebagai berikut:

Fungsi Kernel: Kernel bertindak sebagai inti OS yang mengelola sumber daya hardware dan software. Dalam konteks chmod dan chown, kernel menangani manajemen file system, termasuk penyimpanan dan pengendalian akses file. Kernel menyimpan metadata file (seperti permissions dan ownership) dalam struktur data seperti inode di file system ext4 Linux. Ketika chmod dijalankan, kernel memverifikasi hak akses pengguna (misalnya, apakah owner dapat mengubah permissions) dan memperbarui inode, memastikan keamanan dan integritas data—sesuai dengan prinsip isolasi proses dalam arsitektur OS monolitik atau mikrokernel.

System Call: Perintah chmod dan chown adalah wrapper shell yang memanggil system calls kernel, seperti chmod() dan chown() (didefinisikan dalam POSIX standard). System calls ini mentransisikan dari mode user space ke kernel space melalui interrupt atau syscall interface (misalnya, via glibc di Linux). Contoh: chmod 755 file.txt memanggil syscall chmod() yang mengubah mode file di kernel, memungkinkan kontrol akses tanpa akses langsung ke hardware. Ini mendukung teori layered architecture OS, di mana aplikasi (user space) berkomunikasi dengan kernel melalui API terstruktur untuk mencegah konflik sumber daya.

Arsitektur OS: Dalam arsitektur Unix-like (seperti Linux), permissions adalah bagian dari model discretionary access control (DAC), di mana owner mengontrol akses berdasarkan rwx untuk owner/group/others. Kernel mengimplementasikan ini melalui file system layer, yang terintegrasi dengan scheduler dan memory management untuk efisiensi. Ini berbeda dari arsitektur Windows (NT kernel), yang menggunakan mandatory access control (MAC) dengan ACL, tetapi konsep dasar kontrol akses tetap serupa—kernel sebagai arbiter utama.


- Apa perbedaan hasil di lingkungan OS berbeda (Linux vs Windows)?  

Hasil perintah seperti chmod dan chown (termasuk interpretasi permissions seperti rwxr-xr--) bervariasi karena perbedaan arsitektur dan model keamanan OS, meskipun keduanya bertujuan untuk kontrol akses file. Berikut perbedaannya:

Linux (Unix-like):

chmod dan chown adalah perintah native yang langsung mengubah mode file (permissions) dan ownership melalui kernel. Kode rwxr-xr-- (oktal 754) berlaku universal, dengan kernel menerapkan aturan DAC sederhana. Hasilnya konsisten di semua distribusi Linux (misalnya, Ubuntu atau CentOS), karena didasarkan pada standar POSIX. Tidak ada GUI bawaan untuk ini; penggunaan melalui terminal, dan perubahan segera berlaku tanpa restart.
Kelebihan: Sederhana, cepat, dan efisien untuk scripting/otomasi. Kekurangan: Permissions kurang granular (hanya rwx untuk tiga kategori), sehingga kurang cocok untuk skenario enterprise kompleks.
Windows (NT-based):

Tidak ada perintah chmod atau chown langsung; Windows menggunakan Access Control Lists (ACL) yang lebih canggih melalui perintah seperti icacls (misalnya, icacls file.txt /grant user:(R,W) untuk read/write). Kode seperti rwxr-xr-- tidak berlaku; permissions dikelola via GUI (Properties > Security) atau command line dengan granularitas tinggi (misalnya, deny/allow spesifik untuk pengguna tertentu). chown analog dengan takeown atau icacls /setowner.
Kelebihan: ACL lebih fleksibel (misalnya, kontrol per-user tanpa grup), mendukung inheritance, dan terintegrasi dengan Active Directory. Kekurangan: Lebih kompleks, memerlukan hak admin untuk perubahan besar, dan hasil bisa bervariasi berdasarkan versi (misalnya, Windows 10 vs Server). Perubahan mungkin memerlukan restart layanan atau logoff untuk efek penuh.
Secara keseluruhan, Linux lebih cocok untuk kontrol akses sederhana dan konsisten di server, sedangkan Windows lebih baik untuk lingkungan desktop/enterprise dengan kebutuhan keamanan lanjutan, meskipun keduanya mengandalkan kernel untuk enforcement. Jika dijalankan di Windows via WSL (Windows Subsystem for Linux), hasilnya mirip Linux karena layer emulasi.

---

## Kesimpulan
Tuliskan 2–3 poin kesimpulan dari praktikum ini.

Praktikum ini menunjukkan bagaimana system call digunakan oleh program untuk berinteraksi dengan kernel. Dengan menggunakan perintah strace, kita dapat memantau system call yang dilakukan oleh program, seperti open, read, write, dan close. Hasilnya membantu memahami cara kerja sistem operasi dalam mengelola sumber daya dan menangani permintaan dari program.

Perintah dmesg digunakan untuk memantau log kernel, yang dapat membantu dalam debugging dan memahami kejadian sistem. Dengan demikian, praktikum ini memberikan wawasan tentang interaksi antara program dan kernel, serta cara memantau dan menganalisis system call.

---

## Quiz
1. [Pertanyaan 1]  
   **Jawaban:**  
   Perintah chmod (change mode) digunakan di sistem operasi Unix/Linux untuk mengubah izin akses (permission) pada file atau direktori. Ini memungkinkan pengguna untuk mengontrol siapa yang dapat membaca (read), menulis (write), atau mengeksekusi (execute) file tersebut. Misalnya, chmod 755 file.txt mengubah izin file menjadi readable dan executable oleh semua, tapi hanya writable oleh owner. Perintah ini penting untuk keamanan, karena mencegah akses tidak sah—seperti yang didefinisikan dalam standar POSIX untuk sistem file Unix.


2. [Pertanyaan 2]  
   **Jawaban:**  

   Arti Kode Permission rwxr-xr--
Kode permission rwxr-xr-- adalah representasi simbolik dari izin akses file, yang setara dengan nilai oktal 754. Ini dipecah berdasarkan tiga kategori pengguna:

Owner (rwx): Read (r), write (w), execute (x) — nilai 7 (4+2+1). Owner dapat membaca, menulis, dan mengeksekusi file.
Group (r-x): Read (r), execute (x), tanpa write — nilai 5 (4+0+1). Anggota grup dapat membaca dan mengeksekusi, tapi tidak menulis.
Others (r--): Read (r) saja — nilai 4 (4+0+0). Pengguna lain hanya dapat membaca file.
Ini berarti file tersebut dapat dijalankan oleh owner dan grup, tapi hanya dibaca oleh orang lain. Kode ini umum digunakan untuk skrip atau program yang perlu dieksekusi oleh grup tertentu, seperti dalam konfigurasi server web (misalnya, file CGI di Apache).


3. [Pertanyaan 3]  
   **Jawaban:**  

   Perbedaan antara chown dan chmod
chown (change owner): Mengubah kepemilikan file, yaitu siapa yang menjadi owner (pengguna) dan/atau grup pemiliknya. Contoh: chown user:group file.txt menyerahkan file ke pengguna "user" dan grup "group". Ini memengaruhi siapa yang dapat mengakses file berdasarkan ownership, bukan izin spesifik.
chmod: Mengubah izin akses (permission) file, seperti read/write/execute, tanpa mengubah siapa pemiliknya. Contoh: chmod 644 file.txt mengatur izin tanpa mempengaruhi ownership.
Perbedaannya: chown mengatur kepemilikan (ownership), sedangkan chmod mengatur izin akses (permissions). Keduanya sering digunakan bersama untuk kontrol akses penuh, seperti dalam administrasi sistem Linux, di mana ownership menentukan kontrol utama dan permissions menentukan tingkat akses.

---

## Refleksi Diri
Tuliskan secara singkat:
- Apa bagian yang paling menantang minggu ini?  
- Bagaimana cara Anda mengatasinya?  

---

**Credit:**  
_Template laporan praktikum Sistem Operasi (SO-202501) – Universitas Putra Bangsa_
