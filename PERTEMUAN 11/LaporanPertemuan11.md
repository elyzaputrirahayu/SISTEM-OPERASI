## LAPORAN PERTEMUAN 10
##
<h4> Nama    : Elyza Putri Rahayu <h4>
<h4> NIM     : 254107020035  <h4>
<h4> Kelas   : TI - 1G  <h4>

##

##### Praktikum 9.1 — Permissions
langkah 1
<img src="Screenshot 2026-05-06 104217.png" width="50%">

langkah 2
<img src="Screenshot 2026-05-06 104302.png" width="50%">

langkah 3
<img src="Screenshot 2026-05-06 104412.png" width="50%">

langkah 4
<img src="Screenshot 2026-05-06 104514.png" width="50%">

langkah 5
<img src="Screenshot 2026-05-06 104617.png" width="50%">

Analisis
1. Mengapa secret.txt tidak dapat dibaca oleh group dan others setelah chmod 600?
jawab : Karena permission 600 berarti:

Owner: read (r) + write (w)
Group: tidak ada akses
Others: tidak ada akses

Jadi hanya pemilik file yang bisa membuka dan mengedit file tersebut. Group dan user lain tidak memiliki izin sama sekali, sehingga tidak bisa membaca isi file.

2. Apa perbedaan arti 600 dan 755 terhadap file yang diuji?
jawab : 
- 600:
Owner: read + write
Group: tidak ada akses
Others: tidak ada akses
File bersifat privat (aman)
- 755:
Owner: read + write + execute
Group: read + execute
Others: read + execute
File bisa dijalankan (execute) oleh semua user, cocok untuk script seperti myscript.sh

Jadi perbedaannya:
600 → fokus keamanan (private)
755 → bisa digunakan/dijalankan oleh banyak user

3. Setelah umask 027, permission apa yang dihasilkan untuk file baru, dan mengapa bukan 777?  
jawab : 
Default permission file baru adalah 666 (bukan 777, karena file tidak otomatis executable).

Dengan umask 027:

666 - 027 = 640

Artinya:

Owner: read + write
Group: read
Others: tidak ada akses

Kenapa bukan 777?
Karena:

File biasa defaultnya tidak memiliki execute (x)
Umask digunakan untuk mengurangi izin, bukan menambah

##### Praktikum 9.2 — ACL
<img src="Screenshot 2026-05-06 125212.png" width="50%">
<img src="Screenshot 2026-05-06 191236.png" width="50%">
<img src="Screenshot 2026-05-06 191307.png" width="50%">
<img src="Screenshot 2026-05-06 191441.png" width="50%">

Analisis
1. Mengapa getfacl confidential.txt awalnya tidak menampilkan user tertentu?
jawab : Karena pada awalnya file hanya memiliki permission standar Linux, yaitu:
- owner
- group
- others
Belum ada ACL tambahan (extended ACL) yang diberikan ke user lain.
Perintah getfacl hanya menampilkan entri default tersebut karena belum ada konfigurasi khusus menggunakan setfacl.

2. Setelah setfacl -m u:userA:r confidential.txt, apa perbedaan output ls -l dan getfacl?
jawab : 
- Pada ls -l:
Muncul tanda + di akhir permission (misalnya -rw-r-----+)
Artinya file memiliki ACL tambahan
- Pada getfacl:
Muncul entri baru:
user:userA:r--
Artinya user userA sekarang memiliki akses baca ke file tersebut
Jadi:
ls -l → hanya memberi tanda bahwa ada ACL
getfacl → menampilkan detail lengkap ACL

3. Mengapa file inherited.txt mewarisi ACL dari direktori shared?
jawab : Karena pada direktori shared telah diberikan default ACL menggunakan opsi -d pada setfacl.
Default ACL ini berfungsi sebagai aturan otomatis untuk semua file baru yang dibuat di dalam direktori tersebut.
Akibatnya:
setiap file baru (seperti inherited.txt)
langsung mendapatkan permission yang sama sesuai default ACL direktori

##### Praktikum 9.3A — Membuat dan Mengelola User
<img src="Screenshot 2026-05-07 063926.png" width="50%">
<img src="Screenshot 2026-05-08 032113.png" width="50%">

perintah : 
- sudo useradd -m -s /bin/bash userA
Perintah ini digunakan untuk membuat user baru bernama userA.
- -m → membuat home directory otomatis
- -s /bin/bash → menentukan shell default yang digunakan user

- sudo useradd -m -s /bin/bash userB
Membuat user baru userB dengan home directory dan shell Bash sebagai default.

- sudo passwd userA
Digunakan untuk mengatur atau mengganti password user userA agar bisa login.

- sudo passwd userB
Memberikan password untuk user userB.

- id userA
Menampilkan informasi user seperti UID, GID, dan group yang diikuti oleh userA.

- getent passwd userA
Menampilkan data user dari sistem (seperti isi /etc/passwd), termasuk username, UID, home directory, dan shell.

- sudo usermod -s /bin/zsh userA
Mengubah shell default user userA dari Bash menjadi Zsh.

- getent passwd userA
Digunakan kembali untuk memastikan bahwa shell user sudah berubah menjadi /bin/zsh.

- sudo usermod -L userB
Mengunci akun userB sehingga tidak bisa login.

- sudo passwd -S userB
Menampilkan status akun user userB (aktif atau terkunci).

- sudo usermod -U userB
Membuka kembali (unlock) akun userB agar bisa login lagi.

- sudo passwd -S userB
Digunakan untuk memastikan bahwa status user sudah kembali aktif.

- sudo groupadd developers
Membuat group baru bernama developers.

- sudo groupadd -g 2000 finance
Membuat group finance dengan GID (Group ID) khusus yaitu 2000.

- sudo groupmod -n devteam developers
Mengubah nama group dari developers menjadi devteam.

- sudo gpasswd -a alice devteam
Menambahkan user alice ke dalam group devteam.

- sudo gpasswd -d alice devteam
Menghapus user alice dari group devteam.

- sudo groupdel devteam
Menghapus group devteam dari sistem.

Pertanyaan:
1. Apa perbedaan output id userA sebelum dan sesudah menambah group?
jawab : 
openat(), membuka file atau direktori
read(), membaca isi file
close(), menutup file descriptor
fstat() / newfstatat(), mengambil informasi file (ukuran, izin, dll)

2. Bagaimana status passwd -S userB berubah saat akun di-lock?
jawab : Saat akun userB masih aktif, output passwd -S userB biasanya menampilkan huruf P yang berarti password sudah diatur dan akun dapat digunakan untuk login.
Perubahan status terlihat pada huruf:
- P → akun aktif
- L → akun terkunci (tidak bisa login)

##### Praktikum 9.3B — Group Management
<img src="Screenshot 2026-05-08 042352.png" width="50%">

- sudo groupadd labgroup
Membuat group baru bernama labgroup.

- sudo groupadd readonly-group
Membuat group baru bernama readonly-group.

<img src="Screenshot 2026-05-08 042524.png" width="50%">

- sudo usermod -aG labgroup,readonly-group userA
Menambahkan userA ke group labgroup dan readonly-group.

- sudo usermod -aG readonly-group userB
Menambahkan userB ke group readonly-group.

<img src="Screenshot 2026-05-08 042807.png" width="50%">

- id userA
Menampilkan UID, GID, dan daftar group yang dimiliki userA.

- id userB
Menampilkan informasi group yang dimiliki userB.

- getent group labgroup
Menampilkan informasi group labgroup beserta anggota di dalamnya.

<img src="Screenshot 2026-05-08 042820.png" width="50%">

- getent group readonly-group
Menampilkan informasi dan anggota dari group readonly-group.

Pertanyaan:
1. Apa yang ditampilkan id userA vs groups userA?
jawab : Perintah id userA menampilkan informasi lengkap user seperti UID, GID, dan seluruh group yang dimiliki user tersebut. Sedangkan groups userA hanya menampilkan nama-nama group yang diikuti oleh user tanpa informasi UID dan GID.
2. Mengapa -a pada usermod -aG penting?
jawab : Opsi -a (append) penting karena digunakan untuk menambahkan user ke group tambahan tanpa menghapus group sebelumnya. Jika hanya menggunakan -G tanpa -a, maka daftar group lama user akan diganti dan hanya tersisa group baru yang dimasukkan.

##### Praktikum 9.3C — Password Aging Policy
sudo chage -M 60 -W 7 -m 1 userA
Mengatur kebijakan password untuk userA:

-M 60 → password berlaku maksimal 60 hari
-W 7 → peringatan 7 hari sebelum expired
-m 1 → password minimal digunakan 1 hari sebelum bisa diganti lagi

<img src="Screenshot 2026-05-09 042646.png" width="50%">

- sudo chage -l userA
Menampilkan informasi masa berlaku password dan kebijakan password milik userA.

<img src="Screenshot 2026-05-09 042747.png" width="50%">

- sudo chage -d 0 userA
Memaksa userA mengganti password pada login berikutnya.

<img src="Screenshot 2026-05-09 043707.png" width="50%">

- sudo passwd -l userB
Mengunci akun userB sehingga tidak dapat login menggunakan password.

<img src="Screenshot 2026-05-09 043753.png" width="50%">

- sudo passwd -S userB
Menampilkan status password akun userB.

<img src="Screenshot 2026-05-09 043902.png" width="50%">

- sudo passwd -u userB
Membuka kembali akun userB agar bisa login lagi.

<img src="Screenshot 2026-05-09 043939.png" width="50%">

- sudo passwd -S userB
Memastikan akun userB sudah aktif kembali.

Pertanyaan:
1. Apa arti nilai yang ditampilkan chage -l userA?
jawab : Output chage -l userA menampilkan informasi kebijakan password seperti:
- tanggal terakhir password diganti,
- kapan password akan expired,
- batas minimal dan maksimal umur password,
- serta waktu peringatan sebelum password kedaluwarsa.
Informasi ini digunakan untuk mengelola keamanan akun user.

2. Bagaimana cara membuktikan userB terkunci dari output passwd -S?
jawab : Saat akun dikunci, output passwd -S userB akan menampilkan huruf L yang berarti Locked.
Contoh:
userB L ...
Huruf tersebut menunjukkan bahwa akun tidak dapat digunakan login sampai di-unlock kembali.

3. Kapan sebaiknya menggunakan chage -d 0 vs passwd -e?
jawab : chage -d 0 digunakan untuk memaksa user mengganti password pada login berikutnya dengan mengatur tanggal terakhir perubahan password menjadi 0.

Sedangkan passwd -e digunakan untuk langsung meng-expire password user sehingga user wajib mengganti password saat login berikutnya.

Keduanya memiliki fungsi mirip, tetapi chage -d 0 lebih sering digunakan dalam administrasi sistem Linux untuk pengaturan password aging.

##### Praktikum 9.4 — Konfigurasi sudo

- sudo visudo -f /etc/sudoers.d/lab-userA
Membuka editor aman untuk membuat konfigurasi sudo khusus userA di folder /etc/sudoers.d/.

<img src="Screenshot 2026-05-09 124214.png" width="50%">

- userA ALL=(root) NOPASSWD:/usr/bin/apt update,/usr/bin/apt upgrade
- userA ALL=(root) /bin/systemctl status *
Memberikan izin:
apt update dan apt upgrade tanpa password
systemctl status tetap membutuhkan autentikasi normal

<img src="Screenshot 2026-05-09 124305.png" width="50%">

- sudo -l -U userA
Menampilkan daftar hak akses sudo yang dimiliki oleh userA.

<img src="Screenshot 2026-05-09 124505.png" width="50%">

- sudo grep "userA" /var/log/auth.log | tail -10
Menampilkan 10 log terakhir aktivitas sudo milik userA.

Analisis
1. Mengapa aturan disimpan di /etc/sudoers.d//, bukan langsung di /etc/sudoers?
jawab : Karena folder /etc/sudoers.d/ digunakan untuk menyimpan konfigurasi tambahan agar lebih rapi dan aman. Dengan cara ini, administrator tidak perlu mengedit file utama /etc/sudoers secara langsung sehingga mengurangi risiko kesalahan konfigurasi yang dapat menyebabkan sudo tidak berfungsi.
2. Mana perintah yang bisa dijalankan tanpa password, dan mana yang masih perlu autentikasi?
jawab : 
Perintah:
apt update
apt upgrade
dapat dijalankan tanpa password karena menggunakan opsi NOPASSWD.
Sedangkan:
systemctl status
masih memerlukan autentikasi password karena tidak menggunakan NOPASSWD.

3. Informasi apa saja yang dicatat di log sudo?
jawab : 
Log sudo mencatat informasi seperti:
- nama user yang menjalankan sudo,
- waktu penggunaan sudo,
- perintah yang dijalankan,
- apakah autentikasi berhasil atau gagal,
- serta terminal atau session yang digunakan.
Log ini berguna untuk audit keamanan dan pelacakan aktivitas administrator.

##### Praktikum 9.5 — Disk Quota
<img src="Screenshot 2026-05-10 051203.png" width="50%">

- sudo dd if=/dev/zero of=/tmp/quota-test.img bs=1M count=100
Membuat file kosong berukuran 100 MB yang akan digunakan sebagai filesystem virtual untuk latihan quota.

<img src="Screenshot 2026-05-10 051442.png" width="50%">

- sudo mkfs.ext4 /tmp/quota-test.img
Memformat file image menjadi filesystem ext4 agar bisa di-mount seperti disk biasa.

<img src="Screenshot 2026-05-10 051542.png" width="50%">

- sudo mkdir -p /mnt/quota-test
Membuat folder yang digunakan sebagai tempat mount filesystem quota.

<img src="Screenshot 2026-05-10 051725.png" width="50%">

- sudo mount -o loop,usrquota,grpquota /tmp/quota-test.img /mnt/quota-test
Mount filesystem virtual sekaligus mengaktifkan user quota dan group quota.

<img src="Screenshot 2026-05-10 052554.png" width="50%">

- sudo quotacheck -cug /mnt/quota-test
Membuat database quota untuk user dan group.

<img src="Screenshot 2026-05-10 052538.png" width="50%">

- sudo quotaon -v /mnt/quota-test
Mengaktifkan sistem quota pada filesystem yang sudah di-mount.

<img src="Screenshot 2026-05-10 052633.png" width="50%">

- sudo repquota /mnt/quota-test
Menampilkan laporan penggunaan quota user dan group.

<img src="Screenshot 2026-05-10 052919.png" width="50%">

- sudo edquota -u userA
Membuka editor untuk mengatur batas quota milik userA.

<img src="Screenshot 2026-05-10 053010.png" width="50%">

- sudo repquota /mnt/quota-test
Memastikan quota userA sudah aktif dan terbaca sistem.

<img src="Screenshot 2026-05-10 053144.png" width="50%">

- sudo quotaoff /mnt/quota-test
Menonaktifkan sistem quota.

- sudo umount /mnt/quota-test
Melepas filesystem virtual dari direktori mount.

- sudo rm /tmp/quota-test.img
Menghapus file image quota setelah praktikum selesai.

Analisis
1. Apa perbedaan soft limit dan hard limit saat quota mulai terlampaui?
jawab : Soft limit adalah batas penggunaan yang masih dapat dilampaui sementara dalam periode tertentu (grace period). Sedangkan hard limit adalah batas maksimum mutlak yang tidak boleh dilewati. Jika hard limit tercapai, user tidak dapat menambah data lagi.

2. Mengapa praktikum ini memakai loopback filesystem, bukan langsung /home/?
jawab : Karena loopback filesystem lebih aman untuk praktikum. Dengan metode ini, filesystem utama seperti /home tidak ikut berubah sehingga mengurangi risiko kerusakan atau gangguan pada sistem utama.

3. Dari output repquota, informasi apa yang menunjukkan quota sudah aktif?
jawab : Quota dianggap aktif jika output repquota menampilkan daftar user/group beserta informasi block usage, soft limit, hard limit, dan penggunaan inode. Jika data tersebut muncul, berarti sistem quota sudah berjalan dengan baik.

#####  Latihan
###### Latihan Latihan 9.A — Audit dan Kolaborasi
1. Temukan file SUID aktif dengan find / -perm -4000 -type f 2>/dev/null, lalu jelaskan tiga file yang Anda kenali beserta alasannya.
2. Cari direktori world-writable dan tentukan mana yang valid dan mana yang berisiko.
3. Rancang konfigurasi permission standar dan ACL untuk direktori proyek /srv/webapp/ agar group webapp-team dapat menulis, user deploy hanya membaca, dan file baru selalu mewarisi group proyek.

jawab :
<img src="Screenshot 2026-05-11 193628-1-1.png" width="50%">

- find / -perm -4000 -type f 2>/dev/null
Mencari file yang memiliki permission SUID aktif pada sistem Linux.

<img src="Screenshot 2026-05-11 193738.png" width="50%">

- find / -type d -perm -0002 2>/dev/null
Mencari direktori yang dapat ditulis oleh semua user (world-writable).

<img src="Screenshot 2026-05-11 195100.png" width="50%">

- sudo groupadd webapp-team
Membuat group proyek webapp.

<img src="Screenshot 2026-05-11 195133.png" width="50%">

- sudo mkdir -p /srv/webapp
Membuat direktori proyek webapp.

<img src="Screenshot 2026-05-11 200217-1.png" width="50%">

- sudo chown :webapp-team /srv/webapp
Mengatur group pemilik direktori menjadi webapp-team.
- sudo setfacl -m u:deploy:r-x /srv/webapp
Memberi user deploy akses baca dan execute saja.

<img src="Screenshot 2026-05-11 200327-1.png" width="50%">

- sudo chmod 2775 /srv/webapp
Memberi akses tulis untuk group dan mengaktifkan SGID agar file baru otomatis mewarisi group proyek.

Direktori proyek menggunakan permission group agar anggota tim dapat bekerja bersama. SGID dipakai supaya file baru otomatis memakai group proyek yang sama. ACL digunakan untuk memberi akses khusus kepada user tertentu tanpa mengubah owner atau group utama.

###### Latihan Latihan 9.B — Kebijakan Akun dan Quota
Tuliskan langkah untuk membuat user intern, menambahkannya ke group labgroup, memaksa pergantian password tiap 45 hari (warning 7 hari), memberi izin sudo hanya untuk systemctl status, dan
menetapkan quota ruang serta inode sederhana pada /home/.

<img src="Screenshot 2026-05-11 205722.png" width="50%">

Membuat user baru bernama intern.

<img src="Screenshot 2026-05-11 205845.png" width="50%">

Menambahkan user intern ke group labgroup.

<img src="Screenshot 2026-05-11 205934.png" width="50%">

Password berlaku 45 hari dan peringatan diberikan 7 hari sebelum expired.

<img src="Screenshot 2026-05-11 210038.png" width="50%">
<img src="Screenshot 2026-05-11 210145.png" width="50%">

User intern hanya boleh menjalankan systemctl status.

<img src="Screenshot 2026-05-11 210845.png" width="50%">

- sudo apt install quota -y
Menginstall tools quota Linux.
- mount | grep home
Melihat apakah filesystem /home sudah memakai opsi quota.
- sudo mkdir -p /mnt/quota-test
Membuat direktori untuk mount filesystem quota.
- sudo dd if=/dev/zero of=/tmp/quota-test.img bs=1M count=100
Membuat file image 100 MB sebagai media filesystem virtual.
- sudo mkfs.ext4 /tmp/quota-test.img
Memformat file image menjadi filesystem ext4.
- sudo mount -o loop,usrquota,grpquota /tmp/quota-test.img /mnt/quota-test
Mount filesystem virtual sekaligus mengaktifkan quota user dan group.

<img src="Screenshot 2026-05-11 211334.png" width="50%">

Membuat database quota untuk user dan group.

<img src="Screenshot 2026-05-11 211642.png" width="50%">

<img src="Screenshot 2026-05-11 211756.png" width="50%">

Menampilkan laporan quota untuk memastikan quota user sudah aktif.

<img src="Screenshot 2026-05-11 212635.png" width="50%">

- sudo quotaoff /mnt/quota-test
Menonaktifkan quota.
- sudo umount /mnt/quota-test
Melepas filesystem virtual dari mount point.
- sudo rm /tmp/quota-test.img
Menghapus file image quota setelah praktikum selesai.