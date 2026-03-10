# Laporan Pertemuan 4

#
<h4>Nama : Elyza Putri Rahayu<h4>
<h4>NIM  : 254107020035<h4>
<h4>Kelas: TI-1G<h4>

#

### TUGAS PENDAHULUAN
Jawablah pertanyaan-pertanyaan di bawah ini :
1.	Apa yang dimaksud perintah-perintah direktory : pwd, cd, mkdir, rmdir.
2.	Apa yang dimaksud perintah-perintah manipulasi file :	cp, mv dan rm (sertakan format yang digunakan)
3.	Jelaskan perbedaan Symbolic link menggunakan hard link (direct) dan soft link
(indirect).
4.	Tuliskan maksud perintah-perintah : file, find, which, locate dan grep.

jawaban :
1. a. perintah pwd (Print Working Directory), Digunakan untuk menampilkan lokasi direktori saat ini. Artinya: menampilkan folder tempat kita sedang berada.
   b. cd (Change Directory), Digunakan untuk berpindah dari satu direktori ke direktori lain. formatnya : cd nama_folder, contoh : cd Documents
   c. mkdir (Make Directory), Digunakan untuk membuat folder baru.Formatnya : mkdir nama_folder, contoh : mkdir tugas
   d.  rmdir (Remove Directory), Digunakan untuk menghapus folder kosong. Dan hanya bisa hapus folder yang kosong, Formatnya rmdir nama_folder
2. a. cp (copy), Digunakan untuk menyalin file. Formatnya : cp sumber tujuan, contoh : cp file1.txt file2.txt, Artinya: menyalin file1.txt menjadi file2.txt.
   b. mv (Move / Rename), Digunakan untuk memindahkan atau mengganti nama file. Formatnya mv sumber tujuan, contoh rename : mv file1.txt filebaru.txt, contoh pindah : mv file1.txt /home/elyza/Documents
   c. rm (Remove), Digunakan untuk menghapus file. Formatnya : rm nama_file, contoh : rm file1.txt, Untuk hapus folder beserta isinya : rm -r nama_folder. 
3. Perbedaan Hard Link dan Soft Link :
Hard Link (Direct) :
- Mengarah langsung ke inode file asli
- Jika file asli dihapus, link masih bisa digunakan
- Tidak bisa beda filesystem
- Tidak bisa untuk folder
contoh : ln file1.txt filelink.txt

Soft Link (Symbolic Link / Indirect) :
- Hanya berupa shortcut ke file asli
- Jika file asli dihapus → link rusak
- Bisa beda filesystem
- Bisa untuk folder
contoh : ln -s file1.txt link.txt
4. a. file, Digunakan untuk mengetahui tipe file. Contoh : file tugas.txt
   b. find, Digunakan untuk mencari file di dalam direktori tertentu. Format : find lokasi -name nama_file, contoh : find /home -name tugas.txt
   c. which, Digunakan untuk mengetahui lokasi program. contoh : which python
   d. locate, Digunakan untuk mencari file dengan database sistem (lebih cepat dari find). contoh : locate tugas.txt
   e. grep, Digunakan untuk mencari teks di dalam file. Formatnya : grep kata nama_file, contoh : grep linux tugas.txt

### PERCOBAAN 1 : Directory

1. Melihat Direktori HOME

<img src="Screenshot 2026-03-04 112430.png" width="50%">

Perintah pwd (Print Working Directory) digunakan untuk menampilkan direktori kerja saat ini. Biasanya saat pertama login, sistem akan berada pada direktori HOME user.
Perintah <img src="Screenshot 2026-03-04 192514-1.png" width="8%"> digunakan untuk menampilkan lokasi direktori HOME dari user yang sedang aktif. Variabel $HOME adalah environment variable yang menyimpan path direktori home pengguna.
Tujuan praktikum ini adalah untuk mengetahui lokasi direktori kerja awal dan membandingkannya dengan direktori HOME.

2. Melihat Direktori Aktual dan Parent Direktori 

<img src="Screenshot 2026-03-04 113919.png" width="50%">

- cd . digunakan untuk tetap berada pada direktori saat ini (tidak berpindah).
- cd .. digunakan untuk berpindah ke direktori induk (parent directory).
- cd tanpa argumen akan membawa user kembali ke direktori HOME.
Memahami navigasi direktori menggunakan simbol:
- . (direktori saat ini)
- .. (direktori induk)

3. Membuat Direktori dan Subdirektori

<img src="Screenshot 2026-03-04 114238.png" width="50%">

Perintah mkdir digunakan untuk membuat direktori baru. Dalam praktikum ini dibuat beberapa direktori sekaligus, termasuk subdirektori. 
Perintah ls -l digunakan untuk menampilkan daftar direktori dan file dalam format detail.
Tujuan praktikum ini adalah memahami pembuatan banyak direktori sekaligus dan struktur folder bertingkat.

4. Menghapus Direktori Kosong

<img src="Screenshot 2026-03-04 114704.png" width="50%">

Perintah rmdir digunakan untuk menghapus direktori yang kosong.
Pada percobaan pertama:
rmdir B
akan gagal karena direktori B masih berisi subdirektori F.
Setelah subdirektori dihapus:
rmdir B/F B
maka direktori B dapat dihapus.
Praktikum ini menunjukkan bahwa:
- rmdir hanya bisa menghapus direktori kosong.
- Pengguna harus memiliki izin akses terhadap direktori tersebut.

5. Navigasi Direktori

<img src="Screenshot 2026-03-04 115005.png" width="50%">

Perintah tersebut menghasilkan error karena path yang dituliskan salah. Struktur direktori Linux untuk home user adalah:
/home/username/
Sedangkan:
<img src="Screenshot 2026-03-04 192242.png" width="6%">
tidak valid karena folder user tidak berada langsung di root (/), melainkan berada di dalam direktori /home.
Praktikum ini bertujuan untuk memahami struktur path absolut di sistem Linux.

### Percobaan 2 : Manipulasi File

1. Perintah cp (Copy File / Direktori)
<img src="Screenshot 2026-03-04 211647.png" width="50%">
<img src="Screenshot 2026-03-04 211923.png" width="50%">

Perintah cp digunakan untuk menyalin file atau direktori.
Pada praktikum ini dilakukan beberapa percobaan:
- Menyalin file contoh menjadi contoh1
- Menyalin file ke dalam direktori A
- Menyalin beberapa file sekaligus ke dalam subdirektori A/D
Tujuan praktikum ini adalah memahami cara menyalin file ke lokasi lain dan memahami format perintah:
cp sumber tujuan

2. Perintah mv (Move / Rename)
<img src="Screenshot 2026-03-04 212621-1.png" width="50%">

Perintah mv digunakan untuk:
- Memindahkan file
- Mengganti nama file
Dalam praktikum ini dilakukan:
- Mengganti nama file contoh menjadi contoh2
- Memindahkan beberapa file ke dalam direktori A/D
- Memindahkan file ke direktori C
Format umum perintah:
mv sumber tujuan
- Jika tujuan adalah nama baru → rename
- Jika tujuan adalah folder → pindah file

3. Perintah rm (Remove)
<img src="Screenshot 2026-03-04 212750-1.png" width="50%">

Perintah rm digunakan untuk menghapus file atau direktori.
Pada praktikum ini dilakukan:
- Menghapus file biasa
- Menghapus file dengan konfirmasi menggunakan opsi -i
- Menghapus direktori beserta seluruh isinya menggunakan opsi -rf
Perintah:
rm nama_file
rm -r nama_folder
rm -rf nama_folder

### Percobaan 3 : Membuat Shortcut (File Link)

1. Membuat File
<img src="Screenshot 2026-03-04 214348-1.png" width="50%">

Perintah echo digunakan untuk membuat file bernama halo.txt dan mengisi isinya dengan teks "Hallo apa khabar".
ls -l digunakan untuk melihat detail file termasuk permission, ukuran, dan jumlah link.

2. Membuat Hard Link
<img src="Screenshot 2026-03-04 214427-1.png" width="50%">

Perintah:
ln halo.txt z
membuat hard link bernama z yang terhubung langsung ke file halo.txt.
Ciri hard link:
- Tidak ada tanda panah (→)
- Jumlah link bertambah (biasanya jadi 2)
- Mengarah ke inode yang sama
- Jika file asli dihapus, hard link tetap bisa dibuka
Perintah cat z digunakan untuk melihat isi file melalui hard link tersebut.

3. Membuat Hard Link di Dalam Folder
<img src="Screenshot 2026-03-04 214526-1.png" width="50%">

- mkdir mydir membuat folder baru
- ln z mydir/halo.juga membuat hard link baru di dalam folder tersebut
- cat digunakan untuk memastikan isi file tetap sama
Artinya sekarang ada 3 hard link yang mengarah ke file yang sama.

4. Membuat Soft Link (Symbolic Link)
<img src="Screenshot 2026-03-04 214615-1.png" width="50%">

Perintah:
ln -s z bye.txt
membuat symbolic link (soft link) bernama bye.txt.
Ciri soft link:
- Ada tanda panah → menunjuk ke file asli
- Jika file asli dihapus → link rusak
- Bisa lintas filesystem
- Bisa untuk direktori

### LATIHAN

#### 1. 
<img src="Screenshot 2026-03-10 222104.png" width="50%">

Gambar diatas adalah hasil perintah nya

Pada latihan ini dilakukan percobaan navigasi direktori menggunakan beberapa perintah dasar Linux.
- cd digunakan untuk berpindah direktori.
- pwd digunakan untuk menampilkan direktori kerja saat ini.
- ls -al digunakan untuk menampilkan daftar file dan direktori secara detail.
- cd . menunjukkan direktori saat ini.
- cd .. digunakan untuk berpindah ke direktori induk.
- ls -al | more digunakan untuk menampilkan isi direktori per halaman.
- cat passwd digunakan untuk melihat isi file passwd pada direktori /etc.
- cd - digunakan untuk kembali ke direktori sebelumnya.

#### 2. 
<img src="Screenshot 2026-03-10 222936.png" width="50%">
<img src="Screenshot 2026-03-10 223052.png" width="50%">
<img src="Screenshot 2026-03-10 223122.png" width="50%">
<img src="Screenshot 2026-03-10 223332.png" width="50%">
<img src="Screenshot 2026-03-10 223352.png" width="50%">

Pada latihan ini dilakukan penelusuran beberapa direktori penting dalam sistem Linux.
- /bin berisi program dasar sistem.
- /usr/bin berisi program tambahan untuk pengguna.
- /sbin berisi program administrasi sistem.
- /tmp digunakan untuk menyimpan file sementara.
- /boot berisi file yang digunakan untuk proses booting sistem operasi.

#### 3. 
<img src="Screenshot 2026-03-10 224511.png" width="50%">
<img src="Screenshot 2026-03-10 224547.png" width="50%">

Direktori /dev berisi file perangkat (device files) yang digunakan oleh sistem untuk berkomunikasi dengan perangkat keras.
Perintah who am i digunakan untuk mengetahui terminal yang sedang digunakan oleh pengguna.
Perintah ls -l /dev/tty* digunakan untuk melihat daftar terminal yang tersedia beserta pemiliknya.

#### 4. 
<img src="Screenshot 2026-03-10 225018.png" width="50%">
<img src="Screenshot 2026-03-10 225036.png" width="50%">
<img src="Screenshot 2026-03-10 225053.png" width="50%">
<img src="Screenshot 2026-03-10 225111.png" width="50%">
<img src="Screenshot 2026-03-10 225128.png" width="50%">

Direktori /proc merupakan pseudo filesystem yang berisi informasi mengenai kernel dan proses yang sedang berjalan.
Beberapa file penting yang ditampilkan yaitu:
- interrupts → informasi interrupt perangkat keras
- devices → daftar perangkat yang terdaftar
- cpuinfo → informasi prosesor
- meminfo → informasi penggunaan memori
- uptime → lama waktu sistem berjalan sejak terakhir dinyalakan
- Direktori /proc disebut pseudo filesystem karena file di dalamnya tidak benar-benar tersimpan di disk, tetapi dibuat secara dinamis oleh kernel.

#### 5. 
<img src="Screenshot 2026-03-10 225902.png" width="50%">

Perintah cd ~username digunakan untuk langsung berpindah ke direktori home milik pengguna lain jika memiliki izin akses.

#### 6. 
cd ~ Perintah ini digunakan untuk kembali ke direktori home pengguna yang sedang aktif.

#### 7. 
mkdir work play, Perintah mkdir digunakan untuk membuat direktori baru bernama work dan play pada direktori home.

#### 8. 
rmdir work Perintah rmdir digunakan untuk menghapus direktori kosong bernama work.

#### 9.
cp /etc/passwd ~ Perintah ini menyalin file passwd dari direktori /etc ke direktori home pengguna.

#### 10. 
mv passwd play Perintah mv digunakan untuk memindahkan file passwd ke dalam direktori play.

#### 11.
<img src="Screenshot 2026-03-10 230743.png" width="50%">

Perintah ln -s digunakan untuk membuat symbolic link bernama terminal yang menunjuk ke perangkat terminal /dev/tty.
Jika mencoba membuat hard link ke perangkat tty biasanya akan gagal karena perangkat berada pada filesystem khusus.

#### 12. 
<img src="Screenshot 2026-03-10 230836.png" width="50%">

Perintah ini membuat file hello.txt yang berisi teks hello world.

#### 13. 
<img src="Screenshot 2026-03-10 230846.png" width="50%">

Jika file disalin ke perangkat terminal, isi file akan langsung ditampilkan pada layar terminal karena perangkat tersebut terhubung langsung dengan layar pengguna.

#### 14. 
<img src="Screenshot 2026-03-10 230940.png" width="50%">

Perintah ini membuat symbolic link bernama work yang menunjuk ke direktori play.

#### 15. 
rm -rf work, Perintah rm -rf digunakan untuk menghapus direktori work beserta seluruh isinya secara rekursif tanpa konfirmasi.