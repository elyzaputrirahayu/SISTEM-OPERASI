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

Perintah echo $HOME digunakan untuk menampilkan lokasi direktori HOME dari user yang sedang aktif. Variabel $HOME adalah environment variable yang menyimpan path direktori home pengguna.

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
rmdir hanya bisa menghapus direktori kosong.
Pengguna harus memiliki izin akses terhadap direktori tersebut.

5. Navigasi Direktori

<img src="Screenshot 2026-03-04 115005.png" width="50%">

Perintah tersebut menghasilkan error karena path yang dituliskan salah. Struktur direktori Linux untuk home user adalah:

/home/username/

Sedangkan:

/ < user > /C

tidak valid karena folder user tidak berada langsung di root (/), melainkan berada di dalam direktori /home.

Praktikum ini bertujuan untuk memahami struktur path absolut di sistem Linux.