# LAPORAN PRAKTIKUM MANAJEMEN MEMORI & SYSTEM CALL

#### Nama   : Dandin Sesilia
#### NIM    : 254107020142
#### Kelas  : TI 1H

## Praktikum 10.1 Melihat Penggunaan Memory
1. Jalankan free-h untuk melihat ringkasan RAM dan swap.
2.  Lihat detail memori dari kernel melalui /proc/meminfo.
<img width="700" height="400" alt="lihat memori usage & memori kernel" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week10/image/free-h.png?raw=true"/>

### Analisis
1. Hitung persentase memori tersedia: available / total × 100%. Jika hasilnya
di bawah 10%, sistem mulai kekurangan memori.
> Available = 1.5Gi, Total = 1.9Gi
>
> Perhitungan = 1.5/1.9 x 100% = 78.9%, sistem masih memiliki banyak ruang untuk menjalankan aplikasi lain.

2. Pada baris Swap, apakah kolom used bernilai 0? Jika lebih dari 0, kernel sudah
pernah memindahkan data ke disk karena RAM tidak cukup.
> Kolom used = 0B, kernel belum pernah memindahkan data dari RAM ke disk (swap).

3. Perhatikan field Cached dan Buffers di /proc/meminfo. Nilai ini sesuai
dengan kolom buff/cache pada free-h.
> Data di /proc/meminfo menunjukkan buffers 69.820 kB, cathed 664.064 kB,totalnya sekitar 716 MiB
>
> Data di free -h menunjukkan buff/cache adalah 755Mi. Nilai ini sesuai

## Studi Kasus 10.1 Server Lambat Karena Memori
> **Skenario**: Server aplikasi terasa lambat saat banyak pengguna aktif.
>
> Administrator perlu menentukan apakah penyebabnya adalah kekurangan memori.
1. Periksa kondisi memori secara keseluruhan.
2. Pantau proses secara real-time.
<img width="700" height="400" alt="pemantauan realtime" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week10/image/studycase101.png?raw=true"/>

### Analisis
1. Apakah nilai available sangat kecil (misalnya di bawah 200 MB pada server
dengan RAM 2 GB)? Jika ya, server kemungkinan kekurangan memori.
> Server tidak kekurangan memori, karena nilai available masih sekitar 1500 MB

2. Apakah kolom used pada baris Swap lebih dari 0? Jika ya, kernel sedang
menggunakan swap, yang berarti performa menurun.
> Kolom used pada baris swap menunjukkan 0B yang berarti kernel tidak pernah menggunakan swap
>
> Artinya, penurunan performa server tidak disebabkan oleh swapping


3. Di tampilan top, proses apa yang memiliki %MEM terbesar? Proses tersebut
menjadi kandidat utama penyebab lambatnya server.
> %MEM terbesar digunakan oleh unattended-upgr yang menggunakan 6.5% MEM.
>
> ini adalah proses pembaruan otomatis sistem operasi

## Praktikum 10.2 Mengamati Aktivitas Paging
1. Jalankan vmstat dengan interval 1 detik, 5 sampel.
<img width="700" height="400" alt="vmstat" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week10/image/vmstat.png?raw=true"/>

### Analisis
1. Amati nilai si dan so pada kelima baris. Pada sistem normal dengan RAM
cukup, kedua nilai ini selalu 0.
> si dan so kelima baris bernilai 0 semua, menandakan sistem normal dan RAM cukup

2. Jika nilai si atau so sesekali muncul lebih dari 0, artinya pernah ada aktivitas
swap. Ini masih wajar jika tidak terus-menerus.
> Karena nilai si dan so 0 semua, maka tidak ada aktivitas swap

3. Jika si dan so terus-menerus lebih dari 0, sistem dalam kondisi memory
pressure serius — performa turun drastis karena akses disk jauh lebih lambat
dari RAM.
> Solusinya adalah menambah RAM, mengurangi jumlah proses yang berjalan bersamaan,
>
> atau mengoptimalkan konfigurasi aplikasi.

4. Perhatikan juga kolom free (RAM kosong) dan buff (buffer) untuk memahami
kondisi keseluruhan RAM saat itu.
> kolom free di angka 136.608, artinya memori benar - benar kosong
>
> kolom buffer masih sangat mencukupi untuk mengerjakan tugasnya

## Praktikum 10.3 Membuat dan Mengonfigurasi Swap File
1. Buat file berukuran 512 MB sebagai calon swap.
2. Atur permission file menjadi 600 — hanya root yang boleh membaca dan menulis
3. Format file sebagai area swap, lalu aktifkan.
4. Verifikasi swap aktif.
5. Periksa nilai swappiness, ubah sementara, dan verifikasi perubahan.
<img width="700" height="400" alt="prakt 10.3" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week10/image/prakt103.png?raw=true"/>

### Analisis
1. Berapa nilai swappiness default? Apa artinya bagi perilaku kernel dalam
menggunakan swap?
> Nilai swappiness default adalah 60. Artinya, kernel akan memindah proses yang jarang digunakan ke swap
>
> dengan lebih siap, meskipun RAM tidak benar - benar penuh.

2. Setelah diubah ke 10, konfirmasi nilai berubah pada output cat kedua. Apa
dampak nilai 10 terhadap penggunaan swap dibanding nilai 60?
> Dampak nilai 10 adalah kernel lebih enggan untuk melakukan swap dibanding dengan 60.

3. Apakah entri /swapfile-week10 muncul di swapon–show? Jika tidak,
pastikan Langkah 2 (chmod 600) sudah dijalankan sebelum Langkah 3.
> Ya, entri /swaofile-week10 muncul pada output.

## Praktikum 10.4 Monitoring Memory
1. Ambil snapshot proses diurutkan dari penggunaan memori terbesar.
<img width="700" height="400" alt="ambil snapshot" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week10/image/psaux.png?raw=true"/>
2. Pantau secara real-time dengan top.
<img width="700" height="400" alt="pantau realtime" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week10/image/top.png?raw=true"/>

### Analisis
1. Proses apa yang berada di urutan pertama? Catat nilai %MEM dan RSS-nya.
> Proses yang berada di urutan pertama adah kworker akan tetapi 0.0 memori
>
> Maka, dicatat proses fwupd dengan 2.2%MEM dan RSS-nya 44188.

2. Konversikan RSS dari KB ke MB (bagi 1024). Misalnya, RSS=524288 berarti proses
menggunakan 512 MB RAM. Apakah wajar untuk jenis program tersebut?
> 44188 / 1024 = 43.15MB, sangat wajar untuk proses firmware update.

3. Mengapa VSZ selalu lebih besar dari RSS pada proses yang sama?
> Karena VSZ mencakup seluruh memori yang bisa diakses oleh proses

4. Apakah urutan proses di ps konsisten dengan tampilan top saat diurutkan
berdasarkan %MEM?
> Terlihat agak sedikit berbeda karena top memantau secara realtime,
>
> sedangkan ps memantau pada satu waktu tertentu.

## Praktikum 10.5 Script Monitor Memori
1. Masuk ke direktori kerja dan buat file script:
2. Ketik script
<img width="700" height="400" alt="script memory" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week10/image/nano105.png?raw=true"/>

3. Jalankan script
<img width="700" height="400" alt="run script memory" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week10/image/runnano105.png?raw=true"/>

### Analisis
1. Variabel THRESHOLD=20 menetapkan batas persentase. Perintah free | awk
’/Mem/ {printf "%d", $7/$2*100}’ mengambil kolom ke-7 (available) dibagi
kolom ke-2 (total) dari baris Mem, lalu dikalikan 100 untuk menghasilkan
persentase bilangan bulat.
> Ya, %d digunakan untuk memastikan output adalah bilangan bulat.

2. Kondisi if [ "$AVAIL"-lt "$THRESHOLD" ] bernilai benar jika persentase
memori tersedia di bawah 20.
> Logika if memakai kondisi -lt (less than) yang jika persentase memori dibawah 20
>
> maka akan mengeksekusi blok echo "Peringatan".

3. Ubah THRESHOLD menjadi 90 dan jalankan ulang. Apa yang berubah pada
output? Mengapa demikian?
> Output yang muncul adalah "Peringatan" karena memori yang tersedia pada sistem
>
> diubah menjadi 90, dibawah nilai itu maka akan muncul peringatan.

## Studi Kasus 10.2 Gagal Akses File
1. Buat direktori dan file konfigurasi contoh.
2. Simulasikan permission bermasalah.
3. Kembalikan permission dan verifikasi.
<img width="700" height="400" alt="studi kasus 10.2" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week10/image/studycase102.png?raw=true"/>

### Analisis
1. Mengapa cat menghasilkan Permission denied setelah chmod 000? System
call apa yang gagal?
> Perintah chmod 000 mencabut semua hak akses (baca, tulis, eksekusi) dari semua orang
>
> program tersebut mencoba memanggil system call open().
>
> Karena izinnya 000, kernel menolak permintaan tersebut

2. Apa perbedaan pesan error Permission denied vs No such file or directory?
Coba rm app.conf lalu cat app.conf untuk melihat perbedaannya.
> Permission denied: Filenya ada, tetapi tidak punya izin untuk membukanya.
>
> No such file or directory: Filenya tidak ada di dalam sistem.

3. Permission 644 berarti apa untuk owner, group, dan others?
> Owner = rw-, pemilik bisa membaca dan mengubah isi file
>
> Group = r--, anggota grup hanya bisa membaca
>
> Others = r--, orang diluar grup hanya bisa membaca

## Praktikum 10.6 Mengamati System Call dengan strace
1. Lihat 30 baris pertama system call dari perintah ls.
<img width="700" height="400" alt="prakt 10.6a" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week10/image/prakt106a.png?raw=true"/>

2. Lihat ringkasan statistik dan bandingkan dua direktori berbeda.
<img width="700" height="400" alt="prakt 10.6b" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week10/image/prakt106b.png?raw=true"/>

### Analisis
1. Dari output Langkah 1, identifikasi minimal 4 system call berbeda. Jelaskan
fungsi singkat masing-masing berdasarkan argumen yang terlihat.
- execve: Digunakan untuk menjalankan program. Di sana terlihat argumen "/usr/bin/ls", yang artinya kernel sedang memanggil file biner ls.
- brk: Digunakan untuk mengatur alokasi memori (heap). Argumen NULL di awal biasanya dilakukan untuk mengetahui posisi memori saat ini sebelum dialokasikan.
- openat: Digunakan untuk membuka file (seperti file pustaka .so). Argumen O_RDONLY menunjukkan file dibuka hanya untuk dibaca.
- mmap: Digunakan untuk memetakan file atau perangkat ke dalam memori. Ini sering terlihat setelah openat untuk memasukkan isi file pustaka ke dalam memori RAM agar bisa dieksekusi.

2. Dari ringkasan strace-c, system call mana yang paling sering dipanggil?
Mengapa?
> mmap dipanggil sebanyak 18 kali, karena perintah ls membutuhkan banyak library pendukung
>
> Setiap dibuka, sistem memetakan (teks, data, read-only) ke dalam memori dengan mmap.

3. Apakah ada system call dengan errors lebih dari 0? Apakah itu berarti
program bermasalah, ataukah bagian normal dari logika program?
> Ya, ada beberapa system call dengan error, ini tidak masalah
>
> karena program mencoba mencari file konfigurasi, jika tidak ketemu akan error.

4. Apakah jumlah system call berbeda antara ls dan ls /etc? Faktor apa yang
menyebabkan perbedaan tersebut?
> ls: Total 74 system call (4 error), ls /etc: Total 74 system call (5 error).
> 
> Faktornya jumlah panggilan system call /etc untuk membaca detail tiap file
>
> sehingga, meningkat drastis dibanding menjalankan ls.

## Tugas 10.1 Audit Penggunaan Memori Sistem
1. Buat script memory-audit.sh
2. Ketik script
<img width="700" height="400" alt="nano script tugas 10.1" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week10/image/nanotgs1.png?raw=true"/>

3. Jalankan script 
<img width="700" height="400" alt="run script tugas 10.1" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week10/image/runtgs1.png?raw=true"/>

### Analisis
1. Hitung persentase memori tersedia (available / total × 100%). Apakah sistem dalam kondisi normal?
> Available = 1.6Gi, total = 1.9Gi, maka 1.6/1.9 x 100% = 84.2%, sistem dalam kondisi sangat normal.

2. Mengapa buff/cache tidak dihitung sebagai memori yang terpakai dari sudut pandang ketersediaan untuk aplikasi?
> Karena buff/cache digunakan kernel untuk mempercepat akses data disk. Bersifat sementara dan dapat diambil kembali

3. Dari /proc/meminfo, apakah SwapTotal lebih besar dari 0? Berapa nilai SwapFree?
> Swaptotal > 0, nilai Swapfree adalah 2621432kB

## Tugas 10.2 Identifikasi Proses dengan Memori Tertinggi
**Instruksi:** Simpan daftar 10 proses pengguna memori terbesar ke file.
<img width="700" height="400" alt="tugas 10.2" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week10/image/tgs2.png?raw=true"/>

### Analisis
1. Proses apa di urutan pertama? Catat nilai %MEM dan RSS.
> Proses urutan pertama adalah fwupd dengan 2.1% MEM dan RSSnya 44292.

2. Konversikan RSS ke MB (bagi 1024). Apakah wajar?
> 44292 / 1024 = 43.2, sangat wajar untuk proses tersebut.

3. Jumlahkan %MEM dari 5 proses teratas. Berapa persen RAM yang mereka gunakan bersama?
> Hasil penjumlahan %MEM dari 5 proses teratas adalah 6%.

## Tugas 10.3 Membuat dan Memverifikasi Swap File
1. Buat swap file khusus tugas sebesar 256 MB dan verifikasi.
2. Verifikasi dan simpan hasil
<img width="700" height="400" alt="tugas 10.3" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week10/image/tgs3.png?raw=true"/>

### Analisis
1. Identifikasi kolom NAME, TYPE, SIZE, dan USED pada output swapon –show.
> NAME = /swapfile-tugas-week10, TYPE = file, SIZE = 256M, USED = 0B.

2. Apakah nilai total pada baris Swap di free -h bertambah 256 MB?
> Ya, jadi seluruh totalnya adalah 2.7Gi dari yang sebelumnya 2.5Gi.

3. Mengapa permission 600 penting? Apa risiko jika diatur ke 644?
> Permission 600 memastikan hanya user root yang dapat membaca dan menulis file swap.
>
> Risiko diatur 644, siapapun bisa membaca isi file swap tersebut.

## Tugas 10.4 Analisis System Call dengan strace
**Instruksi:** Analisis system call yang dipanggil perintah ls.
<img width="700" height="400" alt="tugas 10.4" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week10/image/tgs4.png?raw=true"/>

### Analisis
1. Sebutkan minimal 5 system call dari strace-summary.txt beserta fungsi singkatnya.
- mmap: Memetakan file atau perangkat ke dalam memori RAM.
- openat: Membuka file untuk dibaca atau ditulis, sering digunakan untuk memuat library sistem.
- read: Membaca data dari file descriptor (misalnya membaca isi file yang sudah dibuka).
- write: Menulis data ke file descriptor, dalam kasus ls, ini digunakan untuk mencetak teks ke terminal.
- close: Menutup file descriptor yang sudah tidak digunakan lagi agar sumber daya sistem kembali bebas.

2. System call mana yang paling sering dipanggil? Mengapa?
> nmap sering dipanggil karena setiap ls jalan butuh library, setiap library dibuka butuh
>
> mmap untuk memetakan bagian kode, data, dan memori dinamis ke dalam ruang alamat proses.

3. Apakah ada errors lebih dari 0? Apakah program tetap berjalan normal meskipun ada kegagalan tersebut?
> Ada error > 0, program berjalan normal karena error adalah bagian dari logika program.

## Tugas 10.5 Studi Kasus Diagnosa Server Lambat
**Skenario:** Server terasa lambat. Buat script diagnosa yang menggabungkan semua pemeriksaan dari bab ini menggunakan fungsi Bash.

1. Buat file
2. Ketik script
<img width="600" height="800" alt="script tugas 10.5" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week10/image/nanotgs5.png?raw=true"/>

3. Jalankan script
<img width="700" height="400" alt="run script 10.5" src="https://github.com/sesilia-acc/OperationSystem/blob/main/week10/image/runtgs5.png?raw=true"/>

### Analisis
1. Jelaskan peran masing-masing fungsi: cek_memori, cek_swap, cek_proses, cek_paging, dan ringkasan. Mengapa diagnosa dipecah menjadi fungsi terpisah?
- cek_memori: Mengukur kesehatan RAM fisik dengan menghitung persentase memori available terhadap total RAM.
- cek_swap: Memeriksa apakah ada partisi swap yang aktif dan apakah sistem sudah mulai menggunakan ruang disk tersebut.
- cek_proses: Mengidentifikasi 10 proses teratas yang mengonsumsi RAM paling banyak untuk menemukan potensi kebocoran memori.
- cek_paging: Memantau lalu lintas data antara RAM dan Swap secara real-time menggunakan vmstat.
- ringkasan: Melihat status dari fungsi-fungsi sebelumnya untuk memberikan kesimpulan cepat apakah kondisi sistem aman atau tidak.

2. Berdasarkan bagian RINGKASAN, apakah kondisi sistem normal atau kritis? Jelaskan berdasarkan nilai threshold yang digunakan script.
> Kondisi sistem normal. Script menggunakan threshold 20% untuk memori tersedia.
> 
> Memori available adalah 1.6Gi dari total 1.9Gi (sekitar 84%).
>
> Karena 84% > 20%, maka statusnya tetap "normal".

3. Mengapa script menggunakan tee "$LAPORAN" bukan redirection biasa > "$LAPORAN"? Apa keuntungannya?
> Redirection hanya mengirimkan output ke file tanpa menampilkannya di layar terminal.
>
> tee mengirimkan output ke layar terminal SEKALIGUS menyimpan ke file laporan.

4. Dari output cek_paging, apakah ada aktivitas si atau so? Jika ada, apa implikasinya terhadap performa server?
> Aktivitas si dan so bernilai 0 di semua sample data, artinya tidak ada aktivitas paging.