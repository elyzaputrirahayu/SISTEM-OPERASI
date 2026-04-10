## LAPORAN PERTEMUAN 7
##
<h4> Nama    : Elyza Putri Rahayu <h4>
<h4> NIM     : 254107020035  <h4>
<h4> Kelas   : TI - 1G  <h4>

##

### Tugas Praktikum
#### Tugas Praktikum 1 — Toolkit Bash Administrator Pribadi
##### Konteks riil: seorang administrator sering mengulang perintah yang sama setiap hari. Agar pekerjaan lebih efisien dan konsisten, ia perlu memiliki toolkit Bash pribadi yang otomatis aktif setiap login.

1. Menambahkan konfigurasi pada .bashrc untuk :
- menambahkan direktori bin pribadi ke PATH,
- membuat minimal 2 alias yang membantu kerja harian,
- membuat minimal 1 fungsi shell yang berguna untuk administrasi.

<img src="Screenshot 2026-04-09 105629.png" width="50%">

FIle .bashrc digunakan untuk menyimpan konfigurasi shell. Ditambahkan PATH untuk direktori ~/bin, alias untuk mempercepat perintah (ll, gs), fungsi

2. Mengaktifkan konfigurasi menggunakan perintah source ~/.bashrc

3. Membuat direktori bin pribadi menggunakan perintah mkdir -p ~/bin
Membuat script sederhana menggunakan perintah nano ~/bin/ringkasan, lalu menggunakan perintah chmod +x ~/bin/ringkasan untuk menyimpan dan mengasih kan izin

<img src="Screenshot 2026-04-09 110336.png" width="50%">

4. Uji dari direktori yang berbeda untuk memastikan script dapat dipanggil tanpa menuliskan path lengkap.

<img src="Screenshot 2026-04-09 110404.png" width="50%">

4. Cek PATH

<img src="Screenshot 2026-04-09 110442.png" width="50%">

5. Cek alias, fungsi, dan script

<img src="Screenshot 2026-04-09 110617.png" width="50%">

6. Menyimpan bukti pengujian ke file toolkit-bash-report.txt.

<img src="Screenshot 2026-04-09 111224.png" width="50%">

untuk melihat hasilnya :

<img src="Screenshot 2026-04-09 111305.png" width="50%">

#### Tugas Praktikum 2 — Audit File Konfigurasi dan Logging Aman
##### Konteks riil: saat troubleshooting, administrator sering perlu menginventarisasi file konfigurasi dan memisahkan output normal dari pesan error.

<img src="Screenshot 2026-04-10 104632.png" width="50%">

1. Membuat file laporan bernama audit-konfigurasi-$(date +%F).txt.

Menggunakan command substitution $(date +%F) untuk membuat nama file otomatis sesuai tanggal.

<img src="Screenshot 2026-04-10 110920.png" width="50%">

2. Mencari file *.conf di dalam /etc dan simpan hasilnya ke file laporan. 
   -> → menyimpan hasil normal (stdout) ke file laporan
   -2> → menyimpan error (stderr) ke file terpisah
find digunakan untuk mencari file konfigurasi

<img src="Screenshot 2026-04-10 111010.png" width="50%">

3. Menghitung jumlah file konfigurasi
wc -l menghitung jumlah baris (jumlah file)
-< membaca dari file
->> menambahkan hasil ke laporan

<img src="Screenshot 2026-04-10 111111.png" width="50%">

4. Menampilkan laporan + menyimpan pakai tee
| → pipeline (menghubungkan perintah)
tee → menampilkan ke layar dan menyimpan ke file

Pemisahan stdout dan stderr penting untuk membedakan hasil normal dan error.
Hal ini membantu analisis sistem tanpa terganggu pesan error.
Administrator dapat fokus pada hasil utama dan mengecek error secara terpisah.

#### Tugas Praktikum 3 — Mini Health Check Harian Server
##### Konteks riil: administrator perlu membuat pemeriksaan cepat (health check) untuk mengetahui kondisi dasar server sebelum dan sesudah maintenance.

<img src="Screenshot 2026-04-10 122624.png" width="50%">

1. Membuat script di folder bin

<img src="Screenshot 2026-04-10 123517.png" width="50%">

2. Mengisi script

<img src="Screenshot 2026-04-10 123820.png" width="50%">

penjelasan tiap bagian script :
a. Shebang (#!/bin/bash)
   Menentukan bahwa script dijalankan menggunakan shell Bash.
b. Variabel LOGFILE 
   LOGFILE="$HOME/healthcheck-$(date +%F).log"
   Digunakan untuk menyimpan nama file log secara otomatis berdasarkan tanggal saat script dijalankan.
c. Informasi Sistem Dasar
   date, hostname, $USER, $SHELL
   Menampilkan:
   - tanggal dan waktu saat ini
   - nama host komputer
   - user yang sedang aktif
   - shell yang digunakan

d. Uptime
   Menampilkan lama sistem telah berjalan sejak terakhir dinyalakan.
e. Penggunaan Memori
   free -h
   Menampilkan penggunaan RAM dalam format yang mudah dibaca (human-readable).
f. Penggunaan Disk Root
   df -h /
   Menampilkan penggunaan ruang penyimpanan pada direktori root (/).
g. History Command
   history | tail -n 10
   Menampilkan 10 perintah terakhir yang dijalankan user, menggunakan pipeline (|).
h. Tee (saat eksekusi)
   Digunakan untuk menampilkan output ke terminal sekaligus menyimpannya ke file log.
i. Error Handling
   Digunakan untuk mengecek apakah perintah sebelumnya berhasil dijalankan atau tidak.

3. Memberi izin executable

<img src="Screenshot 2026-04-10 123922.png" width="50%">

4. Memastikan PATH sudah ada ~/bin

<img src="Screenshot 2026-04-10 124042.png" width="50%">

5. Menyimpan dan menjalankan log memakai tee

<img src="Screenshot 2026-04-10 124934.png" width="50%">

6. Mengecek status exit

tanda 0 berarti sukses

#### Tugas Praktikum 4 — Penanganan File dengan Nama Kompleks dan Arsip Aman
##### Konteks riil: file hasil backup, ekspor, atau laporan sering memiliki nama yang mengandung spasi atau karakter khusus. Administrator harus tetap dapat memproses file-file tersebut tanpa salah target.

<img src="Screenshot 2026-04-10 134209.png" width="50%">

1. Membuat file dengan nama kompleks
"data laporan.txt" → contoh file dengan spasi
"config[1].conf" → contoh karakter khusus
file1.txt file2.txt file3.txt → untuk wildcard

<img src="Screenshot 2026-04-10 134551.png" width="50%">

2. cat data laporan.txt, Tanpa quoting (error), dianggap 2 file → error
   cat "data laporan.txt", berhasil
   cat data\ laporan.txt, Quoting dan escaping digunakan agar shell tidak salah membaca nama file.

<img src="Screenshot 2026-04-10 134744.png" width="50%">

3. Preview wildcard
hanya menampilkan file yang cocok, digunakan untuk memastikan file yang akan diproses sudah benar

<img src="Screenshot 2026-04-10 135016.png" width="50%">

4. Buat direktori backup

<img src="Screenshot 2026-04-10 135928.png" width="50%">

5. Menyalin file ke backup
Menggunakan variabel path dan quoting untuk memastikan file tersalin dengan aman.

<img src="Screenshot 2026-04-10 140845.png" width="50%">

6. Buat Arsip

<img src="Screenshot 2026-04-10 141032.png" width="50%">

7. Menyimpan ke history

output : 
File awal 
<img src="Screenshot 2026-04-10 140016-1.png" width="50%">

File Backup
<img src="Screenshot 2026-04-10 140039-1.png" width="50%">

Arsip 
<img src="Screenshot 2026-04-10 140845.png" width="50%">

History 
<img src="Screenshot 2026-04-10 141032.png" width="50%">