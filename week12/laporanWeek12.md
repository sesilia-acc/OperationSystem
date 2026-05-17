# LAPORAN PRAKTIKUM MANAJEMEN SERVICE

#### Nama   : Dandin Sesilia
#### NIM    : 254107020142
#### Kelas  : TI 1H

## Praktikum 12.1 - Amati Layanan Aktif Saat Boot
1. Lihat semua layanan yang sedang berjalan
<img width="700" height="400" alt="layanan yg sedang berjalan" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week12/image12/layananrealtime.png?raw=true"/>

2. Lihat semua unit service yang ada (aktif maupun tidak)
<img width="700" height="400" alt="semua unit service" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week12/image12/unitservice.png?raw=true"/>

3. Analisis waktu boot dan temukan layanan paling lambat
<img width="700" height="400" alt="analisis waktu boot" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week12/image12/layananlambat.png?raw=true"/>

### Tantangan
Identifikasi 3 layanan dengan waktu inisialisasi terlama menggunakan systemd-analyze blame. Gunakan pipeline dari Bab 3 (| sort -rh | head -3) untuk mempercepat pencariannya. Untuk setiap layanan, cari tahu fungsinya dengan systemctl cat nama-layanan Tuliskan nama layanan, waktu inisialisasinya, dan penjelasan singkat fungsinya.
<img width="500" height="400" alt="tantangan praktikum 12.1" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week12/image12/tantangan121.png?raw=true"/>

> Layanan dbus.service 999ms, sebagai media komunikasi antar proses di linux.
>
> Layanan systemd-resolved.service 944ms, memastikan aplikasi di komputer bisa terhubung
>
> ke internet dengan query DNS.
>
> Layanan sysstat.service 932ms, mengumpulkan data performa sistem di latar belakang.

## Praktikum 12.2 - Kelola Layanan SSH
1. Periksa status SSH secara menyeluruh.
<img width="700" height="400" alt="periksa keseluruhan SSH" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week12/image12/statusSSH.png?raw=true"/>

2. Lakukan restart dan pantau perubahannya.
<img width="700" height="400" alt="restart SSH" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week12/image12/restartSSH.png?raw=true"/>

3. Lihat dependensi SSH
<img width="700" height="400" alt="lihat dependensi SSH" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week12/image12/dependenciesSSH.png?raw=true"/>

4. Cek semua unit yang gagal di sistem.
<img width="700" height="400" alt="cek unit gagal" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week12/image12/gagalSSH.png?raw=true"/>

### Tantangan
Buat skrip Bash (referensi Bab 7) bernama cek-layanan.sh yang memeriksa status daftar layanan dari sebuah berkas teks. Berkas teks daftar-layanan.txt berisi satu nama layanan per baris (isi minimal: ssh, cron, rsyslog). Skrip membaca setiap nama layanan,memeriksa statusnya dengan systemctl is-active, lalu menulis laporan ke berkas laporan-layanan.log dengan format: [TANGGAL] nama-layanan: ACTIVE/INACTIVE. Gunakan date untuk mendapatkan tanggal.
<img width="600" height="400" alt="tantangan praktikum 12.2" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week12/image12/tantangan122.png?raw=true"/>

## Praktikum 12.3 - Buat Layanan Sederhana dari Skrip Bash
1. Siapkan konten yang akan dilayani
<img width="700" height="400" alt="buat konten" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week12/image12/kontenservice.png?raw=true"/>

2. Buat skrip wrapper untuk server HTTP
<img width="500" height="400" alt="buat skrip http" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week12/image12/skriphttp.png?raw=true"/>

3. Buat berkas unit systemd untuk layanan ini
<img width="500" height="400" alt="buat systemd" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week12/image12/unitsystemd.png?raw=true"/>

4. Jalankan layanan dan verifikasi
<img width="700" height="400" alt="jalankan skrip" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week12/image12/runlayanankustom.png?raw=true"/>

5. Uji fitur restart otomatis
6. Bersihkan layanan uji setelah selesai
<img width="700" height="400" alt="uji fitur dan bersihkan layanan" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week12/image12/restartotomatis.png?raw=true"/>

### Tantangan
Modifikasi berkas unit demo-web.service sebelum menghapusnya: tambahkan
RestartSec=10sagar sistem menunggu 10 detik sebelum mencoba restart, dan tambahkan
Environment="PORT=9091" lalu ubah ExecStart agar menggunakan variabel tersebut.Aktifkan
layanan dengan enable dan WantedBy=multi-user.target, lalu uji apakah layanan aktif
setelah systemctl daemon-reload. Dokumentasikan perbedaan perilaku dibanding versi
sebelumnya.
<img width="700" height="400" alt="tantangan praktikum 12.3" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week12/image12/tantangan123.png?raw=true"/>

## Praktikum 12.4 - Filter dan Analisis Log Layanan
1. Lihat log SSH dari satu jam terakhir.
<img width="700" height="400" alt="log ssh 1 jam terakhir" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week12/image12/ssh1jam.png?raw=true"/>

2. Filter log berprioritas error keatas.
<img width="700" height="400" alt="filter log berprioritas error" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week12/image12/filterlog.png?raw=true"/>

3. Ikuti log secara real-time sambil memicu aktivitas.
4. Ekstrak log ke berkas untuk analisis.
<img width="700" height="400" alt="pantau log dan analisis" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week12/image12/pantaulog.png?raw=true"/>

### Tantangan
Ekstrak semua log dengan prioritas error (-p err) dari 24 jam terakhir untuk layanan SSH,simpan ke berkas error-ssh-24jam.txt. Gunakan pipeline dari Bab 3 untuk menghitung total jumlah baris error dengan wc -l, lalu tampilkan 10 pesan error yang paling sering muncul menggunakan sort | uniq -c | sort -rn | head -10. Tuliskan perintah lengkap yang kamu gunakan.
<img width="700" height="400" alt="tantangan praktikum 12.4" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week12/image12/tantangan124.png?raw=true"/>

## Praktikum 12.5 - Konfigurasi SSH Server
1. Periksa konfigurasi SSH saat ini.
2. Buat backup dan ubah port SSH.
3. Validasi konfigurasi dan restart layanan.
4. Verifikasi port baru dengan ss.
5. Kembalikan port SSH ke 22 setelah praktek.
<img width="700" height="400" alt="praktikum 12.5" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week12/image12/prakt125.png?raw=true"/>

### Tantangan
Ubah konfigurasi SSH untuk menambahkan dua pengaturan keamanan: PermitRootLogin no
(larang login root langsung) dan MaxAuthTries 3 (maksimal tiga kali percobaan). Lakukan
dengan urutan yang aman: backup, edit, validasi dengan sshd-t, reload. Verifikasi perubahan dengan grep-E "PermitRoot|MaxAuth" /etc/ssh/sshd_config. Kemudian periksa log
SSH untuk memastikan tidak ada error setelah perubahan dengan journalctl-u ssh-n 20.
Referensi Bab 2 untuk penggunaan ss dan Bab 9 untuk keamanan pengguna.
<img width="700" height="400" alt="tantangan praktikum 12.5" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week12/image12/tantangan125.png?raw=true"/>

## Latihan
### Latihan 12.1 Audit Layanan dan Analisis Boot
Lakukan audit menyeluruh terhadap layanan yang berjalan di sistem.
1. Jalankan systemctl list-units –type=service –state=running dan catat semua
layanan aktif. Pilih tiga layanan yang kamu kenal, periksa status masing-masing dengan
systemctl status, dan jelaskan fungsinya.
<img width="700" height="400" alt="list unit" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week12/image12/latihan121a.png?raw=true"/>

> ssh.service Menyediakan akses remote (jarak jauh) ke terminal Linux
>
> cron.service Pengatur jadwal otomatisasi tugas di Linux.
>
> rsyslog.service mengumpulkan, dan menyimpan catatan logs dari kernel ke dalam direktori 

2. Jalankan systemd-analyze blame dan identifikasi lima layanan dengan waktu inisialisasi
terlama. Tampilkan hasilnya menggunakan pipeline: systemd-analyze blame | head-5.
<img width="500" height="400" alt="waktu inisialisasi" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week12/image12/latihan121b.png?raw=true"/>

> 5 layanan dgn waktu inisialisasi terlama yaitu,  apt-daily.service, apt-daily-upgrade.service,
> 
>  man-db.service, logrotate.service, plocate-updatedb.service.

3. Jalankan systemctl–failed dan dokumentasikan hasilnya. Jika ada layanan yang gagal cari tahu penyebabnya dengan journalctl -u nama-layanan -n 30.
<img width="500" height="400" alt="layanan gagal" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week12/image12/latihan121c.png?raw=true"/>

> tidak ada layanan yang gagal

### Latihan 12.2 Layanan Kustom dengan Restart Otomatis
Buat layanan systemd kustom yang mendemonstrasikan fitur restart otomatis.
1. Buat skrip Bash (referensi Bab 7) bernama monitor-disk.sh yang setiap 30 detik menuliskan penggunaan disk ke berkas log. Gunakan df -h dan date.
<img width="700" height="400" alt="skrip monitor-disk.sh" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week12/image12/latihan122a.png?raw=true"/>

2. Buat berkas unit /etc/systemd/system/monitor-disk.service untuk menjalankan skrip
tersebut dengan konfigurasi: Restart=always, RestartSec=5s, dan berjalan sebagai pengguna kamu sendiri.
<img width="700" height="400" alt="skrip monitor-disk.service" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week12/image12/latihan122b.png?raw=true"/>

3. Aktifkan dan jalankan layanan. Verifikasi dengan systemctl status dan pastikan log masuk ke journal.
<img width="700" height="400" alt="verifikasi systemctl" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week12/image12/latihan122c.png?raw=true"/>

4. Simulasikan crash dengan membunuh proses secara paksa (kill-9), tunggu 10 detik, dan
verifikasi bahwa layanan hidup kembali secara otomatis.
5. Bersihkan: nonaktifkan layanan dan hapus berkas unit setelah selesai.
<img width="700" height="400" alt="kill dan remove aktifitas" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week12/image12/latihan122de.png?raw=true"/>

### Latihan 12.3 Investigasi Log dan Keamanan SSH
Analisis log sistem dan tingkatkan keamanan konfigurasi SSH.
1. Gunakan journalctl-b-p err untuk menemukan semua error sejak boot terakhir. Simpan
hasilnya ke berkas dan hitung jumlah baris dengan wc-l.
2. Lakukan tiga perubahan keamanan pada /etc/ssh/sshd_config: tambahkan PermitRootLogin no, MaxAuthTries 3, dan LoginGraceTime 30. Ikuti alur aman: backup, edit, validasi sshd-t, reload.
3. Setelah reload, verifikasi tiga hal: layanan masih berjalan (systemctl status ssh), port masih mendengarkan (ss -tlnp | grep ssh), dan konfigurasi baru terbaca (grep -E
"PermitRoot|MaxAuth|GraceTime" /etc/ssh/sshd_config).
4. Kembalikan konfigurasi SSH ke kondisi semula menggunakan berkas backup.
<img width="700" height="400" alt="latihan 12.3" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week12/image12/latihan123.png?raw=true"/>