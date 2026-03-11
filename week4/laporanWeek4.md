# Laporan Operasi File dan Struktur Direktori

#### Nama : Dandin Sesilia
#### NIM : 254107020142
#### Kelas : TI 1H

### Percobaan 1: Direktory
1. Melihat direktori HOME
> $ pwd
>
> $ echo $HOME
<img width="800" height="600" alt="melihat direktori HOME" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week4/images4/1.1.jpeg?raw=true"/>

2. Melihat direktori aktual dan parent direktori
> $ pwd
>
> $ cd .
>
> $ pwd
>
> $ cd ..
>
> $ pwd
>
> $ cd
<img width="800" height="500" alt="membuat parent direktori" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week4/images4/1.2.jpeg?raw=true"/>

3. Membuat satu direktori, lebih dari satu direktori atau sub direktori
> $ pwd
>
> $ mkdir A B C A/D A/E B/F A/D/A
>
> ls -l
>
> ls -l A
>
> ls -l A/D
<img width="800" height="400" alt="membuat sub direktori" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week4/images4/1.3.jpeg?raw=true"/>

4. Menghapus satu atau lebih direktori hanya dapat dilakukan pada direktori kosong dan hanya dapat dihapus oleh pemiliknya kecuali bila diberi izin aksesnya
> rmdir B (terdapat error karena direktori B tidak kosong)
>
> ls -l B
>
> rmdir B/F B
>
> ls -l B (terdapat error karena mencoba melihat isi direktori yang sudah tidak ada)
<img width="800" height="600" alt="menghapus direktori" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week4/images4/1.4.jpeg?raw=true"/>

5. Navigasi direktori dengan instruksi cd untuk pindah dari satu direktori ke direktori lain.
> $ pwd
>
> $ ls -l
>
> $ cd A
>
> $ pwd
>
> $ cd ..
>
> $ pwd
>
> $ cd /home/<user>/C
>
> $ pwd
>
> $ cd /<user>/C (terdapat error karena alamat direktori tidak lengkap, harusnya ada /home/ sebelum user)
>
> $ pwd
<img width="800" height="400" alt="navigasi direktori" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week4/images4/1.5.jpeg?raw=true"/>

### Percobaan 2: Manipulasi file
1. Perintah cp untuk mengcopy file atau seluruh direktori
> $ cat > contoh
>
> $ cp contoh contoh1
>
> $ ls -l
>
> $ cp contoh A
>
> $ ls -l A
>
> $ cp contoh contoh1 A/D
>
> $ ls -l A/D
<img widht="800" height="600" alt="copy file" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week4/images4/2.1.jpeg?raw=true"/>

2. Perintah mv untuk memindah file
> $ mv contoh contoh2
>
> $ ls -l
>
> $ mv contoh1 contoh2 A/D
>
> $ ls -l A/D
>
> mv contoh contoh1 C
>
> ls -l C
<img width="800" height="400" alt="move file" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week4/images4/2.2.jpeg?raw=true"/>

3.  Perintah rm untuk menghapus file
> $ rm contoh2
>
> $ ls -l
>
> $ rm -i contoh
>
> $ rm -rf A C
>
> $ ls -l
<img width="800" height="400" alt="hapus file" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week4/images4/2.2.jpeg?raw=true"/>

### Percobaan 3: Symbolic link
1. Membuat shortcut (file link)
> $ echo "Hallo apa kabar" > halo.txt
>
> $ ls -l
>
> $ ln halo.txt z
>
> $ ls -l
>
> $ cat z
>
> $ mkdir mydir
>
> $ ln z mydir/halo.juga
>
> $ cat mydir/halo.juga
>
> $ ln -s z bye.txt
>
> $ ls -l bye.txt
>
> $ cat bye.txt
<img width="700" height="600" alt="membuat shortcut" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week4/images4/3.jpeg?raw=true"/>

### Percobaan 4: Melihat isi file
> $ ls -l
>
> $ file halo.txt
>
> $ file bye.txt
<img width="800" height="400" alt="lihat isi file" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week4/images4/4.jpeg?raw=true"/>

### Percobaan 5: Mencari file
1. Perintah find
> $ find /home -name "*.txt" -print > myerror.txt
>
> $ cat myerror.txt
>
> $ find . -name "*.txt" -exec wc -l '{}' ';'
<img widht="800" height="300" alt="find" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week4/images4/5.1.jpeg?raw=true"/>

2. Perintah which
> $ which ls
<img width="800" height="500" alt="which" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week4/images4/5.2.jpeg?raw=true"/>

3. Perintah locate
> $ locate "*.txt"
<img width="800" height="300" alt="locate" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week4/images4/5.3.jpeg?raw=true"/>

### Percobaan 6: Mencari text pada file
> $ grep Hallo *.txt
<img width="800" height="500" alt="cari text" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week4/images4/5.4.jpeg?raw=true"/>

### Latihan
#### Latihan 1
> $ cd (pindah ke home direktori)
>
> pwd (melihat path direktori saat ini)
>
> $ ls -al (melihat semua file termasuk yg tersembunyi)
<img width="700" height="400" alt="perintah cd" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week4/images4/cd.jpeg?raw=true"/>

> $ cd . (pindah ke direktori aktif (tidak berubah))
>
> $ pwd 
>
> $ cd .. (pindah ke parent direktory (satu level diatas))
>
> $ pwd
>
> $ ls -al
<img width="700" height="500" alt="perintah cd ." src="https://github.com/sesilia-acc/OperationSystem/blob/main/week4/images4/cd1.jpeg?raw=true"/>

> $ cd ..
>
> $ pwd
>
> $ ls -al
<img width="800" height="400" alt="perintah cd .." src="https://github.com/sesilia-acc/OperationSystem/blob/main/week4/images4/cd2.jpeg?raw=true"/>

> $ cd /etc
>
> $ ls -al | more
<img width="800" height="500" alt="perintah cd /etc" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week4/images4/etc.jpeg?raw=true"/>

> $ cat passwd
<img width="700" height="500" alt="perintah cat passws" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week4/images4/passwd.jpeg?raw=true"/>

> $ cd - (kembali ke direktori sebelumnya)
>
> $ pwd
<img width="800" height="600" alt="" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week4/images4/cd-.jpeg?raw=true"/>

#### Latihan 2 & 3
menelusuri direktori bin dan sistem

> $ ls /bin
<img width="700" height="500" alt="direktori bin" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week4/images4/bin.jpeg?raw=true"/>

> $ ls /usr/bin
<img width="700" height="500" alt="direktori usr/bin" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week4/images4/usrbin.jpeg?raw=true"/>

> $ ls /sbin
<img width="700" height="500" alt="direktori sbin" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week4/images4/sbin.jpeg?raw=true"/>

> $ ls /tmp
<img width="700" height="500" alt="direktori tmp" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week4/images4/tmp.jpeg?raw=true"/>

> $ ls /boot
<img width="700" height="500" alt="direktori boot" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week4/images4/boot.jpeg?raw=true"/>

#### Latihan 4
Menelusuri directory /proc

> $ cat interrupts
<img width="800" height="500" alt="menampilkan isi interrupts" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week4/images4/interrupts.jpeg?raw=true"/>

> $ cat devices
<img width="800" height="500" alt="menampilkan isi devices" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week4/images4/devices.jpeg?raw=true"/>

> $ cat cpuinfo
<img width="800" height="650" alt="menampilkan isi cpuinfo" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week4/images4/cpuinfo.jpeg?raw=true"/>

> $ cat meminfo
<img width="800" height="650" alt="menampilkan isi meminfo" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week4/images4/meminfo.jpeg?raw=true"/>

> $ uptime
<img width="800" height="400" alt="menampilkan isi uptime" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week4/images4/uptime.jpeg?raw=true"/>

> /proc disebut *pseudo-filesystem* karena file didalamnya tidak benar benar tersimpan di hard disk saat menjalankan perintah cat di file /proc, sistem tidak membaca dari hard disk, namun kernel menulis isi data tersebut secara real time dari memori ke terminal.

#### Latihan 5 & 6
Ubah directory ke home user lain (salsabilawidyadhana)
<img width="800" height="500" alt="directory user lain" src=""/>

> tidak dapat masuk ke directory lain karena user tidak ada di sistem

kembali ke home directory sendiri
> cd~

#### Latihan 7 & 8
Membuat subdirectory work dan play
> $ mkdir work play
hapus subdirectory work
> $ rmdir work
<img width="800" height="400" alt="remove work" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week4/images4/mdanr.jpeg?raw=true"/>

#### Latihan 9 & 10
Copy file /etc/passwd ke directory home
> $ cp /etc/passwd ~
Pindahkan ke subdirectory play
> mv ~/passwd ~/play/
<img width="800" height="400" alt="latihan 9 & 10" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week4/images4/lat9&10.jpeg?raw=true"/>

#### Latihan 11 - 15
11. Membuat symbolic link ke tty dalam directory play
> $ cd ~/play
>
> $ ln -s /dev/tty terminal
12. Membuat file hello.txt
> $ echo "Hello World" > hello.txt
13. Copy isi file ke terminal
> $ cp hello.txt terminal
14.  Copy direktori play ke work menggunakan symbolic link
> $ cd ~ 
>
> $ ln -s play work 
15. Hapus direktori work (link-nya)
> $ rm work
<img width="800" height="400" alt="latihan 11 - 15e" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week4/images4/lat11-15.jpeg?raw=true"/>

### Laporan Resmi
a. Analisa tampilan
- ls            : Menampilkan daftar isi direktori secara halaman demi halaman.
- cd dan pwd    : Digunakan untuk navigasi.
- cat /proc/    : Menampilkan informasi real-time kernel.
- ln -s         : bertindak sebagai jalan pintas (shortcut) yang menunjuk ke lokasi lain.

b. Pohon struktur direktory berdasarkan percobaan 1.3
Berdasarkan instruksi mkdir ABCA/D A/E B/F A/D/A: / (Home)

├── A/

│ ├── D/

│ │ └── A/

│ └── E/

├── B/

│ └── F/

└── C/

c. 