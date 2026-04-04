# LAPORAN PRAKTIKUM MANAGEMEN PROSES

#### Nama : Dandin Sesilia
#### NIM : 254107020142
#### Kelas : TI 1H

## Praktikum 6.1 Melihat Proses & Thread
1. Tampilkan semua proses yang berjalan:
> ps aux
<img widht="700" height="400" alt="menampilkan semua proses" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week6/images6/allpro.jpeg?raw=true"/>

2. Tampilkan proses beserta thread-nya, dapat dilihat pada kolom LWP (Light Weight Process ID):
> ps aux -L
<img widht="700" height="500" alt="menampilkan proses dengan thread" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week6/images6/allpro.jpeg?raw=true"/>

3. Lihat PID shell aktif dan detail prosesnya:
> echo $$
>
> ps -p $$ -f
<img widht="700" height="600" alt="Detail proses shell saat ini" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week6/images6/shell.jpeg?raw=true"/>

4. Lihat hierarki proses secara visual:
> pstree -p
<img widht="700" height="700" alt="Pohon proses" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week6/images6/pstree.jpeg?raw=true"/>

### Latihan 6.1
Jalankan ps aux dan amati outputnya:
1. Berapa total proses yang berjalan? Proses apa yang memiliki PID terkecil?. >> Total proses yang berjalan adalah 162 proses, dapat diketahui dengan melakukan perintah ps aux | wc -L. Proses yang memiliki PID terkecil adalah proses [kworker/R-crypt].

2. Jalankan pstree-p dan temukan proses bash Anda. Proses apa yang menjadi induk (PPID) dari bash tersebut?. >> Proses yang menjadi induk (PPID) dari bash adalah login (22610).

3. Bandingkan output ps aux dan ps aux-L. Apa perbedaan yang Anda lihat?. >> Ps aux menampilkan semua proses berdasarkan PID, artinya adalah jika sebuah aplikasi memiliki 10 thread, maka ps aux akan menampilkannya hanya dalam 1 baris saja. Sedangkan ps aux -L menampilkan setiap thread individual berdasarkan LWP, artinya jika sebuah aplikasi memiliki 10 thread, maka akan ditampilkan 10 baris tersebut.

## Praktikum 6.2 Mengamati Siklus Hidup Proses
1. Buat proses di background dan amati kondisinya:
> sleep 60 &
>
> ps aux | grep sleep
<img width="700" height="500" alt="Mengamati kondisi proses" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week6/images6/sleep.jpeg?raw=true"/>

2. Amati perubahan exit code dari perintah yang berhasil dan gagal:
> ls /tmp
>
> echo "Sukses: $?"
>
> ls /direktori-tidak-ada
>
> echo "Gagal: $?"
<img width="700" height="500" alt="Mengamati exit code" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week6/images6/exitcode.jpeg?raw=true"/>

### Latihan 6.2
1. Jalankan sleep 120 & dan amati kolom STAT pada ps aux. Kondisi apa yang ditampilkan? Mengapa proses sleep berada di kondisi tersebut?. >> Kondisi yang ditampilkan pada STAT adalah S yang berarti proses sleep sedang berlangsung di background dan menunggu waktu berakhir. Karena perintah menggunakan &, maka user tetep dapat mengetik di terminal meskipun ada proses yang sedang berlangsung.

2. Jalankan beberapa perintah yang berhasil dan yang gagal, lalu catat exit code masing-masing. Pola apa yang Anda temukan?. >> Exit code berhasil adalah 0, exit code gagal ada bermacam - macam. Exit code 1 untuk general error, exit code 2 untuk kesalahan fatal, exit code 127 untuk perintah yang tidak dikenali. Jadi, angka apapun yang muncul selain 0 itu adalah gagal. 
<img width="700" height="400" alt="Contoh exit code" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week6/images6/example.jpeg?raw=true"/>

## Praktikum 6.3 Mengatur Prioritas Proses
1. Jalankan proses dengan prioritas rendah:
> nice -n 10 sleep 300 &
2. Verifikasi nilai nice pada kolom NI:
> ps aux | grep sleep
<img width="700" height="500" alt="Melihat nilai nice" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week6/images6/nice10.jpeg?raw=true"/>

3. Ubah nilai nice proses yang sudah berjalan:
> renice -n 15 -p <PID>
>
> ps -p <PID> -o pid,ni,cmd
<img width="700" height="500" alt="Mengubah nice dgn renice" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week6/images6/renice.jpeg?raw=true"/>

4. Bersihkan proses percobaan:
> kill %1

### Latihan 6.3
1. Jalankan nice-n 5 sleep 200 & dan verifikasi nilai NI-nya dengan ps.

2. Ubah nilai nice menjadi 10 menggunakan renice, lalu verifikasi kembali.

3. Coba ubah nilai nice menjadi -5 tanpa sudo. Apa yang terjadi? Mengapa Linux membatasi hal ini untuk user biasa?
<img width="700" height="500" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week6/images6/lat3.jpeg?raw=true"/>
>> Jika nilai nice diubah menjadi -5 tanpa sudo yang terjadi adalah permission denied. Linux membatasi hal ini untuk mencegah user biasa berlaku curang dengan menaikkan prioritas proses mereka sendiri

## Praktikum 6.4 Mengirim Sinyal ke Proses
1. Buat proses percobaan:
> sleep 500 &
>
> sleep 600 &
>
> sleep 700 &
>
> ps aux | grep -v grep | grep sleep
<img width="700" height="500" alt="Membuat proses percobaan" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week6/images6/trialsleep.jpeg?raw=true"/>

2. Hentikan satu proses dengan SIGTERM dan verifikasi:
> kill <PID-sleep-500>
>
> ps aux | grep -v grep | grep sleep
<img width="700" height="500" alt="Menghentikan proses dgn sigterm" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week6/images6/sigterm.jpeg?raw=true"/>

3. Jeda dan lanjutkan proses dengan SIGSTOP/SIGCONT:
> kill -SIGSTOP <PID-sleep-600>
>
> ps aux | grep sleep
>
> kill -SIGCONT <PID-sleep-600>
>
> ps aux | grep sleep
<img width="700" height="500" alt="Menjeda & melanjutkan proses" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week6/images6/sigstop.jpeg?raw=true"/>

4. Hentikan semua proses sleep sekaligus:
> pkill sleep
<img width="800" height="600" alt="Menghentikan semua sleep" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week6/images6/sigstop.jpeg?raw=true"/>

### Latihan 6.4
1. Jalankan sleep 400 &, kirim SIGSTOP, dan amati perubahan kolom STAT. Kondisi apa yang muncul?. >> Saat dikirim sinyal SIGSTOP, pada Kolom STAT terdapat huruf T yang seharusnya adalah huruf S atau S+. Kondisi ini terjadi karena SIGSTOP adalah perintah untuk menjeda proses.

2. Kirim SIGCONT dan verifikasi proses kembali berjalan.

3. Hentikan proses dengan SIGTERM lalu verifikasi sudah tidak ada. Kapan Anda memilih SIGKILL daripada SIGTERM?. >> SIGKILL digunakan sebagai langkah terakhir jika suatu aplikasi tidak merespon perintah apapun termasuk SIGTERM. SIGKILL juga bisa digunakan jika user ingin langsung menghentikan suatu proses tanpa ingin menyimpan data yang sedang dikerjakan.
<img width="700" height="500" alt="Latihan 6.4" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week6/images6/lat64.jpeg?raw=true"/>

## Praktikum 6.5 Manajemen Job Foreground dan Background
1. Jalankan tiga job di background:
> sleep 200 &
> 
> sleep 300 &
>
> sleep 400 &
>
> jobs
<img width="700" height="500" alt="3 job background" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week6/images6/buatjob.jpeg?raw=true"/>

2. Bawa job pertama ke foreground, jeda, lalu kembalikan ke background:
> fg %1
>
> ctrl Z untuk jeda
>
> bg %1
>
> jobs
<img width="700" height="500" alt="Pindah job fg ke bg" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week6/images6/pindahjob.jpeg?raw=true"/>

3. Hentikan semua job:
> kill %1 %2 %3
>
> jobs
<img width="800" height="600" alt="Memberhentikan semua job" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week6/images6/killjob.jpeg?raw=true"/>

### Latihan 6.5
1. Jalankan top di foreground. Apa yang terjadi di terminal?. >> Terminal mengetik terus menerus karena memperbarui daftar prose, penggunaan CPU, dan RAM secara realtime.

2. Tekan Ctrl+Z dan cek statusnya dengan jobs. Kondisi apa yang ditampilkan?. >> Proses dihentikan sementara karena ctrl+Z adalah perintah SIGSTOP.

3. Pindahkan ke background dengan bg. Apakah top dapat berjalan dengan baik di background? Mengapa?. >> Top awalnya dapat berjalan di background, ditandai dengan simbol &. Namun, sesaat kemudian proses stopped karena perintah Top membutuhkan terminal untuk mengetik secara realtime.

4. Kembalikan ke foreground dengan fg, lalu keluar dengan q.
<img width="700" height="500" alt="Latihan 6.5" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week6/images6/lat5.jpeg?raw=true"/>

## Praktikum 6.6 Pemantauan Proses
1. Temukan proses dengan penggunaan CPU dan memori tertinggi:
> ps aux --sort=-%cpu | head -10
>
> ps aux --sort=-%mem | head -10
<img width="700" height="500" alt="Proses resource tertinggi" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week6/images6/eksplorasitop.jpeg?raw=true"/>

2. Jalankan top dan eksplorasi shortcut-nya:
> top
<img width="700" height="500" alt="Eksplorasi top" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week6/images6/eksplorasitop.jpeg?raw=true"/>

3. Instal dan jalankan htop:
> sudo apt install -y htop
>
> htop
<img width="700" height="500" alt="Menggunakan htop" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week6/images6/eksplorasitop.jpeg?raw=true"/>

### Latihan 6.6
1. Gunakan ps aux–sort=%mem untuk menemukan proses yang menggunakan memori paling banyak di VM Anda. Proses apa itu?. >> Proses yang menggunakan memori paling banyak (2.0) adalah proses firmware update daemon

2. Di dalam top (tekan 1), Apa yang berubah pada tampilan? Mengapa informasi ini berguna?. >> Tampilan meng-highlight beban CPU paling berat. Informasi ini berguna untuk mengetahui dan memantau beban setiap core CPU secara terpisah.

3. Di dalam htop, navigasikan ke proses sshd menggunakan tombol panah. Tekan F9 dan amati opsi sinyal yang tersedia.
<img width="700" height="500" alt="Eksplorasi htop" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week6/images6/eksplorasitop.jpeg?raw=true"/>

## Latihan!
### Latihan 6A
**Eksplorasi Proses Sistem**
1. Jalankan ps aux–forest dan temukan proses dengan PID 1. Apa nama dan fungsi proses tersebut dalam sistem Linux modern?. >> Nama prosesnya adalah /sbin/init, fungsinya sebagai pengelola utama seluruh ekosistem sistem operasi , termasuk service manager, pengumpul log sistem, dll. 
<img width="700" height="500" alt="PID 1" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week6/images6/6A1.jpeg?raw=true"/>

2. Hitung berapa proses yang dimiliki oleh user root dan berapa yang dimiliki oleh user Anda. Mengapa root memiliki lebih banyak proses?. >> Proses yang dimiliki root ada 86 proses, user memiliki 17 proses. Root memiliki lebih banyak proses karena root mengelola segala aspek sistem operasi agar tidak bisa dikendalikan oleh user biasa.
<img width="700" height="500" alt="Hitung proses" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week6/images6/6A2.jpeg?raw=true"/>

3. Temukan semua proses yang berada dalam kondisi S. Mengapa sebagian besar proses di sistem berada dalam kondisi ini?. >> Sebagian proses berada dalam kondisi S karena proses menunggu untuk digunakan agar tidak memakan CPU terlalu banyak. Proses yang tidak digunakan berada dalam kondisi sleep (S).
<img width="700" height="500" alt="Kondisi S" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week6/images6/6A2.jpeg?raw=true"/>


### Latihan 6B
**Simulasi Manajemen Job**
1. Jalankan tiga perintah sleep dengan durasi 100, 200, dan 300 detik di background. Verifikasi ketiganya dengan jobs.
2. Bawa job kedua ke foreground, jeda dengan Ctrl+Z , lalu kembalikan ke background dengan bg.
3. Hentikan job pertama dengan kill %1. Tampilkan kembali daftar job. Berapa job yang tersisa?. >> Job pertama tidak ditemukan karena telah diselesai dikerjakan, tersisa job 2 dan 3.
<img width="700" height="500" alt="Manajemen Job" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week6/images6/6B.jpeg?raw=true"/>

### Latihan 6C
**Prioritas dan Sinyal**
1. Jalankan dua proses sleep: satu dengan nice +5 dan satu dengan nice +15. Verifikasi nilai NI keduanya dengan ps.
2. Gunakan renice untuk mengubah nice proses pertama menjadi +10. Proses mana yang kini lebih diprioritaskan scheduler?
3. Kirim SIGSTOP ke salah satu proses, verifikasi kondisi T-nya, lalu kirim SIGCONT. Akhiri semua proses percobaan dengan pkill sleep.
<img width="700" height="600" alt="Prioritas dan sinyal" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week6/images6/6C.jpeg?raw=true"/>
