## Laporan Praktikum Pertemuan 2

#
<h4>Nama : Elyza Putri Rahayu<h4>
<h4>NIM  : 254107020035<h4>
<h4>Kelas: TI-1G<h4>

#
### Praktikum 2.1 - Identifikasi CPU dan Memori
#### Pertanyaan latihan 2.1
(1) jumlah CPU(s), core/thread, (2) total RAM, (3) total swap.Jelaskan perbedaan RAM vs swap dalam 2–3 kalimat.

#### jawaban 2.1
1. jumlah CPU(s) nya 1
2. Total RAM nya adalah 1.9Gi
3. total swap nya adalah 2.0Gi
perbedaan RAM vs swap, RAM adalah memori utama berkecepatan tinggi yang aktif menyimpan data sementara saat komputer menyala, bersifat volatile (data hilang saat mati). Swap adalah ruang cadangan di hard disk/SSD (memori virtual) yang digunakan saat RAM penuh, berkinerja lebih lambat, dan berfungsi mencegah sistem crash. RAM jauh lebih cepat dibandingkn swap karena menggunakan chip memori khusus. Swap menggunakan storage (HDD/SSD) yang kecepatannya jauh lebih rendah.

<img src="Screenshot 2026-02-18 124045.png" width="50%">
<img src="Screenshot 2026-02-18 124128.png" width="50%">

### Praktikum 2.2 - Identifikasi Perangkat PCI/USB dan Driver
#### Pertanyaan latihan 2.2
Temukan 1 perangkat PCI (misal NIC) dan tuliskan: Vendor:Device ID (angka heksadesimal), nama driver/modul kernel, dan deskripsi singkat fungsinya

#### Jawaban 2.2
1. Ethernet controller
- Perangkat : Intel Corporation 82540EM Gigabit Ethernet Controller
- Driver/modul kernel : e1000
- Driver berfungsi untuk mengatur kartu jaringan (LAN) sehingga sistem dapat terhubung ke jaringan dan internet.
2. System Peripheral (VirtualBox Guest Service)
- Perangkat : Innotek Systemberatung GmbH VirtualBox Guest Service
- Driver/modul kernel : vboxguest
- Driver ini digunakan untuk mendukung integrasi antara sistem operasi guest (Ubuntu) dengan host (VirtualBox), seperti sinkronisasi waktu dan fitur tambahan VM.
3. Multimedia Audio Controller
- Perangkat : Intel Corporation 82801AA AC'97 Audio Controller
- Driver/modul kernel : snd_intel8x0
- Driver ini berfungsi untuk mengatur perangkat audio sehingga sistem dapat memproses input dan output suara.
4. USB Conntroller (USB 1.1)
- Perangkat : Aplle Inc. Keylargo/Intrepid USB
- Driver/modul kernel : ohci-pci
- Berfungsi mengontrol perangkat USB dengan kecepatan hingga 12 Mbps (USB 1.1)
5. USB Controller (USB 2.0)
- Perangkat : Intel Corporation 82801FB/FBM/FR/FW/FRW USB2 EHCI Controller
- Driver/modul kernel : ehci-pci
- Berfungsi untuk Mengontrol perangkat USB 2.0 dengan kecepatan hingga 480 Mbps.
6. SATA Controller
- Perangkat : Intel Corporation 82801HM/HEM SATA Controller
- Driver/modul Kernel : ahci
- Driver ini mengatur komunikasi antara sistem operasi dan perangkat penyimpanan (hard disk/SSD) berbasis SATA.

<img src="Screenshot 2026-02-19 200448.png" width="50%">
<img src="Screenshot 2026-02-19 213305.png" width="50%">

### Praktikum 2.3 - Identifikasi Storage dan Filesystem
#### 
- Berdasarkan hasil perintah findmnt /, partisi root (/) berada pada /dev/mapper/ubuntu--vg-ubuntu--lv dengan tipe filesystem ext4.
- Berdasarkan perintah sudo blkid, UUID partisi tersebut adalah ab95d77b-7f17-4535-94d1-3d634fee8e31. UUID ini digunakan dalam konfigurasi mounting pada file /etc/fstab.

<img src="Screenshot 2026-02-20 124848-1.png" width="50%">
<img src="Screenshot 2026-02-20 124953-1.png" width="50%">

#### 1.2 Modul Kernel dan Driver Perangkat
#### jawaban 1.2
Menjalankan perintah lsmod untuk melihat daftar modul kernel yang sedang aktif. Hasilnya seperti gambar dibawah

<img src="Screenshot 2026-02-20 232626-1.png" width="50%">

Lalu menjalankan perintah modinfo <modul> untuk melihat detail modul (deskripsi, parameter, file, ko, dependensi). saya memasukkan modinfo async_tx, modul kernel async_tx versi 5.15.0-170-generic. Modul ini berada dalam kondisi in-tree, yang berarti modul tersebut merupakan bagian resmi dari kernel Linux dan disertakan langsung dalam distribusi kernel Ubuntu. Modul async_tx tidak memiliki dependensi tambahan (ditunjukkan oleh bagian depens: yang kosong) hal ini berarti modul dapat berjalan secara mandiri tanpa memerlukan modul kernel lain. Modul async_tx berfungsi untuk menangani operasi transfer data secara asynchronous (tidak sinkron), modul ini membantu meningkatkan efisiensi kinerja sistem dengan memungkinkan proses transfer data berjalan tanpa harus menunggu proses lain selesai terlebih dahulu, dan hasilnya seperti dibawah

<img src="Screenshot 2026-02-20 232830-1.png" width="50%">

### Praktikum 2.4 - Melihat Modul Aktif dan Informasinya
<img src="Screenshot 2026-02-21 102847.png" width="50%">
<img src="Screenshot 2026-02-21 103135-1.png" width="50%">

- EXT4 Filesystem Mounted
  EXT4-fs (sda2): mounted filesystem with ordered data mode, sistem berhasil me-mount filesystem EXT4, partisipasi /dev/sda2 digunakan saat proses boot, Mode ordered berarti penulisan data dilakukan secara aman.
- Driver Audio Terdeteksi 
  snd_intel8x0 00:00:05.0: allow list rate ..., Driver audio snd_intel8x0 aktif, sistem mengenali perangkat sound card.
- Network Interface Aktif
e1000: enp0s3 NIC Link is Up 1000 Mbps Full Duplex, Driver e1000 aktif, interface jaringan enp0s3 sudah terhubung, kecepatan 1000 Mbps (1 Gbps).

### Praktikum 2.5 - Konfigurasi Auto-load dan Blacklist
<img src="Screenshot 2026-02-21 130912.png" width="50%">

Saat menjalankan perintah lsmod | grep -i loop tidak menampilkan apa apa karena sebelumnya sudah dicek menggunakan perintah modinfo loop

#### 1.3 Sistem File dan /dev di Linux
<img src="Screenshot 2026-02-21 133158.png" width="50%">

Menjalankan perintah ls -l /dev/.. (yang mencantumkan isi direktori root) ditampilkan, menunjukkan daftar file dan direktori sistem seperti bin, root, dev, home, lib, sbin, tmp, usr, var, beserta detail perizinan, kepemilikan, ukuran, dan tanggal modifikasi

<img src="Screenshot 2026-02-21 133303.png" width="50%">

- Menjalankan perintah lsblk untuk menampilkan daftar blok perangkat (disk dan partisi). termasuk nama, ukuran, tipe, dan titik kait (mountpoints). Terlihat adanya beberapa perangkat loop (snap packages). Sebuah disk sda berukuran 25G dengan tiga partisi (sda1, sda2 untuk /boot, dan sda3). Volume logis (Lubuntu--vg-ubuntu--lv) yang dikaitkan ke direktori root (/). Perangkat sr0 yang merupakan drive CD-ROM.
- Perintah udevadm info: Perintah ini dijalankan tanpa argumen yang diperlukan, sehingga menghasilkan pesan kesalahan yang menyatakan bahwa nama atau jalur perangkat diperlukan.
- Perintah udevadm monitor: Perintah ini dijalankan dan menampilkan pesan bahwa monitor akan mencetak peristiwa yang diterima untuk UDEV (peristiwa setelah pemrosesan aturan) dan KERNEL (peristiwa uevent kernel).

### Praktikum 2.6 - Mengenali Block vs Character Device
<img src="Screenshot 2026-02-21 141405.png" width="50%">

#### Latihan 2.3
Dari output ls -l, jelaskan perbedaan penanda file untuk block device dan
character device. (Hint: karakter pertama pada permission string)

#### jawaban Latihan 2.3
Berdasarkan output perintah ls -l, perbedaan block device dan character device dapat dilihat dari karakter pertama pada permission string. Huruf b menunjukkan block device seperti /dev/sda, sedangkan huruf c menunjukkan character device seperti /dev/tty. Block device digunakan untuk perangkat penyimpanan berbasis blok, sedangkan character device digunakan untuk perangkat berbasis aliran karakter seperti terminal.

### Praktikum 2.7 - Melihat Informasi udev
<img src="Screenshot 2026-02-21 143905.png" width="50%">
<img src="Screenshot 2026-02-21 144312.png" width="50%">

Berdasarkan hasil perintah udevadm info, device /dev/sda termasuk dalam subsystem block dengan tipe disk. Device memiliki major number 8 dan minor number 0. Informasi vendor menunjukkan ATA dengan model VBOX_HARDDISK, yang menandakan disk virtual dari VirtualBox. Perintah udevadm monitor digunakan untuk memantau event perangkat secara real-time tanpa mengubah sistem.

#### 1.4 Perintah Dasar Terminal Linux

<img src="Screenshot 2026-02-21 165519.png" width="50%">

- Saya mencoba beberapa perintah dasar di terminal Linux. Pertama, menggunakan pwd untuk mengetahui posisi direktori saat ini dan ls untuk melihat isi folder. Perintah ls -l digunakan untuk melihat detail file seperti permission dan pemilik file. 
- Selanjutnya, saya membuat folder latihan_terminal agar proses latihan lebih aman dan tidak mengganggu file sistem. Di dalam folder tersebut, saya membuat file menggunakan touch, menambahkan isi file dengan echo, dan membaca isi file menggunakan cat. 
- Saya juga mencoba menyalin file dengan cp dan mengganti nama file dengan mv. Terakhir, saya menghapus folder menggunakan rm -ri, di mana sistem meminta konfirmasi sebelum menghapus.

### Praktikum 2.8 - Membuat Workspace Praktikum
<img src="Screenshot 2026-02-21 172331.png" width="50%">
<img src="Screenshot 2026-02-21 172523.png" width="50%">
<img src="Screenshot 2026-02-21 172541.png" width="50%">
<img src="Screenshot 2026-02-21 172553.png" width="50%">

- saya membuat beberapa file contoh menggunakan perintah touch, yaitu notes.txt, data.log, dan config.txt. File tersebut ditampilkan menggunakan ls -lah untuk melihat detailnya.
- Selanjutnya, saya menambahkan isi ke dalam data.log menggunakan perintah echo dengan operator >> agar data ditambahkan tanpa menghapus isi sebelumnya. Isi file kemudian dicek menggunakan cat dan dibaca menggunakan less.

### Praktikum 2.9 - Pencarian Pola dengan grep

<img src="Screenshot 2026-02-21 190548.png" width="50%">

- saya menggunakan perintah grep untuk mencari pola tertentu di dalam file data.log.
- Pertama, saya menjalankan grep "ERROR" data.log untuk menampilkan baris yang mengandung kata ERROR, dan hasilnya menampilkan dua baris error.
- Kemudian, saya menggunakan grep -i "error" data.log untuk mencari tanpa membedakan huruf besar dan kecil. Hasilnya tetap sama karena kata ERROR ditulis dengan huruf besar.
- Selanjutnya, saya menjalankan grep -n "WARN" data.log untuk menampilkan nomor baris yang mengandung kata WARN. Hasilnya menunjukkan bahwa WARN berada pada baris ke-2 dan ke-5.
- Terakhir, saya menggunakan grep -v "INFO" data.log untuk menampilkan baris yang tidak mengandung kata INFO. Hasilnya hanya menampilkan baris WARN dan ERROR.

#### Latihan 2.4
Gunakan grep untuk menampilkan hanya baris yang mengandung INFO atau
WARN dari data.log. (Hint: gunakan grep -E dengan pola alternatif)

#### jawaban Latihan 2.4
<img src="Screenshot 2026-02-22 064909.png" width="50%">

Menjalankan perintah grep -E "INFO|WARN" data.log, artinya mencari baris yang mengandung kata INFO atau WARN pada file data.log, dan hasilnya INFO : service started yang berarti layanan berhasil dijalankan, WARN : disk usage high yang artinya peringatan bahwa penggunaan disk tinggi. Jadi file log berisi pesan informasi (INFO) dan peringatan (WARN). Tidak menampilkan ERROR karena memang tidak dicari di perintah ini.

### Praktikum 2.10 - Subtitusi dengan sed (Aman si File Latihan)

Saya menjalankan perintah sed untuk melakukan substitusi teks pada file config.txt.
- pertama membuat file config.txt yang berisi PORT=8080, MODE=DEV, SERVICE_NAME=myserver.
- Kedua menggunakan sed tanpa -i untuk menampilkan hasil perubahan tanpa mengubah file asli.
- Ketiga menggunakan sed -i untuk mengganti MODE=DEV menjadi MODE=prod, myserver menjadi node.
Untuk hasilnya ada pada screenshot an dibawah ini

<img src="Screenshot 2026-02-22 171115.png" width="50%">

Jadi perintah sed berhasil melakukan substitusi teks. Opsi -i digunakan untuk mengubah isi file secara langsung, sedangkan tanpa -i hanya menampilkan hasil perubahan di terminal.

### Praktikum 2.11 - Ekstraksi Kolom dengan awk

- Saya melakukan pengecekan penggunaan disk menggunakan perintah : df -h perintah tersebut menampilkan informasi kapasitas, penggunaan, dan lokasi mount disk.
- selanjutnya menjalankan perintah <img src="Screenshot 2026-02-22 194814-1.png" width="35%"> NR==1 untuk menampilkan header (baris pertama),
<img src="Screenshot 2026-02-22 195126-1.png" width="8%"> untuk menampilkan partisi dengan penggunaan lebih dari 80%, 
<img src="Screenshot 2026-02-22 200750-1.png" width="8%"> untuk menampilkan kolom Filesystem, use%, dan Mounted on.
- Untuk hasilnya hanya header yang tampil karena tidak ada pertisi dengan penggunan di atas 80% . Penggunaan terttinggi hanya 55%. Jadi Sistem dalam kondisi aman karena tidak ada disk yang melebihi batas 80% penggunaan. Untuk hasilnya ada pada screenshot dibawah ini

<img src="Screenshot 2026-02-22 173652.png" width="50%">
<img src="Screenshot 2026-02-22 175625.png" width="50%">

### Praktikum 2.12 - Melihat Proses dengan ps

<img src="Screenshot 2026-02-22 202139.png" width="50%">

- Saya menggunakan perintah ps aux | head untuk menampilkan daftar semua proses, dan yang ditampilkan hanya beberapa baris awal (karena pakai head), terlihat kolom USER, PID, %CPU, %MEM, dll.
- Kemudian perintah ps aux | grep -i sshd, terlihat sshd: /usr/sbin/sshd -D artinya service SSH sedang berjalan. Baris grep --color=auto -i sshd muncul karena perintah grep juga ikut terbaca

### Praktikum 2.13 - Monitoring Real-time dengan top

<img src="Screenshot 2026-02-22 205235.png" width="50%">

Saya menggunakan perintah top dan memperoleh hasil sebagai berikut :
- Load average : 0.16, 0.22, 0.09, artinya beban sistem rendah
- Tasks : 103 proses (1 running, 102 sleeping).
- CPU usage : 100% idle artinya CPU tidak sedang terbebani
- Memory : 1963 MB total, 1488 MB free, artinya masih banyak tersedia.
- Swap : 0 digunakan.
Proses yang tampil dibagian atas menunjukkan daftar proses aktif seperti systemd, ssdh, dan lainnya. Jadi sistem dalam kondisi normal dan stabil karena penggunaan CPU dan memori rendah.

### Praktikum 2.14 - Menghentikan Proses dengan kill

<img src="Screenshot 2026-02-22 232724.png" width="50%">

- Saya menggunakan perintah sleep 300 &, berguna untuk membuat proses berjalan selama 300 detik di background, terlihat pada PID yang muncul adalah 999.
- Kemudian menjalankan perintah ps aux | grep -E "sleep 300" | grep -v grep, hasilnya menunjukkan proses sleep 300 dengan PID 999
- Kemudian menghentikan proses dengan menggunakan perintah kill 999, sistem menampilkan pesan Terminated, yang berarti proses berhasil dihentikan. 
- Mengecek kembali menggunakan perintah ps, proses sleep 300 sudah tidak muncul. Jadi kill berhasil menghentikan proses berdasarkan PID. Jika proses sudah berhenti, maka perintah kill-9 akan menampilkan pesan "No such process"

### Praktikum 2.15 - Cek Disk, Load, dan Service

<img src="Screenshot 2026-02-22 234314.png" width="50%">
<img src="Screenshot 2026-02-22 234424.png" width="50%">
<img src="Screenshot 2026-02-22 234535.png" width="50%">

- Pertama saya menggunakan perintah df -h untuk melihat penggunaan disk. Hasilnya penggunaan masih dibawah batas kritis.
- Lalu  menggunakan perintah du -sh /var/* untuk mengetahui folder yang memakan ruang besar
- Kemudian menggunakan perintah uptime untuk menampilkan beban sistem. Nilai load average rendah, menandakan CPU tidak terbebani.
- Selanjutnya menggunakan perintah systemctl -xe, tidak ditemukan service yang gagal.
- yang terakhir menggunakan perintah journalctl -xe, log menunjukkan status "succeeded" dan tidak ada error kritis. Jadi hasil pengecekan disk, load, service, dan log, sistem berada dalam kondisi normal dan stabil tanpa indikasi masalah.

### Praktikum 2.16 - Monitoring Port dan Koneksi (Network Basics)
<img src="Screenshot 2026-02-23 081211.png" width="50%">

- Pertama saya menggunakan perintah ip a dan hasilnya menunjukkan Interface lo (loopback) dengan IP 127.0.0.1, Interface enp0s3 dalam keadaan UP, IP address: 10.0.2.15. Artinya jaringan aktif dan sudah mendapatkan IP.
- Yang kedua menggunakan perintah ip r, terlihat default gateway: 10.0.2.2, Routing melalui interface enp0s3, artinya server sudah terhubung ke jaringan dan memiliki jalur keluar (internet).
- Yang ketiga menggunakan perintah ss -tulpn, Port yang sedang listening yaitu Port 22 (tcp) dengan Service: sshd, kegunaannya untuk layanan SSH (remote login server). Kemudian ada Port 53 (tcp/udp) dengan Service: systemd-resolved, kegunaannya untuk layanan DNS (penerjemah nama domain ke IP).

#### Latihan 2.5
Pilih satu port yang listening dari output ss -tulpn(misal port 22), lalu
tuliskan service/proses yang membukanya. Jelaskan kegunaan port tersebut
secara singkat.

#### Jawaban Latihan 2.5
Port yang dipilih: 22
Service: sshd
Kegunaan: Digunakan untuk akses remote server melalui protokol SSH secara aman. 
Jadi jaringan dalam kondisi normal, routing aktif, dan service SSH berjalan dengan baik sehingga server dapat diakses secara remote.

### 1.9 Latihan 
#### Latihan 2.A
<img src="Screenshot 2026-02-23 125731-1.png" width="50%">

Saya menggunakan perintah lspci -nnk, perintah tersebut digunakan untuk menampilkan daftar perangkat PCI yang terpasang pada sistem beserta informasi ID vendor, device, dan driver kernel yang digunakan . Salah satu perangkatnya adalah : 

- Nama perangkat : Multimedia audio controller, intel Corporation 82801AA AC'97 Audio Controller
- Vendor:device ID : 1028:0177
- Kernel driver in use : snd_intel8x0

Perintah tersebut berguna untuk mengetahui hardware yang terpasang dan driver yang sedang aktif.

#### Latihan 2.B
<img src="Screenshot 2026-02-23 125813.png" width="50%">

Saya menggunakan perintah findmnt /, digunakan untuk mengetahui device yang digunakan sebagai root filesystem. Kemudian perintah lsblk -f, digunakan untuk melihat tipe filesystem dan UUID. dan hasilnya :
- Device root : sda2
- Tipe filesystem : ext4
- UUID : bb2efec8-7aea-423b-a9b4-d1f89cf1fbc4
UUID digunakan sebagai identitas unik suatu partisi.

#### Latihan 2.C
<img src="Screenshot 2026-02-23 130520.png" width="50%">

Membuat file server.log berisi minimal 10 baris dengan variasi kata INFO, WARN, dan ERROR. Menggunakan perintah grep "ERROR" server.log yang digunakan untuk menampilkan hanya baris ERROR. Hasilnya hanya menampilkan baris yang mengandung kata ERROR. Perintah grep berfungsi untuk mencari dan memfilter teks dalam file.

#### Latihan 2.D
<img src="Screenshot 2026-02-23 130520.png" width="50%">
<img src="Screenshot 2026-02-23 130651.png" width="50%">

Saya menggunakan perintah sed -i 's/server/node/g' server.log, perintah ini mengganti semua kata server menjadi node dalam file. Opsi -i berarti perubahan langsung disimpan ke file. Sebelum dan sesudah perubahan diverivikasi menggunakan perintah cat server.log

#### Latihan 2.E
<img src="Screenshot 2026-02-23 130832.png" width="50%">

Saya menggunakan perintah <img src="Screenshot 2026-02-22 194814-1.png" width="35%">, Perintah ini menampilkan filesystem yang penggunaan disk-nya di atas 70%. awk digunakan untuk memproses dan memfilter kolom tertentu dari output perintah.

#### Latihan 2.F
<img src="Screenshot 2026-02-23 131302.png" width="50%">

- Pertama proses dijalankan dengan perintah sleep 600 &
- Kemudian PID ditemukan menggunakan perintah ps aux | grep sleep | grep -v grep
- Lalu proses dihentikan dengan perintah kill PID

#### Latihan 2.G 
<img src="Screenshot 2026-02-23 131357.png" width="50%">
<img src="Screenshot 2026-02-23 131443.png" width="50%">

Saya menggunakan perintah : 
- systemctl --failed digunakan untuk mengecek service yang gagal.
- systemctl status menampilkan status detail service.
- journalctl digunakan untuk melihat log service.