# Laporan Praktikum Manajemen Perangkat Keras & Perintah Dasar Sistem Operasi

<h4>Nama : Dandin Sesilia<h4>
<h4>NIM : 254107020142<h4>
<h4>Kelas : TI-1H<h4>

## Praktikum 2.1 Identifikasi CPU dan Memori
### Tujuan praktikum : memahami spesifikasi CPU dan kondisi memori pada server/VM.

Langkah - langkah :
1. Melihat informasi CPU :
<img width="600" height="200" alt="lscpu" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week2/images2/lscpu.jpeg?raw=true"/>
2. Melihat penggunaan memori :
<img width="500" height="350" alt="free-h" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week2/images2/free-h.jpeg?raw=true"/>
3. Melihat informasi DMI/BIOS :
<img width="600" height="200" alt="DMI" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week2/images2/DMI.jpeg?raw=true"/>

### Latihan 2.1
Catat :
1. Informasi CPU : 
<h4>a. Jumlah CPU(s) = 1<h4>
<h4>b. Core/Thread = 1<h4>
2. Penggunaan memori :
<h4>a. Total RAM = 1.9Gi<h4>
<h4>b. Total Swap = 2.0Gi<h4>
3. Perbedaan RAM Vs Swap :
    RAM adalah tempat penyimpanan data sementara yang bekerja untuk meproses aplikasi yang sedang berjalan, dan isinya akan hilang saat komputer mati. Sedangkan swap adalah media penyimpanan cadangan yang berfungsi untuk membantu sistem tetap berjalan apabila kapasitas RAM mulai penuh, cara kerja swap lebih lambat dibandingkan dengan RAM.

## Praktikum 2.2 Identifikasi Perangkat PCI/USB dan Driver
### Tujuan praktikum : mengenali perangkat PCI/USB dan melihat driver/modul yang dipakai.

Langkah - langkah :
1. Lihat daftar perangkat PCI :
<img width="600" height="300" alt="daftar PCI" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week2/images2/lspci.jpeg?raw=true"/>
2. Lihat perangkat PCI & driver kernel yang digunakan :
<img width="600" height="350" alt="PCI dan Driver" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week2/images2/lspci-nnk.jpeg?raw=true"/>
3. Fokus pada NIC (Ethernet) untuk mencari modul driver :
<img widht="650" height="250" alt="Ethernet" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week2/images2/infoNIC.jpeg?raw=true"/>
4. Lihat perangkat USB :
<img width="700" height="300" alt="daftar USB" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week2/images2/lsusb.jpeg?raw=true"/>
5. Lihat topologi USB (tree) :
<img width="850" height="300" alt="topologi USB" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week2/images2/lsusb-t.jpeg?raw=true"/>

### Latihan 2.2
Temukan 1 perangkat PCI (misal NIC) dan tuliskan: Vendor:Device ID (angka
heksadesimal), nama driver/modul kernel, dan deskripsi singkat fungsinya.
<h4>a. Perangkat NIC (Ethernet Controller)<h4>
    <h4>Vendor:Device ID: 8086:100e<h4>
    <h4>Nama driver/modul kernel : e1000<h4>
    <h4>Deskripsi fungsi : NIC berperan sebagai jembatan antara komputer dengan jaringan komputer yang biasanya dikirim melalui kabel LAN (ethernet). Vendor:Device ID adalah identitas dari perangkat yang terpasang, tujuannya adalah agar sistem operasi dapat mengenali perangkat dan tidak salah memberikan perintah. Sedangkan driver bertugas sebagai penerjemah antara sistem operasi dan perangkat keras.<h4>

## Praktikum 2.3 Identifikasi Storage dan Filesystem
### Tujuan praktikum : memahami disk/partisi dan filesystem yang terpasang.

Langkah - langkah :
1. Lihat daftar disk/partisi :
<img width="600" height="300" alt="daftar disk" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week2/images2/lsblk-f.jpeg?raw=true"/>
2. Tampilkan UUID dan tipe filesystem :
<img width="800" height="600" alt="UUID dan tipe filesystem" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week2/images2/uuid.jpeg?raw=true"/>
3. Lihat mountpoint untuk root filesystem :
<img width="700" height="400" alt="mountpoint" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week2/images2/mountpoint.jpeg?raw=true"/>

### Interpretasi cepat
Jika findmnt / menunjukkan root berada di /dev/sda2, maka pada lsblk-f Anda bisa lihat tipe filesystem (misal ext4) dan UUID partisi tersebut. UUID penting untuk konfigurasi mounting di /etc/fstab.
#### Hasil :
Pada saat menjalankan perintah findmnt /, didapatkan bahwa root berada pada blok perangkat ubuntu--vg-ubuntu--lv. Dengan menjalankan perintah lsblk -f, diketahui bahwa informasi partisi menggunakan tipe filesystem ext4 dengan UUID 9fd8cc3f-e3fc-4cd6-9e77-4dd99991d8da.

## Praktikum 2.4 Melihat Modul Aktif dan Informasinya
### Tujuan praktikum : mengenal modul aktif dan keterkaitannya dengan perangkat.

Langkah - langkah :
1. Cek versi kernel :
<img width="600" height="300" alt="versi kernel" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week2/images2/versikernel.jpeg?raw=true"/>
2. Tampilkan daftar modul aktif :
<img width="600" height="400" alt="daftar modul aktif" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week2/images2/modulaktif.jpeg?raw=true"/>
3. Pilih salah satu modul (contoh aman: loop) dan lihat detailnya :
<img width="600" height="300" alt="detail modul loop" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week2/images2/modulloop.jpeg?raw=true"/>
4. Muat modul (jika belum aktif), lalu verifikasi :
Modul loop sudah aktif, dibuktikan dengan status builtin pada modinfo loop dan verifikasi /proc/devices diketahui bahwa driver loop aktif pada mayor 7
<img width="900" height="600" alt="verifikasi keaktifan modul loop" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week2/images2/verifloop.jpeg?raw=true"/>
5. (Opsional) lihat pesan kernel terbaru :
<img width="980" height="890" alt="pesan kernel terbaru" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week2/images2/pesankernel.jpeg?raw=true"/>

## Praktikum 2.5 Konfigurasi Auto-load dan Blacklist
### Tujuan praktikum : memahami cara membuat modul otomatis dimuat atau diblokir

Langkah - langkah :
1. Tambahkan modul auto-load :
<img width="600" height="300" alt="buat file auto-load" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week2/images2/createautoload.jpeg?raw=true"/>
2. Verifikasi modul aktif (tanpa reboot) :
<img width="700" height="400" alt="verifikasi modul aktif" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week2/images2/verifmodul.jpeg?raw=true"/>
Terminal kosong karena driver loop sudah menjadi bagian dari kernel dan tidak muncul di daftar lsmod.

## Praktikum 2.6 Mengenali Block Vs Character
### Tujuan praktikum : membedakan perangkat disk vs terminal

Langkah - langkah :
1. Lihat detail salah satu disk :
<img width="800" height="400" alt="detail disk (sda)" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week2/images2/detailsda.jpeg?raw=true"/>
2. Lihat detail device terminal :
<img width="800" height="400" alt="detail device terminal" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week2/images2/detailtty.jpeg?raw=true"/>
3. Lihat disk dan partisi untuk mengaitkan dengan /dev :
<img width="600" height="400" alt="mapping disk" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week2/images2/mappingdisk.jpeg?raw=true"/>

### Latihan 2.3
Dari output ls -l, jelaskan perbedaan penanda file untuk block device dan
character device. (Hint: karakter pertama pada permission string).
<h4>Jawaban :<h4>
<h4>Perbedaan file penanda block device dan character device terletak pada karakter pertama baris perintah hasil ls -l. Pada perintah ls -l /dev/sda karakter pertamanya adalah huruf b yang menjadi penanda bahwa /dev/sda adalah block device. Sedangkan pada perintah ls -l /dev/tty karakter pertamanya adalah huruf c yang menjadi penanda bahwa /dev/tty adalah character device.<h4>

## Praktikum 2.7 Melihat Informasi udev
### Tujuan praktikum : melihat metadata yang dipakai udev untuk membuat device node.

Langkah - langkah :
1. Cek atribut udev untuk disk :
<img width="800" height="400" alt="atribut udev" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week2/images2/atributudev.jpeg?raw=true"/>

## Praktikum 2.8 Membuat Workspace Praktikum
### Tujuan praktikum : membuat area kerja aman untuk semua latihan bab ini.

Langkah - langkah :
1. Membuat workspace praktikum :
<img width="600" height="300" alt="workspace praktikum" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week2/images2/workspace.jpeg?raw=true"/>
2. Membuat file contoh :
<img width="800" height="400" alt="buat file contoh" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week2/images2/createfile.jpeg?raw=true"/>
3. Mengisi file log contoh :
<img width="600" height="300" alt="mengisi file" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week2/images2/isifile.jpeg?raw=true"/>
4. Membaca file dengan less :
<img width="600" height="300" alt="baca file dengan less" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week2/images2/bacafile.jpeg?raw=true"/>

## Praktikum 2.9 Pencarian Pola dengan grep

Langkah - langkah :
1. Cari baris yang mengandung ERROR pada data.log :
<img width="800" height="400" alt="grep sederhana" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week2/images2/simplegrep.jpeg?raw=true"/>
2. Cari tanpa memperhatikan huruf besar/kecil :
-i digunakan untuk grep tanpa memperhatikan huruf besar/kecil (case insensitive)
<img width="800" height="400" alt="grep case insensitive" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week2/images2/caseinsensitive.jpeg?raw=true"/>
3. Tampilkan nomor baris :
Angka di paling depan menunjukkan baris ke berapa
<img width="800" height="400" alt="grep dengan nomor baris" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week2/images2/grepnomorbaris.jpeg?raw=true"/>
4. Tampilkan baris yang tidak cocok (invert match) :
Digunakan untuk menampilkan baris yang bukan "INFO"
<img width="800" height="400" alt="baris invert match" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week2/images2/invertmatch.jpeg?raw=true"/>

### Latihan 2.4
Gunakan grep untuk menampilkan hanya baris yang mengandung INFO atau
WARN dari data.log. (Hint: gunakan grep-E dengan pola alternatif)
<h4>Jawaban :<h4>
<h4>Perintah grep untuk menampilkan hanya baris yang mengandung INFO atau WARN (INFO|WARN) dari data.log adalah grep -E "INFO|WARN" data.log. grep -E digunakan untuk mengaktifkan extended regex yang berfungsi agar sistem mengenali simbol khusus seperti (|) simbol atau.<h4>
<img width="800" height="400" alt="extended regex" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week2/images2/extendedregex.jpeg?raw=true"/>

## Praktikum 2.10 Substitusi dengan sed (Aman di File Latihan)

Langkah - langkah :
1. Buat file config latihan :
<img width="600" height="300" alt="membuat file config" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week2/images2/createconfig.jpeg?raw=true"/>
2. Ganti dev menjadi prod (tanpa mengubah file asli) :
    sed substitusi tanpa in-place
<img width="800" height="400" alt="sed substitusi tanpa in-place" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week2/images2/sednoninplace.jpeg?raw=true"/>
3. Terapkan perubahan langsung ke file (-i) :
    sed in-place
<img width="800" height="400" alt="sed in-place" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week2/images2/sedinplace.jpeg?raw=true"/>
4. Ganti semua kemunculan kata (g untuk global) :
    Contoh ubah myserver menjadi node
<img width="800" height="400" alt="sed global replacement" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week2/images2/sedglobalreplace.jpeg?raw=true"/>

## Praktikum 2.11 Ekstraksi Kolom dengan awk

Langkah - langkah :
1. Lihat output df -h :
<img width="600" height="300" alt="output df -h" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week2/images2/output%20df-h.jpeg?raw=true"/>
2. Ambil kolom filesystem dan persentase pemakaian :
<img width="900" height="400" alt="awk print kolom" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week2/images2/awkkolom.jpeg?raw=true"/>
3. Filter hanya yang pemakaian disk di atas 80% :
<img width="980" height="500" alt="pemakaian disk up 80%" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week2/images2/diskup80.jpeg?raw=true"/>
Pada perintah ini terminal terlihat kosong, hal ini karena tidak ada penggunaan disk yang digunakan diatas 80%. Diketahui melalui output df -h, penggunaan disk tertinggi hanya 43%.

## Praktikum 2.12 Melihat Proses dengan ps

Langkah - langkah :
1. Tampilkan semua proses (format BSD) :
<img width="600" height="300" alt="semua proses" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week2/images2/allprocess.jpeg?raw=true"/>
2. Cari proses tertentu (misal sshd) :
<img width="800" height="400" alt="cari proses sshd" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week2/images2/sshd.jpeg?raw=true"/>
sistem memperlihatkan bahwa proses grep sedang mencari kata "sshd".

## Praktikum 2.13 Monitoring Real-time dengan top

Langkah - langkah :
1. Jalankan top :
<img width="600" height="300" alt="proses top" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week2/images2/top.jpeg?raw=true"/>
2. Amati nilai load average, pemakaian CPU, dan proses teratas. Tekan q untuk
keluar.
<h4>Load average menunjukkan nilai 0 yang berarti sistem sedang santai. CPU hanya terpakai kurang dari 1%, ditunjukkan pada bar %CPU(s).<h4>

## Praktikum 2.14 Menghentikan Proses dengan kill

Langkah - langkah :
1. Jalankan proses dummy di background :
<img width="800" height="400" alt="proses dummy" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week2/images2/rundummy.jpeg?raw=true"/>
2. Cari PID proses sleep :
<img width="800" height="400" alt="cari PID sleep" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week2/images2/caripid.jpeg?raw=true"/>
3. Hentikan dengan SIGTERM :
<img width="800" height="400" alt="kirim sigterm" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week2/images2/sendsigterm.jpeg?raw=true"/>
4. Verifikasi proses berhenti :
<img width="800" height="400" alt="verifikasi proses berhenti" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week2/images2/verifstop.jpeg?raw=true"/>
Terminal kosong karena PID sudah di kill.

## Praktikum 2.15 Cek Disk, Load, dan Service

Langkah - langkah :
1. Cek penggunaan disk :
<img width="600" height="300" alt="kapasitas disk" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week2/images2/kapasitasdisk.jpeg?raw=true"/>
2. Cari direktori yang besar (contoh pada /var) :
<img width="600" height="300" alt="ukuran direktori" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week2/images2/sizedirektori.jpeg?raw=true"/>
3. Cek load dan uptime :
<img width="800" height="400" alt="load dan uptime" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week2/images2/loadaverage.jpeg?raw=true"/>
4. Cek service yang gagal :
<img width="700" height="350" alt="service gagal" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week2/images2/servicegagal.jpeg?raw=true"/>
5. Ambil log error terbaru (jika ada indikasi masalah) :
<img width="800" height="450" alt="journal new log error" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week2/images2/servicegagal.jpeg?raw=true"/>

## Praktikum 2.16 Monitoring Port dan Koneksi (Network Basics)
### Tujuan praktikum : melihat interface, routing, dan port yang sedang listen (berguna untuk
troubleshooting service).

Langkah - langkah :
1. Lihat interface dan IP :
<img width="800" height="400" alt="IP address" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week2/images2/ipaddres.jpeg?raw=true"/>
2. Lihat routing table :
<img width="800" height="400" alt="routing table" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week2/images2/routing.jpeg?raw=true"/>
3. Lihat port yang sedang listening :
<img width="800" height="400" alt="port listening" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week2/images2/portlisteningg.jpeg?raw=true"/>

### Latihan 2.5
Pilih satu port yang listening dari output ss -tulpn (misal port 22), lalu tuliskan service/proses yang membukanya. Jelaskan kegunaan port tersebut secara singkat.
<h4>Jawaban :<h4>
<h4>Port 22<h4>
<h4>Service/proses : systemd dengan PID 1<h4>
<h4>Kegunaan : port 22 digunakan untuk akses remote terminal secara aman<h4>

## LATIHAN!
### Latihan 2.A
<h4>Jalankan lspci-nnk. Pilih 1 perangkat PCI dan tuliskan: nama perangkat, ID vendor:device, dan kernel driver in use.<h4>
<h4>a. Nama perangkat (VGA compatible controller)<h4>
<h4>b. Vendor:Device ID: 15ad:0405<h4>
<h4>c. Kernel driver in use : vmwgfx<h4>
<img width="900" height="500" alt="latihan 2A" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week2/images2/lat2A.jpeg?raw=true"/>

### Latihan 2.B
<h4>Tentukan device root filesystem dengan findmnt /. Lalu cocokkan dengan lsblk-f dan tuliskan tipe filesystem serta UUID-nya.<h4>
<h4>Dengan perintah findmnt /, dapat diketahui bahwa device yang menangani root filesystem adalah /dev/mapper/ubuntu--vg-ubuntu--lv.<h4>
<img width="800" height="400" alt="latihan 2B1" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week2/images2/lat2B1.jpeg?raw=true"/>
<h4>Melaui lsblk -f terbukti cocok dengan tipe filesystem ext4 dan memiliki UUID 9fd8cc3f-e3fc-4cd6-9e77-4dd99991d8da.<h4>
<img width="700" height="400" alt="latihan 2B2" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week2/images2/lat2B2.jpeg?raw=true"/>

### Latihan 2.C
<h4>Buat file server.log berisi minimal 10 baris dengan variasi kata: INFO, WARN, ERROR. Gunakan grep untuk menampilkan hanya baris ERROR.<h4>
<img width="900" height="500" alt="latihan 2C" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week2/images2/lat2Cfix.jpeg?raw=true"/>

### Latihan 2.D
<h4>Gunakan sed untuk mengganti semua kata server menjadi node pada file
latihan. Tunjukkan sebelum dan sesudah.<h4>
<h4>sebelum sed<h4>
<img width="700" height="400" alt="latihan 2D before sed" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week2/images2/lat2D1.jpeg?raw=true"/>
<h4>sesudah sed<h4>
<img width="700" height="400" alt="latihan 2D after sed" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week2/images2/lat2D2.jpeg?raw=true"/>
<h4>Terlihat tidak ada perbedaan antara sebelum dan sesudah proses sed, karena dalam file tidak ada kata server yang harus diganti dengan node.<h4>

### Latihan 2.E
<h4>Gunakan df-h lalu awk untuk menampilkan filesystem yang penggunaan disk
di atas 70%.<h4>
<img width="800" height="400" alt="latihan 2E" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week2/images2/lat2E.jpeg?raw=true"/>
<h4>Muncul di terminal yang menyatakan bahwa tidak ada filesystem yang penggunaan disknya lebih dari 70%.<h4>

### Latihan 2.F
<h4>Jalankan sleep 600 &. Temukan PID-nya dengan ps. Hentikan dengan SIGTERM. Jelaskan beda SIGTERM vs SIGKILL<h4>
<img width="800" height="400" alt="latihan 2F" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week2/images2/lat2F.jpeg?raw=true"/>
<h4>Proses SIGTERM menghasilkan "Terminated" pada terminal yang berarti proses telah dihentikan sebelum 600 detik. SIGTERM adalah perintah penghentian proses secara sopan dan halus yang bersifat meminta. Sedangkan SIGKILL adalah perintah penghentian proses secara kasar yang bersifat memaksa sistem untuk langsung berhenti.<h4>

### Latihan 2.G
<h4>Gunakan systemctl–failed. Jika tidak ada yang gagal, pilih satu service
aktif (misal ssh) dan tampilkan status serta 30 baris log terakhirnya.<h4>
<img width="900" height="500" alt="latihan 2G" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week2/images2/lat2G.jpeg?raw=true"/>
<h4>Baris log terakhirnya masih sedikit karena ternyata ssh di sistem saya tidak otomatis menyala, jadi baru dinyalakan. Sehingga baris log yang terdahulu tidak tercatat.<h4>
