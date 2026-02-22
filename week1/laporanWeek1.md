# Laporan Praktikum Pengenalan Sistem Operasi dan Instalasi

<h4>Nama : Dandin Sesilia<h4>
<h4>NIM : 254107020142<h4>
<h4>Kelas : TI-1H<h4>

## LATIHAN!
### 1.10.1 Latihan Konseptual
#### Latihan 1.1
Jelaskan 5 fungsi utama sistem operasi dengan contoh konkret dari minimal 2
OS berbeda (Windows, macOS, atau Linux).
#### Jawaban :
Fungsi utama sistem operasi adalah
1. **Process management** : mengatur jalannya aplikasi yang sedang terbuka, memulai, menjadwalkan, dan mengakhiri proses, serta mengatur penggunaan CPU.
2. **Memory management** : mengatur alokasi RAM dan optimasi penggunaan memory
3. **File management** : mengatur cara data disimpan, dan mengelola hak akses keamanan file
4. **I/O management** : menjembatani komunikasi antara sistem dan hardware secara efisien
5. **Security & protection** : mengatur identitas pengguna, izin akses, dan enkripsi data untuk keamanan sistem
<h4>Contoh :<h4>
1. Windows : task Manager menampilkan proses yang berjalan dan penggunaan sumber daya
2. Linux : Perintah ps, top, dan htop untuk memantau proses

#### Latihan 1.2
Kapan sebaiknya menggunakan Windows vs Linux vs macOS? Analisis berdasarkan use case: gaming, development, server, creative work, dan enterprise.
#### Jawaban :
1. **Windows** : memiliki dukungan API DirectX dan kompatibilitas driver kartu grafis terluas, sehingga cocok untuk gaming. Karena terintegrasi Microsoft Office dan manajemen jaringan yang mudah dalam skala besar, windows juga cocok untuk enterprice. Windows juga menjadi alternatif kuat untuk rendering 3D dan penggunaan seluruh aplikasi Adobe Suite, sehingga juga rekomend untuk creative work profesional.
2. **Linux** : OS yang paling dominan untuk server karena stabilitasnya tinggi, gratis, dan efisien dalam pengelolaan layanan menggunakan perintah seperti systemctl, sangat baik untuk case server. Kemudahan manajemen paket serta akses terminal yang kuat, linux juga rekomend untuk case development khususnya pengembangan backend dan devOps.
3 **MacOS** : tersedia aplikasi eksklusif seperti Final Cut Pro dan telah difasilitasi layar yang teroptimasi, macOS cocok untuk creative work seperti desain grafis, dan editing. Karena berbasis Unix, macOS menjadi pilihan pengembangan web dengan tampilan grafis yang elegan.

### 1.10.2 Latihan Praktikal
#### Latihan 1.3
Install Ubuntu Server 22.04 LTS di VirtualBox dengan langkah berikut :
1. Download Ubuntu Server ISO dari website resmi
<img width="800" height="500" alt="download ubuntu" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week1/images1/downloadubuntu.jpeg?raw=true"/>
2. Create VM baru di VirtualBox (RAM: 2GB, Disk: 25GB)
<img width="800" height="400" alt="create VM" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week1/images1/createvm.jpeg?raw=true"/>
3. Install dengan automatic partitioning (guided)
<img width="700" height="800" alt="intall partition" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week1/images1/installpartition.jpeg?raw=true"/>
4. Buat user account dengan password yang kuat
5. Reboot dan login ke sistem
<img width="800" height="400" alt="reboot" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week1/images1/reboot.jpeg?raw=true"/>

#### Latihan 1.4
Setelah instalasi Ubuntu Server, lakukan tasks berikut:
1. Update package list: sudo apt update
<img width="600" height="400" alt="update package" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week1/images1/updatepackages.jpeg?raw=true"/>
2. Upgrade packages: sudo apt upgrade
<img width="800" height="400" alt="upgrade package" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week1/images1/upgradepackages.jpeg?raw=true"/>
3. Install neofetch: sudo apt install neofetch
<img width="600" height="400" alt="install neofetch" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week1/images1/installneofetch.jpeg?raw=true"/>
4. Jalankan neofetch dan screenshot hasilnya
<img width="800" height="400" alt="jalankan neofetch" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week1/images1/runneofetch.jpeg?raw=true"/>
5. Check disk usage dengan df-h
<img width="800" height="400" alt="disk usage" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week1/images1/diskusage.jpeg?raw=true"/>
6. Check memory dengan free-h
<img width="800" height="400" alt="memory usage" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week1/images1/memousage.jpeg?raw=true"/>

#### Latihan 1.5
Eksplorasi sistem yang baru diinstall :
1. Tampilkan informasi OS: cat /etc/os-release
<img width="700" height="400" alt="informasi OS" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week1/images1/osinfo.jpeg?raw=true"/>
2. Tampilkan versi kernel: uname-r
<img width="900" height="500" alt="versi kernel" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week1/images1/kernelversion.jpeg?raw=true"/>
3. List partisi: lsblk
<img width="800" height="400" alt="list partisi" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week1/images1/listpartisi.jpeg?raw=true"/>
4. Check network connectivity: ping-c 4 google.com
<img width="800" height="400" alt="network connectivity" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week1/images1/networkconnect.jpeg?raw=true"/>
5. Install dan jalankan htop untuk melihat resource usage
<img width="850" height="500" alt="running htop" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week1/images1/htop.jpeg?raw=true"/>

### 1.10.3 Latihan Refleksi
#### Latihan 1.6
Ceritakan pengalaman Anda dengan sistem operasi:
1. Sistem operasi apa yang Anda gunakan sehari-hari? (Windows, macOS, Linux, atau lainnya)
2. Berapa lama Anda menggunakan sistem operasi tersebut?
3. Apa yang Anda sukai dari sistem operasi tersebut?
4. Apa tantangan atau masalah yang pernah Anda hadapi? pengalaman Anda.
5. Apakah Anda pernah menggunakan sistem operasi lain? Bandingkan
6. Setelah mempelajari bab ini, apakah ada sistem operasi lain yang ingin Anda coba?Mengapa?
#### Jawaban :
Sistem operasi yang saya gunakan sehari-hari adalah Windows. Kalau dihitung-hitung, saya sudah menggunakan Windows kurang lebih selama 5 tahun terakhir ini. Alasannya sebenarnya cukup sederhana, yaitu karena dari awal saya belajar menggunakan komputer, perangkat yang saya pakai sudah memiliki sistem operasi Windows. Jadi, secara tidak langsung saya merasa jauh lebih familiar dan nyaman di sana. Menurut saya, Windows itu sistem operasi yang sangat user dan pemula friendly. Kita tidak perlu pusing memikirkan teknis yang mendalam saat pertama kali mengoperasikan komputer, jadi kesusahan di awal bisa sangat diminimalisir.

Yang paling saya sukai dari Windows adalah kemudahannya yang serba visual; kita hanya tinggal klik-klik ikon saja untuk membuka aplikasi atau mengubah pengaturan. Rasanya jauh lebih praktis dan cepat buat orang yang tidak mau ribet. Tapi, bukan berarti Windows itu sempurna. Ada satu hal yang paling saya tidak suka, yaitu sewaktu Windows tiba-tiba minta update paksa di waktu yang tidak tepat. Selain itu, saya juga pernah merasakan momen menyebalkan saat laptop tiba-tiba hang dan performanya jadi lemot banget, padahal saya lagi butuh cepat. Masalah-masalah kecil seperti ini seringkali bikin emosi, tapi ya mau bagaimana lagi, karena sudah terlanjur nyaman dengan kemudahannya.

Nah, di perkuliahan ini saya mulai mencoba menggunakan sistem operasi Linux, dan jujur saja ternyata Linux itu lebih susah dari yang saya kira sebelumnya. Bedanya terasa sangat jauh dengan Windows. Di Linux, kita harus menghafalkan banyak sekali perintah untuk menjalankan suatu proses, berbeda dengan Windows yang modal ketik sedikit atau klik saja sudah jalan. Awalnya saya sempat merasa malas karena harus bolak-balik melihat catatan perintah, tapi saya sadar kalau pelan-pelan ini akan mulai terbiasa juga.

Setelah saya pelajari lebih dalam di bab ini, sepertinya sistem operasi Linux memang jauh lebih recommended digunakan untuk kebutuhan development atau koding. Linux terasa lebih transparan karena kita bisa melihat apa yang sedang berjalan di latar belakang secara detail lewat terminal. Meskipun kurva belajarnya lumayan menanjak di awal, kontrol yang diberikan Linux buat mengatur memori dan layanan sistem terasa lebih oke. Jadi, walaupun sekarang masih sering bingung, saya rasa ke depannya saya akan lebih sering pakai Linux supaya kodingan saya jadi lebih rapi dan profesional.