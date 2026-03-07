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
<img width="900" height="500" alt="which" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week4/images4/5.1.jpeg?raw=true"/>

3. Perintah locate
> $ locate "*.txt"
<img width="800" height="300" alt="locate" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week4/images4/5.3.jpeg?raw=true"/>

### Percobaan 6: Mencari text pada file
> $ grep Hallo *.txt
<img width="900" height="500" alt="cari text" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week4/images4/5.4.jpeg?raw=true"/>