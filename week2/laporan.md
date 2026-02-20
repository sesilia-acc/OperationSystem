# Laporan Praktikum Manajemen Perangkat Keras & Perintah Dasar Sistem Operasi

<h4>Nama : Dandin Sesilia<h4>
<h4>NIM : 254107020142<h4>
<h4>Kelas : TI-1H<>

## Praktikum 2.1 Identifikasi CPU dan Memori
### Tujuan praktikum : memahami spesifikasi CPU dan kondisi memori pada server/VM.

Langkah - langkah :
1. Melihat informasi CPU :
<img width="900" height="400" alt="lscpu" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week2/images2/lscpu.jpeg?raw=true"/>
2. Melihat penggunaan memori :
<img width="800" height="350" alt="free-h" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week2/images2/free-h.jpeg?raw=true"/>
3. Melihat informasi DMI/BIOS :
<img width="900" height="400" alt="DMI" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week2/images2/DMI.jpeg?raw=true"/>

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
<img width="990" height="400" alt="daftar PCI" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week2/images2/lspci.jpeg?raw=true"/>
2. Lihat perangkat PCI & driver kernel yang digunakan :
<img width="990" height="450" alt="PCI dan Driver" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week2/images2/lspci-nnk.jpeg?raw=true"/>
3. Fokus pada NIC (Ethernet) untuk mencari modul driver :
<img widht="998" height="300" alt="Ethernet" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week2/images2/infoNIC.jpeg?raw=true"/>
4. Lihat perangkat USB :
<img width="850" height="300" alt="daftar USB" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week2/images2/lsusb.jpeg?raw=true"/>
5. Lihat topologi USB (tree) :
<img width="850" height="300" alt="topologi USB" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week2/images2/lsusb-t.jpeg?raw=true"/>

### Latihan 2.2
Temukan 1 perangkat PCI (misal NIC) dan tuliskan: Vendor:Device ID (angka
heksadesimal), nama driver/modul kernel, dan deskripsi singkat fungsinya.
    a. NIC
        Vendor:Device ID: 8086:100e
        Nama driver/modul kernel = e1000
        Fungsi = NIC digunakan sebagai jembatan antara komputer dan jaringan komputer. Vendor:Device ID berfungsi sebagai identitas dari perangkat keras yang tertanam dalam NIC. Sedangkan driver (software) berguna untuk penerjemah sistem operasi dan perangkat keras.

## Praktikum 2.3 Identifikasi Storage dan Filesystem
### Tujuan praktikum : memahami disk/partisi dan filesystem yang terpasang

Langkah - langkah :
1. Lihat daftar disk/partisi (block device dan filesystem) :
2. Tampilkan UUID dan tipe filesystem
3. Lihat mount point untuk root filesystem