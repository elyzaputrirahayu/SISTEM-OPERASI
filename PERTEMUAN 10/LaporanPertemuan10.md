## LAPORAN PERTEMUAN 10
##
<h4> Nama    : Elyza Putri Rahayu <h4>
<h4> NIM     : 254107020035  <h4>
<h4> Kelas   : TI - 1G  <h4>

##

##### Praktikum 10.1 Melihat Penggunaan Memori

<img src="Screenshot 2026-04-29 122026.png" width="50%">

- mkdir -p ~/praktikum-os/week10-memory : Membuat folder untuk menyimpan semua hasil praktikum biar rapi.
- cd ~/praktikum-os/week10-memory : Masuk ke folder yang tadi dibuat supaya semua kerjaan ada di situ.
- free -h : Melihat penggunaan RAM dan swap dalam bentuk yang mudah dibaca (human readable).
- cat /proc/meminfo | head -n 20 : Menampilkan informasi detail memori dari sistem Linux (20 baris pertama saja).


##### Praktikum 10.2 Mengamati Aktivitas Paging

<img src="Screenshot 2026-04-29 124524.png" width="50%">

- vmstat 1 5 Perintah ini digunakan untuk melihat aktivitas memori virtual secara real-time.
Angka 1 artinya data diperbarui setiap 1 detik, dan 5 artinya diambil sebanyak 5 kali (5 baris output).
- si (swap in) → data dari disk ke RAM
- so (swap out) → data dari RAM ke disk
- hasilnya si = 0 dan so = 0. Artinya RAM masih cukup, tidak ada penggunaan swap

##### Praktikum 10.3 Membuat dan Mengonfigurasi Swap File

<img src="Screenshot 2026-04-29 132645.png" width="50%">

- sudo fallocate -l 512M /swapfile-week10 : Membuat file kosong berukuran 512 MB yang akan digunakan sebagai swap.
- sudo chmod 600 /swapfile-week10 : Mengamankan file swap supaya hanya root yang bisa baca/tulis (penting karena berisi data memori).
- sudo mkswap /swapfile-week10 : Mengubah file biasa menjadi format khusus yang bisa digunakan sebagai swap.
- sudo swapon /swapfile-week10 : Mengaktifkan swap agar mulai digunakan oleh sistem.
- swapon --show
  free -h
  Memastikan swap sudah aktif dan melihat total swap bertambah.
- cat /proc/sys/vm/swappiness : Melihat seberapa sering sistem menggunakan swap (biasanya default 60).
- sudo sysctl vm.swappiness=10 : Mengatur agar sistem lebih jarang menggunakan swap (lebih mengutamakan RAM).
- cat /proc/sys/vm/swappiness : Memastikan nilai swappiness sudah berubah menjadi 10.
- sudo swapoff /swapfile-week10
  sudo rm /swapfile-week10
  Mematikan swap dan menghapus file agar sistem kembali seperti semula.

##### Praktikum 10.4 Monitoring Memory

<img src="Screenshot 2026-05-01 124157.png" width="50%"> 

<img src="Screenshot 2026-05-01 124221.png" width="50%"> 

- Proses paling atas adalah yang paling banyak menggunakan memori.
- Kolom %MEM menunjukkan persentase RAM yang dipakai.
- Kolom RSS menunjukkan jumlah RAM yang benar-benar digunakan (dalam KB).
- Untuk ubah ke MB → RSS ÷ 1024
- VSZ lebih besar dari RSS karena VSZ adalah total memori virtual (termasuk yang belum dipakai di RAM).
- Hasil di ps dan top biasanya mirip, tapi bisa berubah karena kondisi sistem selalu berjalan.

##### Praktikum 10.5 Script Monitor Memori

<img src="Screenshot 2026-05-01 130738.png" width="50%">

Script ini digunakan untuk:
- Menampilkan info memori (free -h)
- Menghitung persentase memori tersedia
- Memberi peringatan jika di bawah batas (THRESHOLD)
- Menampilkan 5 proses yang paling banyak pakai RAM

<img src="Screenshot 2026-05-01 130834.png" width="50%">

Pada gambar tersebut Memori / RAM 1,9 GB dan SWAP atau harddisk nya 2 GB

##### Praktikum 10.6 Mengamati System Call dengan strace

<img src="Screenshot 2026-05-02 193138.png" width="50%">

strace ls 2>&1 | head -n 30
Deskripsi:
Perintah ini digunakan untuk melihat 30 baris pertama system call yang dilakukan oleh perintah ls.
strace akan menampilkan semua interaksi antara program dan kernel, sedangkan 2>&1 digunakan untuk menggabungkan output error ke output utama agar bisa ditampilkan oleh head.

hasil dari screenshot tersebut :
1. openat(...) = 3
Artinya:
- Sistem mencoba membuka file
- Berhasil, dikasih nomor file (fd) = 3
2. read(3, ..., 832) = 832
Artinya:
- Membaca isi file dari fd 3
- Berhasil baca 832 byte
3. close(3) = 0
Artinya:
- Menutup file
- 0 = sukses
4. mmap(...)
Artinya:
- Memetakan file ke memori (biar cepat diakses)
5. access(...) = -1 ENOENT
Artinya:
- Coba akses file
- Tapi file tidak ada

<img src="Screenshot 2026-05-02 193209.png" width="50%">

strace -c ls
Deskripsi:
Perintah ini menampilkan ringkasan statistik system call dari perintah ls, seperti jumlah pemanggilan, waktu eksekusi, dan error yang terjadi.

<img src="Screenshot 2026-05-02 193259.png" width="50%">

strace -c ls /etc 2>&1 | tail -n 5
Deskripsi:
Perintah ini digunakan untuk melihat ringkasan system call saat ls dijalankan pada direktori /etc, lalu hanya menampilkan bagian akhir hasilnya menggunakan tail.

##### Studi Kasus 10.1 Server Lambat karena Memori

<img src="Screenshot 2026-05-02 214536.png" width="50%">

free -h

Deskripsi:
Perintah ini digunakan untuk melihat kondisi RAM dan swap secara keseluruhan, termasuk total, digunakan, dan memori yang masih tersedia.

<img src="Screenshot 2026-05-02 214600.png" width="50%">

top

Deskripsi:
Perintah ini digunakan untuk memantau penggunaan CPU dan memori secara langsung (real-time).
Tekan M untuk mengurutkan berdasarkan penggunaan memori, dan q untuk keluar.

Analisis:
1. Apakah nilai available sangat kecil (misalnya di bawah 200 MB pada server
dengan RAM 2 GB)? Jika ya, server kemungkinan kekurangan memori.
jawab : Jika nilai available sangat kecil (misalnya di bawah 200 MB pada RAM 2 GB), maka sistem mengalami kekurangan memori karena hampir seluruh RAM telah digunakan oleh proses.

2. Apakah kolom used pada baris Swap lebih dari 0? Jika ya, kernel sedang
menggunakan swap, yang berarti performa menurun.
jawab : Jika pada baris Swap nilai used lebih dari 0, maka sistem sudah menggunakan swap. Hal ini menandakan RAM tidak cukup sehingga sebagian data dipindahkan ke disk, yang menyebabkan penurunan performa.

3. Di tampilan top, proses apa yang memiliki %MEM terbesar? Proses tersebut
menjadi kandidat utama penyebab lambatnya server.
jawab : Pada tampilan top, proses dengan nilai %MEM terbesar merupakan proses yang paling banyak menggunakan RAM dan menjadi kandidat utama penyebab lambatnya sistem.

##### Studi Kasus 10.2 Gagal Akses File

<img src="Screenshot 2026-05-03 101623.png" width="50%">

Membuat folder praktikum, lalu membuat file konfigurasi app.conf dan memastikan file bisa dibaca.

<img src="Screenshot 2026-05-03 101708.png" width="50%">

Menghapus semua izin akses file (baca, tulis, eksekusi), sehingga file tidak bisa diakses oleh siapa pun.

<img src="Screenshot 2026-05-03 101755.png" width="50%">

Mengembalikan izin file agar bisa dibaca kembali.

Analisis:
1. Mengapa cat menghasilkan Permission denied setelah chmod 000? System
call apa yang gagal?
jawab : Pesan Permission denied muncul karena file tidak memiliki izin baca setelah dilakukan chmod 000.
System call yang gagal adalah openat(), karena kernel menolak akses ke file tersebut.

2. Apa perbedaan pesan error Permission denied vs No such file or directory?
Coba rm app.conf lalu cat app.conf untuk melihat perbedaannya.
jawab : 
<img src="Screenshot 2026-05-03 101924.png" width="50%">

Perbedaan error:
- Permission denied → file ada, tapi tidak boleh diakses
- No such file or directory → file memang tidak ada

3. Permission 644 berarti apa untuk owner, group, dan others?
jawab : 
Arti permission 644:
- Owner (6) → read + write
- Group (4) → read saja
- Others (4) → read saja

#### Tugas Praktikum
##### Tugas 10.1 Audit Penggunaan Memori Sistem

mkdir -p ~/praktikum-os/week10-memory
cd ~/praktikum-os/week10-memory

Perintah ini digunakan untuk membuat direktori kerja praktikum jika belum ada (mkdir -p), lalu berpindah ke direktori tersebut (cd) agar semua file tersimpan rapi di satu tempat.

nano memory-audit.sh

Perintah ini digunakan untuk membuat dan membuka file script bernama memory-audit.sh menggunakan editor nano.

<img src="Screenshot 2026-05-03 134621.png" width="50%">

Script ini digunakan untuk mengambil informasi kondisi memori sistem menggunakan free -h dan /proc/meminfo, lalu menyimpannya ke file laporan dan menampilkannya di terminal.

<img src="Screenshot 2026-05-03 135103.png" width="50%">

chmod +x memory-audit.sh
Memberikan izin agar file script bisa dijalankan sebagai program.

bash memory-audit.sh
Menjalankan script untuk menghasilkan laporan kondisi memori sistem. Dan hasilnya seperti gambar dibawah ini
<img src="Screenshot 2026-05-03 135133.png" width="50%">

Analisis
1. Hitung persentase memori tersedia (available / total × 100%). Apakah
sistem dalam kondisi normal?
jawab : Persentase memori tersedia sekitar 84%, yang berarti kondisi memori sangat aman dan jauh dari kekurangan memori.
2. Mengapa buff/cache tidak dihitung sebagai memori yang terpakai dari sudut
pandang ketersediaan untuk aplikasi?
jawab : Nilai buff/cache = 336 MiB menunjukkan bahwa sebagian memori digunakan oleh sistem sebagai cache dan buffer. buff/cache tidak dianggap sebagai memori “terpakai penuh” karena masih bisa digunakan kembali oleh aplikasi.
3. Dari /proc/meminfo, apakah SwapTotal lebih besar dari 0? Berapa nilai
SwapFree?
jawab : Dari output:

SwapTotal = 2.0 GiB
SwapUsed = 0 B
SwapFree = 2.0 GiB

- Swap belum digunakan sama sekali
- Artinya RAM masih sangat cukup
- Sistem tidak mengalami tekanan memori

##### Tugas 10.2 Identifikasi Proses dengan Memori Tertinggi

<img src="Screenshot 2026-05-03 190849.png" width="50%">

Analisis
1. Proses apa di urutan pertama? Catat nilai %MEM dan RSS.
jawab : Dari output:
Proses: /usr/lib/snapd/snapd
%MEM: 2.1%
RSS: 42720 KB
2. Konversikan RSS ke MB (bagi 1024). Apakah wajar?
jawab : Penggunaan memori sekitar 41.7 MB, ini sangat wajar, karena proses snapd adalah layanan sistem untuk manajemen paket Snap yang memang berjalan di background.
3. Jumlahkan %MEM dari 5 proses teratas. Berapa persen RAM yang mereka
gunakan bersama?
jawab : Ambil 5 teratas:

2.1%
1.3%
1.0%
0.9%
0.7%

Total:

2.1+1.3+1.0+0.9+0.7=6.0%

Kesimpulan:
Kelima proses tersebut hanya menggunakan sekitar 6% dari total RAM, yang berarti penggunaan memori masih sangat ringan.

##### Tugas 10.3 Membuat dan Memverifikasi Swap File
<img src="Screenshot 2026-05-03 194324.png" width="50%">
<img src="Screenshot 2026-05-03 194507.png" width="50%">
<img src="Screenshot 2026-05-03 194540.png" width="50%">
<img src="Screenshot 2026-05-03 194639.png" width="50%">

Analisis
1. Identifikasi kolom NAME, TYPE, SIZE, dan USED pada output swapon –show.
jawab : 
Output swapon --show menampilkan beberapa kolom penting:

NAME → lokasi file swap yang digunakan
Contoh: /swapfile-tugas-week10
TYPE → jenis swap
Biasanya file (karena kita pakai file, bukan partisi)
SIZE → ukuran total swap
Pada tugas ini sebesar 256 MB
USED → jumlah swap yang sedang digunakan
Jika bernilai 0B, berarti swap belum dipakai
2. Apakah nilai total pada baris Swap di free -h bertambah 256 MB?
jawab : Ya, nilai pada baris Swap di free -h bertambah 256 MB, menandakan swap file berhasil dibuat dan diaktifkan.
3. Mengapa permission 600 penting? Apa risiko jika diatur ke 644?
jawab :
Permission 600 berarti:
- hanya root yang bisa membaca dan menulis file
- user lain tidak punya akses sama sekali
Mengapa penting?
Swap file bisa berisi:
- data sementara dari aplikasi
- informasi sensitif dari memori (password, token, dll)
Jika permission diatur ke 644:
- user lain bisa membaca file swap
- berisiko terjadi kebocoran data sensitif

##### Tugas 10.4 Analisis System Call dengan strace
<img src="Screenshot 2026-05-03 200649.png" width="50%">
<img src="Screenshot 2026-05-03 200734.png" width="50%">
<img src="Screenshot 2026-05-03 200930.png" width="50%">

Analisis
1. Sebutkan minimal 5 system call dari strace-summary.txt beserta fungsi singkatnya.
jawab : 
- read
- write
- close
- mmap
- mprotect

2. System call mana yang paling sering dipanggil? Mengapa?
jawab : write, Perintah ls digunakan untuk menampilkan daftar file ke layar (terminal).
Setiap kali ls menampilkan nama file atau output lainnya, sistem akan memanggil system call write() untuk mengirim data tersebut ke standar output (stdout).
Semakin banyak file yang ditampilkan, maka:
semakin banyak pemanggilan write(), karena setiap baris output harus ditulis ke terminal

3. Apakah ada errors lebih dari 0? Apakah program tetap berjalan normal meskipun ada kegagalan tersebut?
jawab : ada, access gagal 2x, statfs gagal 2x, arch_prctl gagal 1x, dan program tetap berjalan normal meskipun ada kegagalan

##### Tugas 10.5 Studi Kasus Diagnosa Server Lambat
<img src="Screenshot 2026-05-04 163622.png" width="50%">
<img src="Screenshot 2026-05-04 165152.png" width="50%">

Analisis
1. Jelaskan peran masing-masing fungsi: cek_memori, cek_swap, cek_proses, cek_paging, dan ringkasan. Mengapa diagnosa dipecah menjadi fungsi terpisah?
jawab : 
cek_memori → mengecek kondisi RAM dan menghitung persentase memori tersedia
cek_swap → melihat apakah swap digunakan atau tidak
cek_proses → menampilkan proses yang paling banyak menggunakan memori
cek_paging → memantau aktivitas paging (si/so) menggunakan vmstat
ringkasan → memberikan kesimpulan akhir kondisi sistem

Alasan dipisah fungsi:
Agar script lebih rapi, mudah dibaca, dan setiap bagian memiliki tugas spesifik sehingga mudah diperbaiki atau dikembangkan.

2. Berdasarkan bagian RINGKASAN, apakah kondisi sistem normal atau kritis? Jelaskan berdasarkan nilai threshold yang digunakan script.
jawab : 
Script menggunakan threshold:
- jika memori tersedia < 20% → KRITIS
- jika ≥ 20% → normal
Berdasarkan hasil sebelumnya (±84%), maka kondisi sistem NORMAL

3. Mengapa script menggunakan tee "$LAPORAN" bukan redirection biasa > "$LAPORAN"? Apa keuntungannya?
jawab : tee digunakan agar output tampil di terminal, sekaligus disimpan ke file laporan
Jika hanya pakai >:
output tidak tampil di layar
Keuntungan:
Bisa melihat hasil langsung dan tetap menyimpan laporan.

4. Dari output cek_paging, apakah ada aktivitas si atau so? Jika ada, apa implikasinya terhadap performa server?
jawab :
Jika si = 0 dan so = 0 → tidak ada aktivitas swap → kondisi normal
Jika si/so > 0 terus-menerus → sistem kekurangan RAM
Kesimpulan:
Jika tidak ada aktivitas paging, maka performa server masih optimal.