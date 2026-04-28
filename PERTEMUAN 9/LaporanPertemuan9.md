## LAPORAN PERTEMUAN 9
##
<h4> Nama    : Elyza Putri Rahayu <h4>
<h4> NIM     : 254107020035  <h4>
<h4> Kelas   : TI - 1G  <h4>

##

##### Latihan Latihan 9.1
Modifikasi laporan-sistem.sh agar menyimpan output ke file
laporan-YYYY-MM-DD.txt sekaligus menampilkannya di terminal. Petunjuk:
gunakan tee yang sudah dipelajari di bab sebelumnya.

jawaban
<img src="Screenshot 2026-04-23 231606-1.png" width="50%">
<img src="Screenshot 2026-04-23 232203-1.png" width="50%">

##### Latihan Latihan 9.2
Buat script kalkulator.sh yang menerima tiga argumen: angka1
operator angka2 dengan operator +, -, *, atau /. Contoh:
./kalkulator.sh 20 + 5 menghasilkan 25. Gunakan case untuk memilih
operasi, dan validasi jika argumen tidak lengkap.

jawaban
<img src="Screenshot 2026-04-26 203651-1.png" width="50%">

- #!/usr/bin/env bash
Baris ini disebut shebang, yang berfungsi untuk menentukan bahwa script dijalankan menggunakan interpreter Bash.

- $# digunakan untuk menghitung jumlah argumen yang dimasukkan.
-ne 3 berarti jumlah argumen harus tepat 3.
Jika tidak sesuai, script akan menampilkan cara penggunaan dan berhenti (exit 1).

- $1, $2, $3 adalah argumen yang dimasukkan pengguna.
Disimpan ke variabel agar lebih mudah digunakan dalam proses selanjutnya.

- Digunakan untuk memastikan bahwa input berupa angka.
[[ ... =~ regex ]] digunakan untuk pencocokan pola.
Jika bukan angka, script akan menampilkan pesan error dan berhenti.

- case digunakan untuk memilih operasi berdasarkan operator.
Jika operator +, maka dilakukan penjumlahan.
Jika operator selain itu, akan dianggap tidak valid.

<img src="Screenshot 2026-04-26 203745-1.png" width="50%">

Memberi izin eksekusi chmod +x kalkulator.sh

<img src="Screenshot 2026-04-26 203818-1.png" width="50%">

Menjalankan Script

##### Latihan 9.3
Tambahkan ke script grading-batch.sh sebuah ringkasan di bagian bawah
yang menampilkan: jumlah mahasiswa per grade (A, B, C, D, E) menggunakan
perulangan for kedua yang mengiterasi array MAHASISWA.

Jawaban

<img src="Screenshot 2026-04-26 213633.png" width="50%">

Script grading-batch.sh digunakan untuk:

Menyimpan data mahasiswa dalam array.
Menyimpan nilai mahasiswa menggunakan associative array.
Menentukan grade berdasarkan nilai menggunakan percabangan if.
Menampilkan hasil nilai dan grade tiap mahasiswa.
Menghitung jumlah mahasiswa untuk setiap grade (A, B, C, D, E) menggunakan perulangan kedua.

<img src="Screenshot 2026-04-26 215505.png" width="50%">

1. Deklarasi Data
Bagian ini digunakan untuk menyimpan daftar nama mahasiswa dan nilai masing-masing mahasiswa dalam bentuk array.

2. Perulangan Pertama (Menampilkan Nilai dan Grade)

Perulangan pertama digunakan untuk:

Mengambil nilai tiap mahasiswa
Menentukan grade berdasarkan rentang nilai
Menampilkan hasil ke terminal

Contoh logika:

Nilai ≥ 85 → Grade A
Nilai ≥ 70 → Grade B
Nilai ≥ 60 → Grade C
Nilai ≥ 50 → Grade D
Selain itu → Grade E

3. Inisialisasi Counter
Variabel ini digunakan untuk menghitung jumlah mahasiswa pada masing-masing kategori grade.

4. Perulangan Kedua (Menghitung Jumlah Grade)

Perulangan kedua digunakan untuk:

Mengiterasi kembali array MAHASISWA
Mengambil nilai setiap mahasiswa
Mengelompokkan berdasarkan grade
Menambahkan nilai counter sesuai kategori
Menampilkan Ringkasan

5. Bagian akhir script menampilkan jumlah mahasiswa untuk setiap grade:

echo "Jumlah A: $countA"

<img src="Screenshot 2026-04-26 215613.png" width="50%">

Memberi izin eksekusi
Menjalankan script

<img src="Screenshot 2026-04-26 215629.png" width="50%">

Hasil

##### Latihan 9.4
Tambahkan fungsi konfirmasi() ke lib-validasi.sh. Fungsi ini
menampilkan pertanyaan, membaca input Y/N dari user, mengembalikan
0 jika Y dan 1 jika N. Buat script demo yang memanggil fungsi ini sebelum
menghapus sebuah file.

jawaban

<img src="Screenshot 2026-04-26 225409.png" width="50%">
<img src="Screenshot 2026-04-26 225859.png" width="50%">

1. File Library (lib-validasi.sh)

File ini berisi fungsi konfirmasi() yang dapat digunakan ulang pada script lain.

Fungsi konfirmasi
konfirmasi() {
  read -p "Apakah Anda yakin? (Y/N): " jawaban

Digunakan untuk membaca input dari user.

case "$jawaban" in
  [Yy]) return 0 ;;
  [Nn]) return 1 ;;
Jika user memasukkan Y/y, fungsi mengembalikan nilai 0 (sukses).
Jika user memasukkan N/n, fungsi mengembalikan nilai 1 (batal).
  *) echo "Input tidak valid" ;;

Digunakan untuk menangani input selain Y atau N.

2. Script Demo (demo-hapus.sh)
a. Mengimpor fungsi
source ./lib-validasi.sh

Digunakan untuk memanggil fungsi dari file lain agar dapat digunakan dalam script utama.

b. Pengecekan file
if [ ! -f "$file" ]; then

Digunakan untuk memastikan file yang akan dihapus benar-benar ada.

c. Pemanggilan fungsi konfirmasi
konfirmasi

Memanggil fungsi untuk meminta persetujuan dari user.

d. Mengecek hasil fungsi
if [ $? -eq 0 ]; then
$? digunakan untuk mengambil nilai return dari fungsi terakhir.
Nilai 0 berarti user menyetujui.
e. Penghapusan file
rm "$file"

Digunakan untuk menghapus file jika user menyetujui.

f. Pesan hasil

Script akan menampilkan:

"File berhasil dihapus" jika user memilih Y
"Penghapusan dibatalkan" jika user memilih N
- Hasil Output
Jika memilih Y:
Apakah Anda yakin? (Y/N): Y
File berhasil dihapus
Jika memilih N:
Apakah Anda yakin? (Y/N): N
Penghapusan dibatalkan
- Kesimpulan

Dari praktikum ini dapat disimpulkan bahwa:

Fungsi dalam Bash memungkinkan kode digunakan kembali (reusable).
Pemisahan fungsi ke dalam file library membuat script lebih modular dan terstruktur.
Penggunaan konfirmasi sangat penting untuk mencegah kesalahan fatal seperti penghapusan file secara tidak sengaja.
Nilai return (0 dan 1) dapat digunakan sebagai dasar pengambilan keputusan dalam script.

<img src="Screenshot 2026-04-26 230045.png" width="50%">
Memberi izin eksekusi, membuat file percobaan, menjalankan script

##### Latihan Latihan 9.5
Script debug-latihan.sh tidak menangani direktori yang tidak ada. Perbaiki
dengan menambahkan:
• set -e di baris kedua
• Pengecekan -d "$DIREKTORI" sebelum memanggil du
• Pesan error yang informatif jika direktori tidak ditemukan
Uji dengan direktori yang tidak ada.

jawaban 

<img src="Screenshot 2026-04-26 231758.png" width="50%">
<img src="Screenshot 2026-04-26 231916.png" width="50%">

set -e
Script akan langsung berhenti jika ada error
Mencegah error berlanjut ke proses berikutnya

-d "$DIREKTORI"
Mengecek apakah path adalah direktori yang valid
Jika tidak → tampilkan error

du -sh
du = disk usage
-s = ringkas
-h = human readable

##### Tugas Praktikum
###### Tugas 1 Script Absensi Kelas
Konteks: instruktur mencatat kehadiran mahasiswa dari command line.
Instruksi:
1. Buat script absensi.sh yang:
• Menerima argumen nama mahasiswa dan status (hadir/izin/alpha)
• Menyimpan entri ke absensi-YYYY-MM-DD.txt dengan format [HH:MM]
NAMA - STATUS
• Opsi -r: tampilkan rekapitulasi (jumlah per status)
• Opsi -h: tampilkan bantuan
2. Rekam minimal 5 entri dan tampilkan rekapitulasinya.
Konsep wajib: variabel, parameter posisional, getopts, if, for, fungsi, dan
redirection ke file.

<img src="Screenshot 2026-04-28 230409.png" width="50%">

Membuat file baru untuk script absensi.
Script ini:
- menerima nama & status
- menyimpan ke file absensi
- bisa menampilkan rekap dengan -r
- pakai fungsi, getopts, dan perulangan

<img src="Screenshot 2026-04-28 230604.png" width="50%">

Menambahkan data absensi ke file

<img src="Screenshot 2026-04-28 230649.png" width="50%">

Menampilkan jumlah hadir, izin, dan alpha

<img src="Screenshot 2026-04-28 230727.png" width="50%">

Melihat isi file absensi yang sudah dibuat

###### Tugas 2 Script Health Check Sistem
Konteks: administrator membuat pemeriksaan kondisi server sebelum maintenance.
Instruksi:
1. Buat script healthcheck.sh menggunakan template profesional dari bagian
Best Practices.
2. Script menampilkan: tanggal/waktu, hostname, uptime, penggunaan CPU,
memori, dan disk untuk setiap filesystem yang terpasang.
3. Jika penggunaan disk mana pun melebihi 80%, tampilkan peringatan.
4. Simpan hasil ke healthcheck-YYYY-MM-DD.log dan tampilkan ke terminal
sekaligus menggunakan tee.
5. Opsi -t <persen> mengubah batas peringatan disk (default 80).
Konsep wajib: set -euo pipefail, trap, getopts, fungsi dengan local,
for, if, dan tee

<img src="Screenshot 2026-04-28 220615.png" width="50%">

- Membuat file script baru bernama healthcheck.sh untuk ditulis kodenya.
- Menuliskan isi script untuk cek kondisi sistem (CPU, memori, disk) dan simpan ke file log.

<img src="Screenshot 2026-04-28 220721.png" width="50%">

Memberi izin supaya file bisa dijalankan sebagai program.
Menjalankan script untuk melihat kondisi sistem dan membuat file log.

<img src="Screenshot 2026-04-28 220743.png" width="50%">

Melihat apakah file log seperti healthcheck-2026-xx-xx.log sudah berhasil dibuat.