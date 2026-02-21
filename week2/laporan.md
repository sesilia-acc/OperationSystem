# Laporan Praktikum Manajemen Perangkat Keras & Perintah Dasar Sistem Operasi

<h4>Nama : Dandin Sesilia<h4>
<h4>NIM : 254107020142<h4>
<h4>Kelas : TI-1H<>

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
    a. Jumlah CPU(s) = 1
    b. Core/Thread = 1
2. Penggunaan memori :
    a. Total RAM = 1.9Gi
    b. Total Swap = 2.0Gi
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
    a. Perangkat NIC (Ethernet Controller)
        Vendor:Device ID: 8086:100e
        Nama driver/modul kernel : e1000
        Deskripsi fungsi : NIC berperan sebagai jembatan antara komputer dengan jaringan komputer yang biasanya dikirim melalui kabel LAN (ethernet). Vendor:Device ID adalah identitas dari perangkat yang terpasang, tujuannya adalah agar sistem operasi dapat mengenali perangkat dan tidak salah memberikan perintah. Sedangkan driver bertugas sebagai penerjemah antara sistem operasi dan perangkat keras.

## Praktikum 2.3 Identifikasi Storage dan Filesystem
### Tujuan praktikum : memahami disk/partisi dan filesystem yang terpasang.

Langkah - langkah :
1. Lihat daftar disk/partisi :
<img width="250" height="150" alt="daftar disk" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week2/images2/lsblk-f.jpeg?raw=true"/>
2. Tampilkan UUID dan tipe filesystem :
<img width="400" height="150" alt="UUID dan tipe filesystem" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week2/images2/uuid.jpeg?raw=true"/>
3. Lihat mountpoint untuk root filesystem :
<img width="200" height="100" alt="mountpoint" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week2/images2/mountpoint.jpeg?raw=true"/>

### Interpretasi cepat
Jika findmnt / menunjukkan root berada di /dev/sda2, maka pada lsblk-f Anda bisa lihat tipe filesystem (misal ext4) dan UUID partisi tersebut.
UUID penting untuk konfigurasi mounting di /etc/fstab.
#### Hasil :
Pada saat menjalankan perintah findmnt /, didapatkan bahwa root berada pada blok perangkat ubuntu--vg-ubuntu--lv. Dengan menjalankan perintah lsblk -f, diketahui bahwa informasi partisi menggunakan tipe filesystem ext4 dengan UUID 9fd8cc3f-e3fc-4cd6-9e77-4dd99991d8da.

## Praktikum 2.4 Melihat Modul Aktif dan Informasinya
### Tujuan praktikum : mengenal modul aktif dan keterkaitannya dengan perangkat.

Langkah - langkah :
1. Cek versi kernel :
<img width="80" height="20" alt="versi kernel" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week2/images2/versikernel.jpeg?raw=true"/>
2. Tampilkan daftar modul aktif :
<img width="200" height="130" alt="daftar modul aktif" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week2/images2/modulaktif.jpeg?raw=true"/>
3. Pilih salah satu modul (contoh aman: loop) dan lihat detailnya :
<img width="350" height="200" alt="detail modul loop" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week2/images2/modulloop.jpeg?raw=true"/>
4. Muat modul (jika belum aktif), lalu verifikasi :
<img width="100" height="20" alt="verifikasi keaktifan modul loop" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week2/images2/verifloop.jpeg?raw=true"/>
    Modul loop sudah aktif, dibuktikan dengan status builtin pada modinfo loop dan verifikasi /proc/devices diketahui bahwa driver loop aktif pada mayor 7.
5. (Opsional) lihat pesan kernel terbaru :
<img width="980" height="890" alt="pesan kernel terbaru" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week2/images2/pesankernel.jpeg?raw=true"/>