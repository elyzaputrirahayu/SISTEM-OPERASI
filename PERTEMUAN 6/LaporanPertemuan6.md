# Laporan Pertemuan 6

#
<h4>Nama : Elyza Putri Rahayu<h4>
<h4>NIM  : 254107020035<h4>
<h4>Kelas: TI-1G<h4>
#

### Latihan 6.1
Jalankan ps aux dan amati outputnya:
1. Berapa total proses yang berjalan? Proses apa yang memiliki PID
terkecil?
2. Jalankan pstree -p dan temukan proses bash Anda. Proses apa yang
menjadi induk (PPID) dari bash tersebut?
3. Bandingkan output ps aux dan ps aux -L. Apa perbedaan yang Anda
lihat?

##### Jawaban
1. 
<img src="Screenshot 2026-04-01 120408.png" width="50%">

Perintah ps aux digunakan untuk menampilkan seluruh proses yang berjalan di sistem.
Jumlah proses dapat dihitung menggunakan wc -l, jumlah prosesnya 107
PID terkecil biasanya adalah PID 1, yaitu /sbin/init, yang merupakan proses utama sistem

2. 
<img src="Screenshot 2026-04-01 120932.png" width="50%">

Perintah pstree -p digunakan untuk menampilkan hubungan antar proses dalam bentuk struktur pohon.
Dengan perintah ini, dapat diketahui proses induk (parent process) dari suatu proses.
Proses bash biasanya merupakan turunan dari proses seperti sshd atau systemd.

3. 
<img src="Screenshot 2026-04-01 121527.png" width="50%">
<img src="Screenshot 2026-04-01 121550.png" width="50%">

Perintah ps aux menampilkan daftar proses yang sedang berjalan di sistem.
Sedangkan ps aux -L menampilkan informasi yang lebih detail termasuk thread dari setiap proses.

Perbedaan utama adalah:
ps aux hanya menampilkan proses
ps aux -L menampilkan proses beserta thread yang dimiliki

Sehingga jumlah baris output pada ps aux -L lebih banyak dibandingkan ps aux.

### Latihan 6.2
1. Jalankan sleep 120 & dan amati kolom STAT pada ps aux. Kondisi
apa yang ditampilkan? Mengapa proses sleep berada di kondisi tersebut?
2. Jalankan beberapa perintah yang berhasil dan yang gagal, lalu catat exit
code masing-masing. Pola apa yang Anda temukan?

##### Jawaban
1. 
<img src="Screenshot 2026-04-01 123222.png" width="50%">

Perintah sleep 120 & digunakan untuk menjalankan proses di background yang akan berhenti selama 120 detik.
Dengan menggunakan ps aux, terlihat bahwa status proses sleep adalah S (Sleeping). Hal ini terjadi karena proses tersebut sedang dalam keadaan menunggu dan tidak melakukan aktivitas CPU.

2. 
<img src="Screenshot 2026-04-01 123457.png" width="50%">

Exit code adalah nilai yang dihasilkan oleh suatu proses setelah selesai dijalankan. Nilai ini dapat dilihat menggunakan perintah echo $?.

Dari percobaan yang dilakukan:
Perintah yang berhasil menghasilkan exit code 0
Perintah yang gagal menghasilkan exit code selain 0

Sehingga dapat disimpulkan bahwa exit code digunakan untuk mengetahui status keberhasilan suatu perintah.

### Latihan 6.3
1. Jalankan nice -n 5 sleep 200 & dan verifikasi nilai NI-nya dengan
ps.
2. Ubah nilai nice menjadi 10 menggunakan renice, lalu verifikasi kembali.
3. Coba ubah nilai nice menjadi -5 tanpa sudo. Apa yang terjadi? Mengapa
Linux membatasi hal ini untuk user biasa?

##### Jawaban
1. 
<img src="Screenshot 2026-04-01 124316.png" width="50%">

Perintah nice -n 5 sleep 200 & digunakan untuk menjalankan proses dengan prioritas lebih rendah dari default. Nilai nice sebesar 5 menunjukkan bahwa proses tersebut memiliki prioritas yang lebih rendah dibandingkan proses dengan nilai nice 0.

2. 
<img src="Screenshot 2026-04-01 124658.png" width="50%">

Perintah renice digunakan untuk mengubah nilai nice dari proses yang sedang berjalan. Setelah diubah menjadi 10, prioritas proses menjadi lebih rendah dibandingkan sebelumnya.

3. 
<img src="Screenshot 2026-04-01 130350.png" width="50%">

Ketika mencoba mengubah nilai nice menjadi negatif tanpa menggunakan sudo, sistem menolak dengan pesan "Permission denied". Hal ini terjadi karena peningkatan prioritas proses dapat mempengaruhi kinerja sistem secara keseluruhan.

Linux membatasi akses ini hanya untuk pengguna dengan hak akses administrator (root) agar mencegah penyalahgunaan sumber daya sistem.

### Latihan 6.4
1. Jalankan sleep 400 &, kirim SIGSTOP, dan amati perubahan kolom
STAT. Kondisi apa yang muncul?
2. Kirim SIGCONT dan verifikasi proses kembali berjalan.
3. Hentikan proses dengan SIGTERM lalu verifikasi sudah tidak ada. Kapan
Anda memilih SIGKILL daripada SIGTERM ?

##### Jawaban
1. 
<img src="Screenshot 2026-04-01 131249.png" width="50%">

Perintah kill -STOP digunakan untuk menghentikan sementara suatu proses. Setelah sinyal ini dikirim, status proses berubah menjadi T (Stopped) yang menunjukkan bahwa proses sedang dihentikan sementara dan tidak berjalan.

2. 
<img src="Screenshot 2026-04-01 131452.png" width="50%">

Perintah kill -CONT digunakan untuk melanjutkan kembali proses yang sebelumnya dihentikan. Setelah diberikan sinyal ini, proses kembali berjalan dengan status normal yaitu Sleeping.

3. 
<img src="Screenshot 2026-04-01 131956.png" width="50%">

Perintah kill tanpa opsi akan mengirim sinyal SIGTERM, yang digunakan untuk menghentikan proses secara normal. Proses akan diberi kesempatan untuk menyelesaikan pekerjaannya sebelum berhenti.

SIGKILL digunakan ketika proses tidak merespon SIGTERM. Sinyal ini akan langsung menghentikan proses secara paksa tanpa memberikan kesempatan untuk cleanup.

### Latihan 6.5
1. Jalankan top di foreground. Apa yang terjadi di terminal?
2. Tekan Ctrl+Z dan cek statusnya dengan jobs. Kondisi apa yang
ditampilkan?
3. Pindahkan ke background dengan bg. Apakah top dapat berjalan dengan
baik di background? Mengapa?
4. Kembalikan ke foreground dengan fg, lalu keluar dengan q .

##### Jawaban
1. 
<img src="Screenshot 2026-04-01 163117.png" width="50%">

Perintah top digunakan untuk menampilkan informasi proses yang berjalan secara real-time. Ketika dijalankan di foreground, terminal akan menampilkan data sistem secara terus-menerus dan tidak dapat digunakan untuk menjalankan perintah lain sampai proses dihentikan.

2. 
<img src="Screenshot 2026-04-01 163203.png" width="50%">

Kombinasi tombol Ctrl + Z digunakan untuk menghentikan sementara proses yang berjalan di foreground. Perintah jobs digunakan untuk melihat daftar proses yang sedang dikelola oleh shell. Status yang ditampilkan adalah Stopped, yang berarti proses dihentikan sementara.

3. 
<img src="Screenshot 2026-04-01 163249.png" width="50%">

Perintah bg digunakan untuk melanjutkan proses yang dihentikan ke background. Namun, aplikasi seperti top tidak berjalan dengan baik di background karena bersifat interaktif dan membutuhkan tampilan langsung di terminal.

4. 
<img src="Screenshot 2026-04-01 163345.png" width="50%">

Perintah fg digunakan untuk mengembalikan proses dari background ke foreground. Setelah kembali ke foreground, aplikasi top dapat berjalan normal kembali. Untuk keluar dari aplikasi top, digunakan tombol q.

### Latihan 6.6
1. Gunakan ps aux –sort=%mem untuk menemukan proses yang menggunakan memori paling banyak di VM Anda. Proses apa itu?
2. Di dalam top, tekan 1 . Apa yang berubah pada tampilan? Mengapa
informasi ini berguna?
3. Di dalam htop, navigasikan ke proses sshd menggunakan tombol panah.
Tekan F9 dan amati opsi sinyal yang tersedia.

##### jawaban 
1. 
<img src="Screenshot 2026-04-01 164907.png" width="50%">

Perintah ps aux --sort=-%mem digunakan untuk menampilkan daftar proses yang diurutkan berdasarkan penggunaan memori terbesar. Dengan menambahkan head, hanya ditampilkan beberapa proses teratas. Proses yang berada di urutan pertama merupakan proses yang menggunakan memori paling besar.

2. 
<img src="Screenshot 2026-04-01 165013.png" width="50%">

Pada aplikasi top, menekan tombol 1 akan mengubah tampilan penggunaan CPU dari total menjadi per core. Informasi ini berguna untuk mengetahui distribusi beban kerja pada masing-masing core CPU.

3. 
<img src="Screenshot 2026-04-01 165117.png" width="50%">

Aplikasi htop menyediakan antarmuka interaktif untuk mengelola proses. Dengan menekan tombol F9, pengguna dapat memilih sinyal yang akan dikirim ke proses tertentu. Hal ini memudahkan dalam mengontrol proses secara langsung tanpa menggunakan perintah manual.

### Latihan 6.A
Eksplorasi Proses Sistem
1. Jalankan ps aux –forest dan temukan proses dengan PID 1. Apa
nama dan fungsi proses tersebut dalam sistem Linux modern?
2. Hitung berapa proses yang dimiliki oleh user root dan berapa yang
dimiliki oleh user Anda. Mengapa root memiliki lebih banyak proses?
3. Temukan semua proses yang berada dalam kondisi S. Mengapa sebagian
besar proses di sistem berada dalam kondisi ini?

##### Jawaban 
1. 
<img src="Screenshot 2026-04-01 181220.png" width="50%">

Perintah ps aux --forest digunakan untuk menampilkan proses dalam bentuk hirarki. Proses dengan PID 1 adalah systemd, yang merupakan proses pertama yang dijalankan saat sistem booting. Proses ini berfungsi sebagai init system yang mengatur dan mengelola seluruh proses serta layanan dalam sistem Linux.

2. 
<img src="Screenshot 2026-04-01 181543.png" width="50%">

Perintah ps aux digunakan untuk menampilkan seluruh proses yang berjalan. Dengan menggunakan grep dan wc -l, dapat dihitung jumlah proses yang dimiliki oleh user tertentu.

Dari hasil pengamatan, user root memiliki lebih banyak proses karena bertanggung jawab menjalankan berbagai layanan sistem dan daemon yang dibutuhkan oleh sistem operasi.

3. 
<img src="Screenshot 2026-04-01 181649.png" width="50%">

Sebagian besar proses di sistem Linux berada dalam kondisi Sleeping (S). Hal ini terjadi karena banyak proses tidak selalu aktif menggunakan CPU, melainkan menunggu event tertentu seperti input pengguna atau permintaan sistem.

Kondisi ini membantu efisiensi penggunaan CPU karena hanya proses aktif saja yang menggunakan sumber daya.

### Latihan 6.B
Simulasi Manajemen Job
1. Jalankan tiga perintah sleep dengan durasi 100, 200, dan 300 detik di
background. Verifikasi ketiganya dengan jobs.
2. Bawa job kedua ke foreground, jeda dengan Ctrl+Z , lalu kembalikan
ke background dengan bg.
3. Hentikan job pertama dengan kill %1. Tampilkan kembali daftar job.
Berapa job yang tersisa?

##### Jawaban
1. 
<img src="Screenshot 2026-04-01 191644.png" width="50%">

Perintah sleep digunakan untuk menunda proses selama waktu tertentu. Dengan menambahkan simbol &, proses dijalankan di background. Perintah jobs digunakan untuk menampilkan daftar job yang sedang berjalan di background.

2. 
<img src="Screenshot 2026-04-01 192058.png" width="50%">

Perintah fg %2 digunakan untuk memindahkan job ke-2 ke foreground. Kombinasi Ctrl + Z digunakan untuk menghentikan sementara proses. Kemudian perintah bg %2 digunakan untuk melanjutkan kembali proses tersebut di background.

3. 
<img src="Screenshot 2026-04-01 192228.png" width="50%">

Perintah kill %1 digunakan untuk menghentikan job pertama. Setelah dihentikan, jumlah job yang tersisa dapat dilihat menggunakan perintah jobs, dan hasilnya menunjukkan bahwa hanya dua job yang masih berjalan.

### Latihan 6.C
Prioritas dan Sinyal
1. Jalankan dua proses sleep: satu dengan nice +5 dan satu dengan nice
+15. Verifikasi nilai NI keduanya dengan ps.
2. Gunakan renice untuk mengubah nice proses pertama menjadi +10.
Proses mana yang kini lebih diprioritaskan scheduler?
3. Kirim SIGSTOP ke salah satu proses, verifikasi kondisi T-nya, lalu kirim
SIGCONT. Akhiri semua proses percobaan dengan pkill sleep.

##### Jawaban
1. 
<img src="Screenshot 2026-04-01 202056.png" width="50%">

Perintah nice digunakan untuk menjalankan proses dengan nilai prioritas tertentu. Nilai nice yang lebih besar menunjukkan prioritas yang lebih rendah. Dari hasil pengamatan, kedua proses memiliki nilai nice yang berbeda sesuai dengan perintah yang diberikan.

2. 
<img src="Screenshot 2026-04-01 202200.png" width="50%">

Perintah renice digunakan untuk mengubah nilai nice dari proses yang sedang berjalan. Setelah diubah menjadi 10, proses tersebut memiliki prioritas lebih tinggi dibandingkan proses dengan nice 15 karena nilai nice yang lebih kecil menunjukkan prioritas yang lebih tinggi.

3. 
<img src="Screenshot 2026-04-01 202414.png" width="50%">

Sinyal SIGSTOP digunakan untuk menghentikan sementara proses sehingga statusnya menjadi Stopped (T). Sinyal SIGCONT digunakan untuk melanjutkan kembali proses tersebut sehingga kembali ke kondisi normal.
Perintah pkill digunakan untuk menghentikan semua proses berdasarkan nama. Dalam hal ini, semua proses sleep dihentikan sekaligus.