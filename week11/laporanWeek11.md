# LAPORAN PRAKTIKUM MANAJEMEN FILE & USER/GROUP

#### Nama   : Dandin Sesilia
#### NIM    : 254107020142
#### Kelas  : TI 1H

## Praktikum 11.1 - Permissions
**Tujuan:** membaca permission, mengubahnya dengan aman, dan memahami efek chmod, chown, serta umask pada file nyata.
1. Buat direktori kerja dan dua file uji.
<img width="700" height="400" alt="buat direktori" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week11/image11/direk111.png?raw=true">

2. Jadikan secret.txt privat hanya untuk owner.
<img width="500" height="400" alt="jadikan privat" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week11/image11/fileprivat111.png?raw=true">

3. Jadikan myscript.sh dapat dijalankan.
<img width="500" height="400" alt="run myscript.sh" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week11/image11/fileprivat111.png?raw=true">

4. Buat direktori bersama dan amati efek SGID sederhana.
<img width="500" height="400" alt="buat direktori bersama" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week11/image11/direkSGID111.png?raw=true">

5. Uji efek umask pada file baru.
<img width="500" height="400" alt="uji umask" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week11/image11/direkSGID111.png?raw=true">

### Analisis
1. Mengapa secret.txt tidak dapat dibaca oleh group dan others setelah chmod 600?
> Karena chmod 600 adalah perintah untuk permission file (baca dan ubah) hanya owner saja (-rw-------).

2. Apa perbedaan arti 600 dan 755 terhadap file yang diuji?
> 600 = menjadikan file read n write oleh owner saja, group dan others tidak memiliki akses sama sekali
>
> 755 = owner bisa read, write, dan execute, group dan other bisa read dan execute.

3. Setelah umask 027, permission apa yang dihasilkan untuk file baru, dan mengapa bukan 777?
> permission yang dihasilkan setelah umask adalah -rw-r----- = 640, karena default linux pada file baru adalah 666,
>
> maka 666 - 027 = 640.

### Tantangan
> Ubah owner atau group salah satu file uji ke akun atau group lain yang tersedia di sistem,
>
> kemudian jelaskan perubahan output ls -l sebelum dan sesudahnya.
<img width="500" height="400" alt="tantangan 11.1" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week11/image11/tantangan111.png?raw=true">
Mengubah permission owner dari yang awalnya owner adalah inisesil, sekarang berubah menjadi user root. Apabila permission masih 600, maka user inisesil kehilangan haknya untuk mengakses file.

## Praktikum 11.2 - ACL
**Tujuan:** memahami ACL dari nol: melihat kondisi awal, menambah akses untuk satu user, lal umembuat direktori yang mewariskan ACL otomatis.
1. Siapkan file dan lihat permission standar tanpa ACL tambahan.
<img width="700" height="400" alt="buat file uji acl" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week11/image11/fileujiACL112%20-%20Copy%20(2).png?raw=true">

2. Beri akses baca ke satu user tertentu tanpa mengubah owner atau group.
<img width="700" height="400" alt="tambah user acl" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week11/image11/tambahuserACL112.png?raw=true">

3. Buat direktori bersama yang mewariskan ACL ke file baru.
<img width="700" height="400" alt="buat direktori bersama" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week11/image11/sharedACL112.png?raw=true">

### Analisis
1. Mengapa getfacl confidential.txt awalnya tidak menampilkan user tertentu?
> Karena pada awalnya hanya menampilkan permission default sebelum ditambah user.

2. Setelah setfacl -m u:userA:r confidential.txt, apa perbedaan output ls -l dan getfacl?
> ls -l hanya menampilkan tanda + sebagai tanda ACL aktif.
>
> Sedangan getfacl menampilkan rincian lengkap termasuk masknya juga.

3. Mengapa file inherited.txt mewarisi ACL dari direktori shared?
> Karena menggunakan fitur default ACL (-d) pada direktori shared.

### Tantangan
> Tambahkan satu ACL lagi agar group readonly-group hanya dapat membaca confidential.txt.
>
> Setelah itu, hapus ACL untuk userA dan verifikasi hasil akhirnya dengan getfacl.
<img width="700" height="400" alt="tantangan 11.2" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week11/image11/tantangan112.png?raw=true">

## Praktikum 11.3A - Membuat dan Mengelola User
**Tujuan:** membuat user baru, memodifikasi propertinya, dan memahami perbedaan opsi user add dan user mod.
<img width="700" height="400" alt="praktikum 11.3A" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week11/image11/113a.png?raw=true">

### Pertanyaan
1. Apa perbedaan output id userA sebelum dan sesudah menambah group?
> Sebelum ditambah group user hanya memiliki 1 group
>
> Sesudah ditambah group menjadi ada satu group tambahan 

2. Bagaimana status passwd -S userB berubah saat akun di-lock?
> Statusnya berubah jadi L yaitu lock (terkunci).

## Praktikum 11.3B - Group Management
**Tujuan:** membuat group, menambahkan user ke group, dan memverifikasi keanggotaan.
<img width="700" height="400" alt="praktikum 11.3b" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week11/image11/113b.png?raw=true">

### Pertanyaan
1. Apa yang ditampilkan id userA vs groups userA?
> id userA menampilkan informasi lengkap terkait userA, termasuk uid
>
> groups userA hanya menampilkan informasi group yang diikuti oleh userA, tanpa uid

2. Mengapa -a pada user mod -aG penting?
> -a memastikan bahwa group baru ditambahkan ke daftar group yang sudah ada tanpa menghapusnya.

## Praktikum 11.3C - Password Aging Policy
**Tujuan:** menerapkan kebijakan umur password dan mengamati efeknya.
<img width="700" height="400" alt="praktikum 11.3c" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week11/image11/113c.png?raw=true">

### Pertanyaan
1. Apa arti nilai yang ditampilkan chage -l userA?
> Perintah ini menampilkan kebijakan kedaluwarsa password secara detail.

2. Bagaimana cara membuktikan userB terkunci dari output passwd -S?
> Membuktikannya dengan melihat karakter kedua pada baris output setelah nama user, L (locked), P (password usable).

3. Kapan sebaiknya menggunakan chage -d 0 vs passwd -e?
> change -d digunakan saat ingin mengontrol dan melihat perubahan yang spesifik.
>
> passwd -S digunakan saat ingin memaksa pergantian password tanpa perlu menghafal parameter angka.

### Tantangan
> Buat user bernama intern yang:
>
> • memiliki shell /bin/bash;
>
> • menjadi anggota labgroup;
>
> • dipaksa ganti password pada login pertama;
>
> • password expired setelah 45 hari dengan warning 7 hari sebelumnya.
<img width="700" height="400" alt="tantangan 11.3c" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week11/image11/tantangan113c.png?raw=true">

## Praktikum 11.4 - Konfigurasi sudo
**Tujuan:** membuat aturan sudo terbatas, memverifikasi hak akses, dan membaca log.
1. Buat file konfigurasi sudo khusus untuk userA.
2. Verifikasi aturan yang aktif dan uji hasilnya.
<img width="700" height="400" alt="praktikum 11.4" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week11/image11/114.png?raw=true">

### Analisis
1. Mengapa aturan disimpan di /etc/sudoers.d//, bukan langsung di /etc/sudoers?
> Agar bisa menambah atau menghapus hak akses user tanpa harus mengedit file utama.

2. Mana perintah yang bisa dijalankan tanpa password, dan mana yang masih perlu autentikasi?
> userA dapat menjalankan perintah /usr/bin/apt update dan /usr/bin/apt upgrade tanpa perlu memasukkan password.
>
> Perintah /bin/systemctl status * masih berada di bawah aturan default, sehingga masih memerlukan password user.

3. Informasi apa saja yang dicatat di log sudo?
> Timestamp, user & TTY, lokasi direktori, identitas target, perintah yang dijalankan.

### Tantangan
> Tambahkan satu aturan baru agar userA boleh menjalankan /bin/systemctl restart ssh tetapi tidak boleh menjalankan reboot.
<img width="700" height="400" alt="tantangan praktikum 11.4" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week11/image11/tantangan114.png?raw=true">

## Praktikum 11.5 - Disk Quota
**Tujuan:** memahami alur quota secara aman pada loopback filesystem tanpa mengubah filesystem utama.
1. Buat image filesystem kecil dan mount dengan opsi quota.
2. Buat database quota dan aktifkan enforcement.
<img width="700" height="400" alt="langkah 1-2" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week11/image11/langkah12.png?raw=true">

3. Tetapkan quota untuk user uji dan amati hasilnya.
4. Bersihkan lingkungan uji setelah selesai.
<img width="700" height="400" alt="langkah 3-4" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week11/image11/langkah34.png?raw=true">

### Analisis
1. Apa perbedaan soft limit dan hard limit saat quota mulai terlampaui?
> Soft Limit: Ini adalah ambang batas peringatan. User akan diberikan masa tenggang.
>
> Hard Limit: Ini adalah batas mutlak. Akan diblokir jika melewati batas.

2. Mengapa praktikum ini memakai loopback filesystem, bukan langsung /home/?
> Agar tidak merusak kuota pada direktori /home dan bebas melakukan uji coba.

3. Dari output repquota, informasi apa yang menunjukkan quota sudah aktif?
> Akan mencetak tabel yang berisi kolom User, used, soft, hard, dan grace.

### Tantangan
> Coba atur quota baru untuk userA dengan batas inode yang sangat kecil,
>
> kemudian jelaskan kapan pembatasan inode lebih penting daripada pembatasan block.
<img width="700" height="400" alt="tantangan praktikum 11.5" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week11/image11/tantangan115.png?raw=true">

> Pembatasan Inode lebih penting saat kamu ingin menjaga kesehatan struktur sistem file.

## Latihan 11A - Audit dan Kolaborasi
1. Temukan file SUID aktif dengan find /-perm-4000-type f 2>/dev/null, lalu jelaskan tiga file yang Anda kenali beserta alasannya.
2. Cari direktori world-writable dan tentukan mana yang valid dan mana yang berisiko.
3. Rancang konfigurasi permission standar dan ACL untuk direktori proyek /srv/webapp/ agar group webapp-team dapat menulis, user deploy hanya membaca, dan file baru selalu mewarisi group proyek.
<img width="700" height="400" alt="latihan 11a" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week11/image11/latihan11a.png?raw=true">

## Latihan 11B - Kebijakan Akun dan Quota
Tuliskan langkah untuk membuat user intern, menambahkannya ke group labgroup, memaksa pergantian password tiap 45 hari (warning 7 hari), memberi izin sudo hanya untuk systemctl status, dan menetapkan quota ruang serta inode sederhana pada /home/.
<img width="700" height="400" alt="latihan 11b" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week11/image11/latihan11b.png?raw=true">
