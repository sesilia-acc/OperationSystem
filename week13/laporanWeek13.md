# LAPORAN PRAKTIKUM BACKUP DAN PEMULIHAN SISTEM

#### Nama   : Dandin Sesilia
#### NIM    : 254107020142
#### Kelas  : TI 1H

## Praktek 12.1: Rencanakan Strategi Backup
1. Buat direktori struktur data simulasi yang akan di-backup:
<img width="700" height="500" alt="Meyiapkan direktori" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week13/image13/direktori121.png?raw=true"/>

> total file di simulasi ini ada 3 file.

2. Buat dokumen rencana backup menggunakan heredoc:
<img width="700" height="500" alt="Rencana backup" src=" https://github.com/sesilia-acc/OperationSystem/blob/main/week13/image13/rencanabackup121.png?raw=true"/>

3. Hitung estimasi kebutuhan ruang backup untuk 30 hari:
<img width="700" height="500" alt="Estimasi kebutuhan" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week13/image13/estimasikebutuhan121.png?raw=true"/>

> perbandingan kebutuhan ruang strategi full+incremental dibandingkan jika full
>
> backup dilakukan setiap hari (fullx30) adalah sekitar 21,3% dari total ruang
>
> yang digunakan oleh strategi full backup.

### Tantangan
Buat file teks berisi rencana backup yang lebih lengkap menggunakan teknik heredoc dari Bab 3. Rencana harus mencantumkan: jadwal harian dan mingguan, estimasi ruang untuk setiap jenis backup, lokasi penyimpanan, dan prosedur pengujian restore Simpan ke file rencana-lengkap.txt. Kemudian gunakan teknik redirection dan pipeline dari Bab 3 untuk menghitung berapa baris rencana yang kamu tulis.
<img width="700" height="500" alt="tantangan praktek 12.1" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week13/image13/tantangan121.png?raw=true"/>

## Praktek 12.2: Sinkronisasi Direktori dengan rsync
1. Jalankan sinkronisasi pertama:
<img width="700" height="500" alt="Sinkronisasi pertama" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week13/image13/sync122.png?raw=true"/>

> Dry run hanya sebagai simulasi untuk menampilkan daftar file yang akan diproses tanpa mengubah data sama sekali
>
> Eksekusi sebenarnya (rsync -av) benar-benar mentransfer data, membuat folder baru, dan mengubah kapasitas file.

2. Tambahkan file baru, hapus satu file, lalu amati efek–delete:
<img width="700" height="500" alt="Amati efek delete" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week13/image13/rsync122.png?raw=true"/>

> app.log ikut terhapus dari tujuan karena perintah --delete memaksa menghapus file apapun di folder tujuan.
>
> baru.txt muncul karena sebelum sinkronisasi telah membuat file baru, sehingga waktu rsync file sudah terbaca.

3. Buat snapshot pertama dan kedua menggunakan–link-dest:
<img width="700" height="500" alt="Buat snapshot dengan hard link" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week13/image13/snapshot122.png?raw=true"/>

4. Verifikasi hard link dengan membandingkan inode:
<img width="700" height="500" alt="Verifikasi hard link" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week13/image13/hardlink122.png?raw=true"/>

> Nomor inode untuk file laporan.txt di snap-1 dan snap-2 tidak sama, sehingga linux membaca sbg file terpisah.

5. Bersihkan snapshot setelah praktek

### Tantangan
Buat skrip Bash (mengacu ke Bab 7) bernama rsync-backup.shdidirektori lab yang menjalankan rsync dari direktori data-sumber/ ke direktori bernama sesuai tanggal hari ini dalam format YYYY-MM-DD. Gunakan tee dari Bab 3 untuk menulis output rsync ke layar sekaligus ke file log bernama backup-TANGGAL.log. Jadikan skrip ini executable dengan chmod +x dan jalankan untuk memverifikasi hasilnya.
<img width="700" height="500" alt="Tantangan praktek 12.2" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week13/image13/tantangan122.png?raw=true"/>

## Praktek 12.3: Buat Arsip Backup dan Verifikasi Integritasnya
1. Buat arsip full backup dan simpan checksumnya:
<img width="700" height="500" alt="Pembuatan cheksum" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week13/image13/arsiptar123.png?raw=true"/>

> File arsip 369 bytes, file sumber 32.768 bytes. File arsip berhasil menyusut karena tar -czf mengompresi gzip.

2. Periksa isi arsip dan coba ekstrak satu file:
<img width="700" height="500" alt="Periksa arsip tar" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week13/image13/periksatar123.png?raw=true"/>

3. Verifikasi integritas arsip menggunakan checksum:
<img width="700" height="500" alt="Verifikasi integritas" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week13/image13/verifinteg123.png?raw=true"/>

> Pesan OK itu file backup dijamin aman dan file arsip yang ada sekarang sama persis saat pertama kali dibuat.

4. Buat arsip incremental setelah menambahkan file baru:
<img width="700" height="500" alt="Backup incremental" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week13/image13/backupincrement123.png?raw=true"/>

> Ukuran full snap 449 bytes, ukuran incremental 424 bytes, penghematan tidak terlihat signifikan karena folder kecil

### Tantangan
Buat arsip incremental sesi kedua. Tambahkan beberapa file baru ke data-sumber/dokumen/ dan ubah isi app.conf. Kemudian jalankan tar dengan file snapshot yang sama untuk menghasilkan incremental backup kedua. Bandingkan ukuran ketiga arsip (full, incr-1, incr-2). Kemudian verifikasi isi setiap arsip menggunakan tar-tzf untuk memastikan setiap arsip hanya mengandung file yang sesuai dengan jenisnya.
<img width="700" height="500" alt="tantangan praktek 12.3" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week13/image13/tantangan123.png?raw=true"/>

## Praktek 12.4: Jadwalkan Skrip Backup Otomatis
1. Buat skrip backup yang menggunakan rsync dengan logging:
<img width="700" height="500" alt="Skrip backup" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week13/image13/skripbackup124.png?raw=true"/>

2. Uji skrip secara manual sebelum mendaftarkannya ke cron:
<img width="700" height="500" alt="Uji skrip" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week13/image13/runskrip124.png?raw=true"/>

> Ya, log sudah mencatat timestamp dan direktori dengan benar dan konsisten.

3. Daftarkan skrip ke crontab untuk berjalan setiap 2 menit(untuk keperluan pengujian):
<img width="700" height="500" alt="Daftarkan ke crontab" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week13/image13/daftarcrontab124.png?raw=true"/>

4. Tunggu beberapa menit lalu verifikasi cron telah menjalankan backup:
<img width="700" height="500" alt="Execute cron" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week13/image13/executecron124.png?raw=true"/>

> Ada 4 direktori backup yg berhasil dibuat dengan timestamp sesuai waktu eksekusi.

5. Bersihkan crontab dan direktori:

### Tantangan
Jadwalkan skrip rsync-backup.sh dari challengebox Praktek 12.2 agar berjalan setiap hari pukul 02:00 menggunakan crontab. Tambahkan ke skrip tersebut agar output rsync disimpan ke/var/log/backup.log menggunakan teknik tee dari Bab3(sehingga sekaligus tercetak di terminal saat dijalankan manual dan tersimpan ke log). Tulis cron expression yang tepat dan jelaskan setiap field-nya.
<img width="700" height="500" alt="tantangan praktek 12.4" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week13/image13/tantangan124.png?raw=true"/>

## Praktek 12.5: Simulasi Pemulihan dari Backup
1. Siapkan data sumber dan buat backup sebagai persiapan:
<img width="700" height="500" alt="Siapkan data awal" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week13/image13/dataawal125.png?raw=true"/>

2. Simpan checksum file - file penting untuk verifikasi nanti:
<img width="700" height="500" alt="Simpan cheksum file sumber" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week13/image13/cheksum125.png?raw=true"/>

3. Simulasikan kehilangan data: hapus beberapa file secara sengaja:
<img width="700" height="500" alt="Simulasi kehilangan data" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week13/image13/simulasi125.png?raw=true"/>

4. Pulihkan file yang hilang dari arsip tar ke direktori sementara:
<img width="700" height="500" alt="Restor dari tar ke direktori sementara" src=""/>

5. Pulihkan file konfigurasi dari snapshot rsync:
<img width="700" height="500" alt="Restore dari snapshot rsync" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week13/image13/restorersync125.png?raw=true"/>

6. Verifikasi integritas setelah pemulihan:
<img width="700" height="500" alt="Verifikasi cheksum setelah restore" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week13/image13/verifcheksum125.png?raw=true"/>

> Ya, semua cheksum sudah menunjukkan status OK.

7. Bersihkan seluruh direktori lab:

### Tantangan
Perpanjang skenario pemulihan: hapus seluruh direktori data-sumber/konfigurasi/ sekaligus (bukan hanya satu file). Kemudian pulihkan seluruh direktori tersebut dari snapshot menggunakan rsync dengan arah transfer yang dibalik (sumber adalah snapshot, tujuan adalah direktori yang rusak). Verifikasi hasil pemulihan dengan membandingkan checksum seluruh isi direktori menggunakan find dan md5sum. Catat perbedaan waktu antara restore satu file dan restore satu direktori penuh.
<img width="700" height="500" alt="" src=""/>

## Latihan
### Latihan 12.1: Implementasi Sistem Backup Lengkap
Rancang dan implementasikan sistem backup untuk direktori simulasi.
1. Buat struktur direktori simulasi dengan minimal 10 file yang tersebar di tiga subdirektori: dokumen/ konfigurasi/, dan media/.
<img width="700" height="500" alt="struktur direktori" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week13/image13/lat121a.png?raw=true"/>

2. Buat skrip backup-harian.sh yang menggunakan rsync dengan–link-dest untuk membuat snapshot harian. Skrip harus mencatat log dengan timestamp ke backup-harian.log.
<img width="700" height="500" alt="skrip backup harian" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week13/image13/lat121b.png?raw=true"/>

3. Buat skrip backup-mingguan.sh yang menggunakan tar-czf untuk membuat arsip terkompresi. Skrip harus membuat checksum MD5 dari setiap arsip yang dibuat.
<img width="700" height="500" alt="skrip backup mingguan" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week13/image13/lat121c.png?raw=true"/>

4. Daftarkan keduanya ke crontab dengan jadwal yang berbeda. Jalankan masing-masing secara manual dan verifikasi log dan output yang dihasilkan.
<img width="700" height="500" alt="daftar crontab" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week13/image13/lat121d.png?raw=true"/>
<img width="700" height="500" alt="run crontab" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week13/image13/lat121d1.png?raw=true"/>

5. Simulasikan kehilangan file dan lakukan restore dari kedua jenis backup. Dokumentasikan langkah - langkah restore dan waktu yang dibutuhkan.
<img width="700" height="500" alt="simulasi kehilangan" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week13/image13/lat121e.png?raw=true"/>

### Latihan 12.2: Analisis Kompresi dan Performa Backup
Analisis trade-off antara kecepatan dan rasio kompresi.
1. Buat direktori dengan tiga jenis file: teks biasa (10 file .txt masing-masing 100 baris), file konfigurasi .conf, dan file biner simulasi menggunakan dd if=/dev/urandom of=biner.bin bs=1M count=5.
2. Buat tiga arsip dari direktori yang sama menggunakan gzip (-z), bzip2 (-j), dan xz (-J). Ukur waktu setiap proses menggunakan time.
3. Bandingkan ukuran ketiga arsip dengan ls-lh dan hitung rasio kompresi masing-masing terhadap ukuran asli.
4. Buat tabel di file analisis-kompresi.txt yang merangkum: jenis kompresi, waktu kompres, ukuran hasil, dan rasio kompresi.
5. Berdasarkan data tersebut, rekomendasikan kompresi yang paling tepat untuk: backup harian otomatis, arsip jangka panjang, dan backup file biner. Berikan alasan untuk setiap rekomendasi.
<img width="700" height="500" alt="latihan 12.2" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week13/image13/lat122.png?raw=true"/>

> Untuk backup harian gunakan gzip, karena berjalan secara berkala dan otomatis di latar belakang sistem produksi.
>
> Untuk arsip jangka panjang gunakan Xz, karena optimal untuk menghemat kapasita memori jangka panjang.
>
> Untuk backup file biner gunakan gzip/tar, karena idak memiliki pola perulangan bit yang bisa dikompresi

### Latihan 12.3: Disaster Recovery Drill
Lakukan simulasi pemulihan bencana secara menyeluruh.
1. Buat direktori “produksi” dengan struktur lengkap: file konfigurasi, dokumen, dan skrip. Buat backup penuh menggunakan tar dan simpan checksumnya.
2. Dokumentasikan kondisi awal: daftar file, ukuran, dan checksum semua file menggunakan find dan md5sum.
3. Simulasikan bencana: hapus seluruh direktori produksi dengan rm-rf.
4. Catat waktu mulai pemulihan, lakukan restore lengkap dari backup, dan catat waktu selesai. Hitung RTO aktual. 
5. Verifikasi semua file pulih dengan benar menggunakan checksum yang disimpan di langkah 2.
6. Bandingkan RTO aktual dengan target yang kamu tentukan. Jika lebih lama, identifikasi bottleneck dan usulkan cara mempercepatnya
<img width="700" height="500" alt="latihan 12.3" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week13/image13/lat122.png?raw=true"/>

> Target RTO < 5 detik, RTO aktual 0.03 detik
>
> RTO Aktual lebih cepat daripada batas target, sehingga sistem pemulihan bencana dinilai sukses.
