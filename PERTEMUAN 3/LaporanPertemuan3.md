# Laporan Pertemuan 3

#
<h4>Nama : Elyza Putri Rahayu<h4>
<h4>NIM  : 254107020035<h4>
<h4>Kelas: TI-1G<h4>

#

### Latihan 3.1
Buatlah script yang:
1. Menampilkan daftar 10 file terbesar di direktori /var/log/
2. Menyimpan hasilnya ke file large-logs.txt
3. Menampilkan output juga di terminal menggunakan tee
4. Menangani error dengan redirect ke error.log

jawab : 
<img src="Screenshot 2026-02-27 135416.png" width="50%">

- Pada praktikum ini dibuat sebuah script bash bernama latihan3_1.sh untuk menampilkan 10 file terbesar pada direktori /var/log/.
- Script menggunakan perintah du -ah untuk menampilkan ukuran seluruh file dan direktori secara lengkap dalam format yang mudah dibaca. Output tersebut kemudian diurutkan dari ukuran terbesar ke terkecil menggunakan sort -rh. Selanjutnya, perintah head -n 10 digunakan untuk mengambil 10 file terbesar saja.
- Untuk memenuhi kebutuhan penyimpanan dan tampilan sekaligus, digunakan perintah tee yang berfungsi menampilkan output di terminal serta menyimpannya ke dalam file large-logs.txt.
- Selain itu, error yang mungkin terjadi selama proses eksekusi diarahkan ke file error.log menggunakan redirect 2>, sehingga kesalahan tidak tampil di terminal tetapi tercatat dalam file terpisah.
- Script dijalankan setelah diberikan izin eksekusi menggunakan perintah chmod +x latihan3_1.sh.
Hasil eksekusi menunjukkan daftar 10 file terbesar pada direktori /var/log/ berhasil ditampilkan dan disimpan sesuai dengan ketentuan soal.

### Latihan 3.2
Buat pipeline yang:
1. Membaca /etc/passwd
2. Mengekstrak username (kolom pertama)
3. Mengurutkan alfabetis
4. Menyimpan ke file sorted-users.txt
Hint: Gunakan cut, sort, dan operator redirect.

jawab : 
<img src="Screenshot 2026-02-27 143916-1.png" width="50%">
<img src="Screenshot 2026-02-27 143946-1.png" width="50%">
<img src="Screenshot 2026-02-27 144041-1.png" width="50%">
<img src="Screenshot 2026-02-27 144141-1.png" width="50%">

Perintah cut -d: -f1 digunakan untuk mengambil kolom pertama (username) dari file /etc/passwd. Output tersebut kemudian diurutkan secara alfabetis menggunakan sort. Hasil akhirnya disimpan ke dalam file sorted-users.txt menggunakan operator redirect >.

### Latihan 3.3
Tulis script monitoring yang:
1. Mencatat penggunaan CPU dan memory setiap 5 detik
2. Menyimpan log dengan timestamp
3. Berjalan selama 1 menit (12 iterasi)
4. Output ditampilkan di terminal DAN disimpan ke file

jawab :
<img src="Screenshot 2026-02-27 150608-1.png" width="50%">

Script dibuat menggunakan perulangan for sebanyak 12 iterasi dengan jeda 5 detik menggunakan perintah sleep. Informasi penggunaan CPU diambil menggunakan perintah top dalam batch mode, sedangkan penggunaan memory diambil menggunakan perintah free -m. Timestamp ditambahkan menggunakan perintah date. Output ditampilkan di terminal dan disimpan ke file monitoring.log menggunakan tee.

### Latihan 3.4 

Buat perintah yang:
1. Mencari semua file .conf di sistem
2. Membuang pesan "Permission denied"
3. Menghitung jumlah file yang ditemukan
4. Menyimpan daftar path lengkap ke file

<img src="Screenshot 2026-02-27 151534.png" width="50%">
<img src="Screenshot 2026-02-27 151614.png" width="50%">
<img src="Screenshot 2026-02-27 151909.png" width="50%">

Perintah find digunakan untuk mencari seluruh file dengan ekstensi .conf pada sistem. Error “Permission denied” dibuang dengan redirect stderr (2>/dev/null). Daftar path lengkap disimpan ke file menggunakan tee, dan jumlah file dihitung menggunakan wc -l.

### Latihan 3.5

Implementasikan script backup yang:
1. Menggunakan tar untuk backup direktori
2. Menampilkan progress dengan tee
3. Mencatat stdout ke backup-success.log
4. Mencatat stderr ke backup-error.log
5. Menambahkan timestamp di setiap log entry

<img src="Screenshot 2026-02-27 160312.png" width="50%">
<img src="Screenshot 2026-02-27 160406.png" width="50%">

Script backup dibuat menggunakan perintah tar untuk membuat arsip terkompresi. Opsi verbose (-v) digunakan untuk menampilkan progress. Output standar (stdout) diarahkan ke backup-success.log dan error (stderr) diarahkan ke backup-error.log. Setiap baris log ditambahkan timestamp menggunakan perintah date. Perintah tee digunakan agar output tetap tampil di terminal sekaligus disimpan ke file log.