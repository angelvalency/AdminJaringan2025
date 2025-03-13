<div align="center">
  <h1 style="font-weight: bold"> LAPORAN PRAKTIKUM 4 WORKSHOP ADMINISTRASI JARINGAN <br> NTP - Samba </h1>
  <h4 style="text-align: center;">Dosen Pengampu : Dr. Ferry Astika Saputra, S.T., M.Sc.</h4>
</div>
<br />
<br />
<div align="center">
  <img src="https://upload.wikimedia.org/wikipedia/id/4/44/Logo_PENS.png" alt="Logo PENS">
  <h3 style="text-align: center;">Disusun Oleh : </h3>
  <p style="text-align: center;">
    Firsty Angelica Valency (3123500029)<br>
  </p>
  <h3 style="text-align: center;line-height: 1.5">Program Studi Teknik Informatika<br>Departemen Teknik Informatika Dan Komputer<br>Politeknik Elektronika Negeri Surabaya<br>2024/2025</h3>
  <hr>
</div>

--- 

# Daftar Isi
- [Daftar Isi](#daftar-isi)
- [A. Network Time Protocol (NTP)](#a-network-time-protocol-ntp)
  - [A.1. Mengapa NTP Penting?](#a1-mengapa-ntp-penting)
  - [A.2. NTP Client di Linux](#a2-ntp-client-di-linux)
  - [A.3  Konfigurasi NTP Server di Indonesia](#a3--konfigurasi-ntp-server-di-indonesia)
  - [A.4. Analogi Masalah Tanpa NTP](#a4-analogi-masalah-tanpa-ntp)
  - [A.5. Waktu GMT dan UTC di Linux](#a5-waktu-gmt-dan-utc-di-linux)
  - [A.6. TimeSync](#a6-timesync)
  - [A.7. NTPSec](#a7-ntpsec)
- [B.  SAMBA](#b--samba)
  - [B.1. Fungsi Utama SAMBA](#b1-fungsi-utama-samba)
  - [B.2. SAMBA sebagai Sistem Autentikasi](#b2-samba-sebagai-sistem-autentikasi)
  - [B.3. Integrasi SAMBA dengan Active Directory](#b3-integrasi-samba-dengan-active-directory)
  - [B.4. Keunggulan SAMBA](#b4-keunggulan-samba)
  - [B.5. Contoh Penggunaan SAMBA dengan AD](#b5-contoh-penggunaan-samba-dengan-ad)
  - [B.6. Konfigurasi SAMBA](#b6-konfigurasi-samba)
- [C. TUGAS](#c-tugas)
  - [C.1. Unlimited File Sharing](#c1-unlimited-file-sharing)
  - [C.2. Limited File Sharing](#c2-limited-file-sharing)
  - [C.3. Rangkuman](#c3-rangkuman)


---

# A. Network Time Protocol (NTP)

NTP (Network Time Protocol) server diperlukan untuk memastikan bahwa seluruh sistem, host, dan perangkat dalam jaringan memiliki waktu yang seragam dan akurat. Tanpa NTP, setiap perangkat mungkin memiliki waktu yang berbeda-beda karena clock internal perangkat tidak selalu akurat dan dapat mengalami drift (pergeseran waktu) seiring berjalannya waktu. Hal ini dapat menimbulkan masalah, terutama dalam lingkungan yang membutuhkan sinkronisasi waktu yang presisi, seperti dalam sistem keuangan, log audit, atau investigasi insiden keamanan.

## A.1. Mengapa NTP Penting?
1. Konsistensi Waktu: NTP memastikan semua perangkat dalam jaringan memiliki waktu yang sama. Ini penting untuk log sistem, transaksi, dan koordinasi antar perangkat.
2. Audit dan Investigasi: Ketika terjadi insiden atau audit, log waktu yang konsisten memudahkan analisis. Jika waktu berbeda-beda, akan sulit melacak urutan kejadian atau menentukan penyebab masalah.
3. Koordinasi Sistem: Beberapa sistem bergantung pada waktu yang akurat untuk berfungsi dengan baik, seperti database terdistribusi, sistem replikasi, atau skedul tugas.

## A.2. NTP Client di Linux
Di Linux, NTP Client (seperti `ntpd` atau `chrony`) digunakan untuk menyinkronkan waktu sistem dengan NTP server. Jika NTP Client tidak diinstal atau dikonfigurasi, waktu di sistem Linux bisa berbeda dengan waktu sebenarnya atau dengan perangkat lain dalam jaringan.

## A.3  Konfigurasi NTP Server di Indonesia
Ketika menginstal NTP Client di Linux, biasanya server NTP akan mengarah ke server waktu lokal atau regional, seperti server NTP di Indonesia. Ada tiga server NTP yang umum digunakan untuk redundansi dan keandalan:
1. Server NTP Primer: Server utama yang digunakan sebagai referensi waktu.
2. Server NTP Sekunder: Cadangan jika server primer tidak tersedia.
3. Server NTP Tersier: Cadangan tambahan untuk memastikan sinkronisasi waktu tetap berjalan.

Contoh server NTP di Indonesia adalah:
- `0.id.pool.ntp.org`
- `1.id.pool.ntp.org`
- `2.id.pool.ntp.org`

## A.4. Analogi Masalah Tanpa NTP
Bayangkan sebuah insiden keamanan terjadi di jaringan perusahaan. Tanpa sinkronisasi waktu:
- Log dari server A mencatat kejadian pukul 10:00.
- Log dari server B mencatat kejadian yang sama pukul 10:05.
- Log dari perangkat jaringan mencatat pukul 9:58.

Perbedaan waktu ini membuat tim investigasi kesulitan menentukan urutan kejadian yang sebenarnya. Sistem juga bisa kewalahan karena log yang tidak konsisten, sehingga proses deteksi dan respons insiden menjadi lambat atau tidak akurat.

## A.5. Waktu GMT dan UTC di Linux
Di Linux, waktu biasanya disetel menggunakan standar UTC (Coordinated Universal Time), yang merupakan standar waktu global. GMT (Greenwich Mean Time) sering digunakan secara bergantian dengan UTC, meskipun secara teknis ada perbedaan kecil. Penggunaan UTC memastikan konsistensi waktu di seluruh dunia, terlepas dari zona waktu lokal.

NTP server dan client sangat penting untuk memastikan waktu yang konsisten dan akurat di seluruh sistem. Tanpa NTP, perbedaan waktu dapat menyebabkan masalah serius dalam audit, investigasi insiden, dan operasional sistem. Dengan mengarahkan NTP client ke server lokal (seperti server NTP Indonesia), waktu sistem akan lebih akurat dan sesuai dengan zona waktu yang relevan.


## A.6. TimeSync 
Debian 12 memiliki ntp client default yang sudah terinstall yaitu timesync. Systemd -timesync adalah layanan sinkronisasi waktu sederhana yang terintegrasi dengan systemd. 

## A.7. NTPSec
NTPSec adalah versi yang lebih aman dan lebih efisien dari NTP (Network Time Protocol) dirancang untuk meningkatkan keamanan, mengurangi kerentanan, dan mempercepat kinerja dibandingkan dengan NTP. Dibawah ini adalah konfigurasi NTPSec: 

- Instalasi Package

![App Screenshot](assets/ntp/sudo_apt_install_ntpsec.png)

- Edit File Konfigurasi

![App Screenshot](assets/ntp/nano_etc_ntpsec_ntp_conf.png)


- Modifikasi Baris 24

![App Screenshot](assets/ntp/comment_tos_min_clock_4_minsane.png)

![App Screenshot](assets/ntp/tos_minclock_4_minsane_3.png)


- Modifikasi Baris 34
  
![App Screenshot](assets/ntp/pool_debian_pool_ntp_org_iburst.png)

![App Screenshoot](assets/ntp/comment_pool_debian_pool_ntp_org_iburst.png)

![App Screenshoot](assets/ntp/tambah_pool_ntp_nict_jp_iburst.png)


- Restart Layanan ntpsec


![App Screenshoot](assets/ntp/systemctl_restart_ntpsec.png)

- Verifikasi Status NTP
  
![App Screenshot](assets/ntp/ntpq_p.png)



# B.  SAMBA
SAMBA adalah implementasi open source dari protokol SMB (Server Message Block) yang awalnya dikembangkan oleh Microsoft. Protokol SMB digunakan untuk berbagi sumber daya seperti file, printer, dan perangkat lainnya dalam jaringan. SAMBA memungkinkan sistem operasi seperti Linux dan Unix untuk berintegrasi dengan lingkungan Windows, sehingga memungkinkan pertukaran data dan sumber daya antara sistem yang berbeda.

## B.1. Fungsi Utama SAMBA
1. File Sharing : Memungkinkan berbagi file antara sistem Windows dan Linux.
2. Printer Sharing: Memungkinkan berbagi printer antara sistem yang berbeda.
3. Authentication: Dapat digunakan sebagai sistem autentikasi terpusat.
4. Integrasi dengan Active Directory (AD): SAMBA dapat berintegrasi dengan Active Directory, yang memungkinkan manajemen pengguna dan hak akses secara terpusat.


## B.2. SAMBA sebagai Sistem Autentikasi
SAMBA dapat digunakan sebagai sistem autentikasi terpusat dengan memanfaatkan Active Directory (AD). Active Directory adalah layanan direktori yang dikembangkan oleh Microsoft untuk jaringan berbasis Windows. Dengan SAMBA, sistem Linux dapat berintegrasi dengan AD, sehingga memungkinkan:

1. Centralized Authentication:
   - Setiap PC yang login akan menyimpan informasi login di AD server.
   - Informasi ini mencakup username, password, dan hak akses.
   - Dengan AD, admin tidak perlu mengatur autentikasi secara manual di setiap komputer.

2. Manajemen Pengguna Terpusat:
   - Misalnya, ada 30 mahasiswa yang perlu login ke jaringan. Tanpa AD, admin harus mengatur autentikasi satu per satu di setiap komputer.
   - Dengan AD, admin hanya perlu membuat akun sekali di AD server, dan semua komputer yang terhubung ke AD akan mengenali akun tersebut.

3. Single Sign-On (SSO):
   - Pengguna hanya perlu login sekali ke AD, dan mereka dapat mengakses semua sumber daya (file, printer, dll.) yang diizinkan tanpa perlu login ulang.

4. Role-Based Access Control (RBAC):
   - AD memungkinkan admin untuk mengatur hak akses berdasarkan peran (role). Misalnya, admin dapat memberikan akses penuh kepada admin dan akses terbatas kepada pengguna biasa.

## B.3. Integrasi SAMBA dengan Active Directory

SAMBA dapat berfungsi sebagai:
1. Domain Controller:
  SAMBA dapat bertindak sebagai Domain Controller (DC) yang menggantikan fungsi AD server di lingkungan Windows memungkinkan sistem Linux untuk mengelola pengguna dan grup seperti di AD.

2. Domain Member:
 	SAMBA dapat bergabung ke domain AD yang sudah ada sebagai anggota (member) memungkinkan sistem Linux untuk menggunakan autentikasi dari AD server yang sudah ada.

3. File and Print Server:
   	SAMBA dapat menyediakan layanan berbagi file dan printer yang terintegrasi dengan AD.

## B.4. Keunggulan SAMBA

1. Open Source:
SAMBA dikembangkan oleh komunitas open source, sehingga dapat digunakan secara gratis dan dimodifikasi sesuai kebutuhan.

2. Kompatibilitas Antar Platform:
SAMBA menjembatani sistem operasi yang berbeda, seperti Windows, Linux, dan macOS. Misalnya, pengguna Windows dapat mengakses file yang disimpan di server Linux melalui SAMBA.

3. Fleksibilitas:
SAMBA dapat digunakan dalam berbagai skenario, mulai dari jaringan kecil hingga enterprise.

4. Keamanan:
SAMBA mendukung enkripsi dan protokol keamanan modern, seperti Kerberos, untuk melindungi data yang ditransfer.

## B.5. Contoh Penggunaan SAMBA dengan AD
Misalnya, di sebuah laboratorium komputer dengan 30 mahasiswa:
Tanpa AD:
Admin harus membuat akun untuk setiap mahasiswa di setiap komputer.
Proses ini memakan waktu dan rentan terhadap kesalahan.

Dengan AD dan SAMBA:
Admin membuat akun sekali di AD server.
Semua komputer yang terhubung ke AD (baik Windows maupun Linux) akan mengenali akun tersebut.
Mahasiswa dapat login ke komputer manapun menggunakan akun yang sama.
Admin dapat mengelola hak akses (misalnya, membatasi akses ke folder tertentu) secara terpusat.


## B.6. Konfigurasi SAMBA
- Instalasi SAMBA

  ![App Screenshot](assets/samba/sudo_apt_install_samba.png)

- Membuat Direktori Share

  ![App Screenshot](assets/samba/mkdir_home_share01.png)

  ![App Screenshot](assets/samba/hak_akses_777.png)

- Edit File Konfigurasi SAMBA

  ![App Screenshot](assets/samba/nano_etc_ntpsec_smb.conf.png)

- Konfigurasi Global

  ![App Screenshot](assets/samba/unix_charset_UTF_8.png)

  ![App Screenshot](assets/samba/interface_blm_diedit.png)

  ![App Screenshot](assets/samba/interface_sdh_diedit.png)

- Konfigurasi Share

  ![App Screenshot](assets/samba/share.png)

- Restart Layanan SAMBA

  ![App Screenshot](assets/samba/restart_smb.png)



# C. TUGAS
## C.1. Unlimited File Sharing
Berikut ini adalah konfigurasinya:

- Install samba client

  ![App Screenshot](assets/unlimited_share/ip_a_install_smbclient.png)

- Akses Folder dengan file sharing di Linux

   ![App Screenshot](assets/unlimited_share/smbclient_server_share.png)

- Masuk folder eksplorer Windows Network dan  Isi tab identity network dengan ip address server Linux 

  ![App Screenshot](assets/unlimited_share/windows_file_share.png)


- Membuat folder di Windows

  ![App Screenshot](assets/unlimited_share/windows_folder_create.png)

- Cek Directory share di Linux

  ![App Screenshot](assets/unlimited_share/other_sysadmin29_windows_file.png)

  ![App Screenshot](assets/unlimited_share/hasil_folder_share.png)

- Membuka directory share

  ![App Screenshot](assets/unlimited_share/hasil_add_folder.png)

- Close debian lalu coba melakukan langkah yang sama untuk menambahkan gambar

  ![App Screenshot](assets/unlimited_share/samba_accs_again_new_ip.png)

- Menambahkan gambar di File manager Windows

  ![App Screenshot](assets/unlimited_share/tambah_gambar_di_folder_windows.png)

- Cek di folder manager Linux

  ![App Screenshot](assets/unlimited_share/hasil_add_gambar_di_debian.png)


## C.2. Limited File Sharing
Berikut adalah konfigurasinya:
- Membuat group baru

  ![App Screenshot](assets/limit_share/group_add_smbgroup01.png)

- Membuat direktori share01

  ![App Screenshot](assets/limit_share/group_add_smb_group_01_dan_mkdir_share01.png)

- Mengubah kepemilikan grup direktori share01

  ![App Screenshot](assets/limit_share/chgrp_smbgroup_01_home_share01.png)


- Mengubah Izin direktori

  ![App Screenshot](assets/limit_share/chmod_770_home_share01.png)

- Mengedit Konfigurasi Samba

  ![App Screenshot](assets/limit_share/nano_etc_smb_smb_conf.png)

- Restart Layanan SAMBA

  ![App Screenshot](assets/limit_share/systemctl_restart_smbd.png)

- Menambahkan user Samba

  ![App Screenshot](assets/limit_share/add_user_debian.png)

  ![App Screenshot](assets/limit_share/smbpasswd_a_debian.png)

  ![App Screenshot](assets/limit_share/usermode_aG_smbgroup_01_debian.png)


- Cek IP File share

  ![App Screenshot](assets/limit_share/cek_ip_add_limit_share.png)


- Masuk folder eksplorer Windows Network dan  Isi tab identity network dengan ip address server Linux 

  ![App Screenshot](assets/limit_share/tab_identity.png)

  ![App Screenshot](assets/limit_share/windows_akses_limited_shared.png)

- Menambahkan file angel.txt

  ![App Screenshot](assets/limit_share/edit_file_limit_share.png)

- Cek directory share01 di Linux
  
  ![App Screenshot](assets/limit_share/cek_file_di_linux_after_add_di_windows.png)


## C.3. Rangkuman 
Buat rangkuman tentang package management

Rangkuman tentang Manajemen Paket di Debian 12 (Bookworm)
Package Manager adalah alat yang membantu kita mengelola software di sistem operasi. Tugas utamanya adalah memudahkan proses mengunduh, menginstal, memperbarui, dan menghapus software. Di Debian, ada beberapa alat untuk mengelola paket, dan cara penggunaannya bisa melalui Interface grafis (GUI) atau perintah terminal (CLI).

1. APT (Advanced Package Tool)
APT adalah alat berbasis CLI (Command Line Interface) yang paling sering digunakan di Debian. Berikut beberapa perintah dasar APT: 
Perintah untuk Mencari Informasi (bisa diakses tanpa login sebagai root):
- `apt show nama_paket`: Menampilkan informasi detail tentang sebuah paket.
- `apt search kata_kunci`: Mencari paket yang sesuai dengan kata kunci.
- `apt-cache policy nama_paket`: Menampilkan versi paket yang tersedia di repositori.

  Perintah untuk Mengelola Sistem (harus dijalankan sebagai root atau menggunakan `sudo`):
- `apt update`: Memperbarui daftar paket yang tersedia dari repositori.
- `apt install nama_paket`: Menginstal sebuah paket.
- `apt upgrade`: Memperbarui semua paket yang sudah terinstal.
- `apt full-upgrade`: Memperbarui paket, termasuk menambah atau menghapus paket lain jika diperlukan.
- `apt remove nama_paket`: Menghapus paket, tapi menyimpan file konfigurasinya.
- `apt purge nama_paket`: Menghapus paket beserta file konfigurasinya.
- `apt autoremove`: Menghapus paket yang tidak diperlukan lagi.
- `apt clean`: Membersihkan cache paket yang sudah diunduh.
- `apt autoclean`: Membersihkan cache paket yang sudah usang.


2. Software (Simplified Package Manager)

    ![App Screenshot](assets/rangkuman/simplified_debian_interface.png)

    Software adalah alat berbasis GUI (Graphical User Interface) yang lebih mudah digunakan, terutama untuk pengguna yang tidak terbiasa dengan terminal. Dengan alat ini, kita bisa:
   - Mencari  aplikasi.
   - Menginstal aplikasi.
   - Menghapus aplikasi.
   - Memperbarui sistem.


3. Discover: KDE Package Manager

    ![App Screenshot](assets/rangkuman/kde_gui.png)

    Discover adalah alat berbasis GUI yang dirancang khusus untuk lingkungan desktop KDE. Dengan Discover, kita bisa:
   - Mencari aplikasi.
   - Menginstal aplikasi.
   - Memperbarui aplikasi.
   - Menghapus aplikasi.
   - Mengelola repositori (sumber software).

 4. Synaptic: Comprehensive Package Manager

    ![App Screenshot](assets/rangkuman/synaptic.png)

    Synaptic adalah alat berbasis GUI yang lebih lengkap dan detail dibandingkan Software atau Discover. Dengan Synaptic, kita bisa:
   - Melihat semua paket yang tersedia, baik yang sudah terinstal maupun belum.
   - Mengurutkan paket berdasarkan kategori, status, atau sumber.
   - Menginstal, memperbarui, atau menghapus paket.
   - Mengelola repositori.
   Synaptic cocok untuk user yang ingin kontrol lebih detail atas paket-paket di sistem mereka.

   4. Instalasi Paket dengan Gdebi dan Dpkg
Ketika kita ingin menginstal paket dari sumber eksternal (bukan dari repositori resmi Debian), paket yang bisa diinstal biasanya memiliki format .deb. Ada beberapa cara untuk menginstal paket dengan format ini, salah satunya menggunakan Gdebi atau Dpkg.
Gdebi adalah alat berbasis GUI (interface grafis) yang memudahkan kita untuk menginstal paket .deb. Kelebihan Gdebi adalah bisa secara otomatis mengelola dependensi (paket-paket lain yang dibutuhkan oleh paket yang akan diinstal).
    ![App Screenshot](assets/rangkuman/gdebi.png)


    Dpkg adalah alat berbasis CLI (Command Line Interface) yang juga bisa digunakan untuk menginstal paket .deb. Namun, Dpkg tidak mengelola dependensi secara otomatis, jadi jika ada dependensi yang kurang, kita harus menginstalnya secara manual.

5. Perbedaan Antara GUI dan CLI
- GUI (Graphical User Interface):
  - Lebih mudah digunakan, terutama untuk pemula.
  - Cocok untuk pengguna yang tidak ingin menggunakan terminal.
  - Contoh: Software, Discover, Synaptic.

- CLI (Command Line Interface):
  - Lebih cepat dan powerful untuk pengguna yang sudah terbiasa.
  - Cocok untuk pengguna yang ingin kontrol penuh atas sistem.
  - Contoh: APT.




