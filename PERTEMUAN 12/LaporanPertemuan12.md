## LAPORAN PERTEMUAN 10
##
<h4> Nama    : Elyza Putri Rahayu <h4>
<h4> NIM     : 254107020035  <h4>
<h4> Kelas   : TI - 1G  <h4>

##

#### Praktek 10.1: Amati Layanan Aktif Saat Boot
<img src="Screenshot 2026-05-15 225500.png" width="50%">
<img src="Screenshot 2026-05-15 225616.png" width="50%">
<img src="Screenshot 2026-05-15 225707.png" width="50%">

Tantangan 10.1 :
Identifikasi tiga layanan dengan waktu inisialisasi terlama menggunakan systemd-analyze blame. 
Gunakan pipeline dari Bab 3 (| sort -rh | head -3) untuk mempercepat pencariannya. 
Untuk setiap layanan, cari tahu fungsinya dengan systemctl cat nama-layanan. Tuliskan nama layanan, waktu inisialisasinya, 
dan penjelasan singkat fungsinya.
jawab :
<img src="Screenshot 2026-05-15 230516-1.png" width="50%">

1. snap.lxd.activate.service
Waktu inisialisasi: 5.052 detik
Fungsi: layanan untuk mengaktifkan dan menjalankan LXD yang digunakan dalam manajemen container Linux berbasis Snap.
2. snapd.seeded.service
Waktu inisialisasi: 4.579 detik
Fungsi: layanan yang memastikan paket Snap bawaan sistem telah terpasang dan dikonfigurasi dengan benar saat boot.
3. snapd.service
Waktu inisialisasi: 4.484 detik
Fungsi: layanan utama Snap daemon yang bertugas mengelola instalasi, pembaruan, dan menjalankan aplikasi berbasis Snap.

<img src="Screenshot 2026-05-15 230605-1.png" width="50%">
<img src="Screenshot 2026-05-15 230914-1.png" width="50%">
<img src="Screenshot 2026-05-15 231022-1.png" width="50%">

#### Praktek 10.2: Kelola Layanan SSH
<img src="Screenshot 2026-05-15 231935.png" width="50%">
<img src="Screenshot 2026-05-15 232011.png" width="50%">
<img src="Screenshot 2026-05-15 232058.png" width="50%">
<img src="Screenshot 2026-05-15 232150.png" width="50%">
<img src="Screenshot 2026-05-15 232233.png" width="50%">
<img src="Screenshot 2026-05-15 232344.png" width="50%">

Tantangan 10.2 :
Buat skrip Bash (referensi Bab 7) bernama cek-layanan.sh yang memeriksa status daftar layanan dari sebuah berkas teks. 
Berkas teks daftar-layanan.txt berisi satu nama layanan per baris (isi minimal: ssh, cron, rsyslog). 
Skrip membaca setiap nama layanan, memeriksa statusnya dengan systemctl is-active, 
lalu menulis laporan ke berkas laporan-layanan.log dengan format: [TANGGAL] nama-layanan: ACTIVE/INACTIVE. 
Gunakan date untuk mendapatkan tanggal.

jawab :
1. nano daftar-layanan.txt
Membuat file berisi daftar layanan yang akan dicek.

2. 
<img src="Screenshot 2026-05-15 233734-1.png" width="50%">

Menambahkan nama layanan satu per satu ke dalam file.

3. nano cek-layanan.sh
Membuat script untuk mengecek status layanan otomatis.
<img src="Screenshot 2026-05-15 234152-1.png" width="50%">
Script membaca daftar layanan, mengecek statusnya menggunakan systemctl is-active, lalu menyimpan hasil ke file log.

4. 
<img src="Screenshot 2026-05-15 234316-1.png" width="50%">

- chmod +x cek-layanan.sh
Memberi izin agar script dapat dijalankan.
- bash cek-layanan.sh
Menjalankan script pengecekan layanan.
- cat laporan-layanan.log
Menampilkan isi laporan status layanan.
Hasilnya :
[Fri May 15 04:42:41 PM UTC 2026] ssh: active 
[Fri May 15 04:42:41 PM UTC 2026] cron: active
[Fri May 15 04:42:41 PM UTC 2026] rsyslog: active

#### Praktek 10.3: Buat Layanan Sederhana dari Skrip Bash
<img src="Screenshot 2026-05-17 175823.png" width="50%">
<img src="Screenshot 2026-05-17 180117.png" width="50%">
<img src="Screenshot 2026-05-17 180355.png" width="50%">
<img src="Screenshot 2026-05-17 180537.png" width="50%">
<img src="Screenshot 2026-05-17 181024.png" width="50%">
<img src="Screenshot 2026-05-17 181417.png" width="50%">

Tantangan 10.3 :
Modifikasi berkas unit demo-web.service sebelum menghapusnya: tambahkan RestartSec=10s agar sistemmenunggu 10 detik sebelum mencoba restart, 
dan tambahkan Environment="PORT=9091" lalu ubah ExecStart agar menggunakan variabel tersebut. 
Aktifkan layanan dengan enable dan WantedBy=multi-user.target, lalu uji apakah layanan aktif setelah systemctl daemon-reload. 
Dokumentasikan perbedaan perilaku dibanding versi sebelumnya.

<img src="Screenshot 2026-05-17 193604.png" width="50%">
<img src="Screenshot 2026-05-17 194024.png" width="50%">

Versi sebelumnya menggunakan RestartSec=3s, sehingga service langsung restart setelah gagal. 
Pada versi baru, service menunggu 10 detik sebelum restart sehingga proses restart lebih lambat dan stabil. 
Selain itu, port layanan sebelumnya ditulis langsung di ExecStart, sedangkan versi baru 
menggunakan variabel environment PORT=9091 sehingga konfigurasi port menjadi lebih fleksibel dan mudah diubah.

#### Praktek 10.4 : Filter dan Analisis Log Layanan
<img src="Screenshot 2026-05-17 201642.png" width="50%">
<img src="Screenshot 2026-05-17 202024.png" width="50%">

Tantangan 10.4 :
<img src="Screenshot 2026-05-17 202757-1.png" width="50%">
Perintah yang digunakan untuk mengekstrak log error SSH 24 jam terakhir adalah:
journalctl -u ssh -p err --since "24 hours ago" --no-pager > error-ssh-24jam.txt
Perintah untuk menghitung jumlah error:
wc -l error-ssh-24jam.txt
Perintah untuk menampilkan 10 pesan error yang paling sering muncul:
sort error-ssh-24jam.txt | uniq -c | sort -rn | head -10

Praktikum ini menggunakan journalctl untuk memfilter, memantau, dan menganalisis log layanan sistem. 
Pipeline Linux seperti sort, uniq, dan wc membantu proses analisis log menjadi lebih cepat dan efisien.

#### Praktek 10.5: Konfigurasi SSH Server
<img src="Screenshot 2026-05-17 204100.png" width="50%">
<img src="Screenshot 2026-05-17 204601.png" width="50%">
<img src="Screenshot 2026-05-17 205017.png" width="50%">
<img src="Screenshot 2026-05-17 205041.png" width="50%">

Tantangan 10.5 :
Ubah konfigurasi SSH untuk menambahkan dua pengaturan keamanan: PermitRootLogin no (larang login root langsung) dan 
MaxAuthTries 3 (maksimal tiga kali percobaan). Lakukan dengan urutan yang aman: backup, edit, validasi dengan sshd -t, reload. 
Verifikasi perubahan dengan grep -E "PermitRoot|MaxAuth" /etc/ssh/sshd_config. 
Kemudian periksa log SSH untuk memastikan tidak ada error setelah perubahan dengan journalctl -u ssh -n 20. 
Referensi Bab 2 untuk penggunaan ss dan Bab 9 untuk keamanan pengguna.
<img src="Screenshot 2026-05-17 205304.png" width="50%">
<img src="Screenshot 2026-05-17 205505.png" width="50%">
<img src="Screenshot 2026-05-17 205913.png" width="50%">
<img src="Screenshot 2026-05-17 205955.png" width="50%">

Konfigurasi keamanan SSH ditambahkan dengan PermitRootLogin no untuk mencegah login langsung menggunakan akun root, 
dan MaxAuthTries 3 untuk membatasi percobaan login agar lebih aman dari brute force attack.
Setelah konfigurasi diubah, validasi dilakukan menggunakan sshd -t untuk memastikan tidak ada kesalahan sintaks. 
Layanan kemudian di-reload agar perubahan diterapkan tanpa menghentikan koneksi SSH yang sedang aktif.

#### Latihan
##### Latihan 10.1 Audit Layanan dan Analisis Boot
Lakukan audit menyeluruh terhadap layanan yang berjalan di sistem.
1. Jalankan systemctl list-units –type=service –state=running dan catat semua
layanan aktif. Pilih tiga layanan yang kamu kenal, periksa status masing-masing dengan
systemctl status, dan jelaskan fungsinya.
2. Jalankan systemd-analyze blame dan identifikasi lima layanan dengan waktu inisialisasi
terlama. Tampilkan hasilnya menggunakan pipeline: systemd-analyze blame | head -5.
3. Jalankan systemctl –failed dan dokumentasikan hasilnya. Jika ada layanan yang gagal, cari
tahu penyebabnya dengan journalctl -u nama-layanan -n 30.

<img src="Screenshot 2026-05-17 222021.png" width="50%">

Menampilkan semua layanan yang sedang berjalan.

<img src="Screenshot 2026-05-17 222252.png" width="50%">

Melihat detail status layanan seperti PID, status aktif, dan log terbaru.

<img src="Screenshot 2026-05-17 222645.png" width="50%">

Menampilkan 5 layanan dengan waktu boot paling lama.

<img src="Screenshot 2026-05-17 222730.png" width="50%">

Menampilkan layanan yang gagal berjalan. Tetapi dalam screenshot tersebut hasilnya tidak ada yang gagal

##### Latihan 10.2 Layanan Kustom dengan Restart Otomatis
Buat layanan systemd kustom yang mendemonstrasikan fitur restart otomatis.
1. Buat skrip Bash (referensi Bab 7) bernama monitor-disk.sh yang setiap 30 detik menuliskan
penggunaan disk ke berkas log. Gunakan df -h dan date.
2. Buat berkas unit /etc/systemd/system/monitor-disk.service untuk menjalankan skrip
tersebut dengan konfigurasi: Restart=always, RestartSec=5s, dan berjalan sebagai pengguna kamu sendiri.
3. Aktifkan dan jalankan layanan. Verifikasi dengan systemctl status dan pastikan log masuk
ke journal.
4. Simulasikan crash dengan membunuh proses secara paksa (kill -9), tunggu 10 detik, dan
verifikasi bahwa layanan hidup kembali secara otomatis.
5. Bersihkan: nonaktifkan layanan dan hapus berkas unit setelah selesai.

1. Buat script monitor disk
nano monitor-disk.sh
<img src="Screenshot 2026-05-17 223651.png" width="50%">

2. Beri izin execute
chmod +x monitor-disk.sh

3. Buat service systemd
sudo nano /etc/systemd/system/monitor-disk.service
<img src="Screenshot 2026-05-17 224015.png" width="50%">

<img src="Screenshot 2026-05-17 224301.png" width="50%">

4. Reload systemd
sudo systemctl daemon-reload
5. Aktifkan service
sudo systemctl enable --now monitor-disk
6. Cek status
systemctl status monitor-disk
7. Cek log journal
journalctl -u monitor-disk -n 20

<img src="Screenshot 2026-05-17 224442.png" width="50%">

Simulasi crash
sudo kill -9 $(systemctl show monitor-disk --property=MainPID --value)
9. Tunggu lalu cek lagi
sleep 10
systemctl status monitor-disk
Memastikan service hidup kembali otomatis.

<img src="Screenshot 2026-05-17 224626.png" width="50%">

Bersihkan service

##### Latihan 10.3 Investigasi Log dan Keamanan SSH
Analisis log sistem dan tingkatkan keamanan konfigurasi SSH.
1. Gunakan journalctl -b -p err untuk menemukan semua error sejak boot terakhir. Simpan
hasilnya ke berkas dan hitung jumlah baris dengan wc -l.
2. Lakukan tiga perubahan keamanan pada /etc/ssh/sshd_config: tambahkan PermitRootLogin
no, MaxAuthTries 3, dan LoginGraceTime 30. Ikuti alur aman: backup, edit, validasi sshd
-t, reload.
3. Setelah reload, verifikasi tiga hal: layanan masih berjalan (systemctl status ssh), port
masih mendengarkan (ss -tlnp | grep ssh), dan konfigurasi baru terbaca (grep -E
"PermitRoot|MaxAuth|GraceTime" /etc/ssh/sshd_config).
4. Kembalikan konfigurasi SSH ke kondisi semula menggunakan berkas backup.

<img src="Screenshot 2026-05-17 232600.png" width="50%">

1. Simpan log error
journalctl -b -p err --no-pager > error-boot.txt
2. Hitung jumlah error
wc -l error-boot.txt
3. Backup konfigurasi SSH
sudo cp /etc/ssh/sshd_config /etc/ssh/sshd_config.backup
4. Edit konfigurasi SSH
sudo nano /etc/ssh/sshd_config
menambahkan :
<img src="Screenshot 2026-05-17 232654.png" width="50%">

<img src="Screenshot 2026-05-17 232738.png" width="50%">

5. Validasi konfigurasi
sudo sshd -t
6. Reload SSH
sudo systemctl reload ssh
7. Verifikasi SSH aktif
systemctl status ssh

<img src="Screenshot 2026-05-17 232930.png" width="50%">

8. Verifikasi port SSH
ss -tlnp | grep ssh
9. Verifikasi konfigurasi
grep -E "PermitRoot|MaxAuth|GraceTime" /etc/ssh/sshd_config

<img src="Screenshot 2026-05-17 233022.png" width="50%">

10. Kembalikan konfigurasi awal
sudo cp /etc/ssh/sshd_config.backup /etc/ssh/sshd_config
sudo systemctl restart ssh

Mengembalikan konfigurasi SSH seperti semula.