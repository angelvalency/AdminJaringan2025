<div align="center">
  <h1 style="font-weight: bold"> Unix-and-Linux-sysadmin-notes <br> Rangkuman Chapter 6: Software Installation</h1>
</div>
<br />
<br />
<div align="center">
  <img src="assets/img/cover-book-unix-linux-sysadmin/cover_book_unix_linux_administration_handbook.png" alt="cover_book_unix_linux_administration_handbook.png">
</div>
<br />
<br />
<div align="center">
  <p style="line-height: 1.5"> Unix and Linux system administration handbook by Evi Nemeth Garth Snyder Trent R. Hein Ben Whaley Dan Mackin</h3>
  <p>
</div>

---
# Daftar Isi
- [Daftar Isi](#daftar-isi)
- [Chapter 6: Software Installation](#chapter-6-software-installation)
  - [A. Instalasi Sistem Operasi](#a-instalasi-sistem-operasi)
    - [A.1 Instalasi dari Jaringan](#a1-instalasi-dari-jaringan)
  - [B. Sistem Manajemen Paket di Linux](#b-sistem-manajemen-paket-di-linux)
  - [C. Manajemen Paket Tingkat Tinggi](#c-manajemen-paket-tingkat-tinggi)
    - [C.1 Repositori Paket](#c1-repositori-paket)
    - [C.2 APT: Advanced Package Tool](#c2-apt-advanced-package-tool)
    - [C.3 yum: Yellowdog Updater, Modified](#c3-yum-yellowdog-updater-modified)
  - [D. Lokalisasi dan Konfigurasi Perangkat Lunak](#d-lokalisasi-dan-konfigurasi-perangkat-lunak)


---

# Chapter 6: Software Installation

## A. Instalasi Sistem Operasi

&nbsp;&nbsp;&nbsp;&nbsp; Distribusi Linux dan FreeBSD memiliki prosedur yang cukup sederhana untuk instalasi dasar. Untuk komputer fisik,  dapat melakukan boot dari CD, DVD, atau USB drive. Sementara itu, untuk  `mesin virtual,  dapat melakukan boot dari file ISO`. Instalasi sistem operasi dari media lokal cukup mudah berkat adanya aplikasi antarmuka grafis (GUI) yang membimbing pengguna melalui proses ini.

### A.1 Instalasi dari Jaringan

&nbsp;&nbsp;&nbsp;&nbsp; Jika  perlu menginstal sistem operasi pada lebih dari satu komputer, metode instalasi menggunakan media lokal akan menjadi kurang efisien. Proses ini memakan waktu, rentan terhadap kesalahan, dan membosankan jika harus dilakukan berulang kali. Solusi yang lebih baik adalah melakukan instalasi melalui jaringan menggunakan server.

&nbsp;&nbsp;&nbsp;&nbsp; Metode yang paling umum digunakan melibatkan `DHCP   dan  TFTP`   untuk melakukan boot tanpa menggunakan media fisik. Setelah itu, sistem akan mengambil file instalasi OS dari server jaringan melalui `HTTP, FTP, atau NFS`. File instalasi bisa berada di server yang sama atau di server lain.

&nbsp;&nbsp;&nbsp;&nbsp; Instalasi yang sepenuhnya otomatis dapat dilakukan melalui   PXE (Preboot eXecution Environment) . `PXE adalah str dari Intel yang memungkinkan sistem untuk melakukan boot melalui interface jaringan.

&nbsp;&nbsp;&nbsp;&nbsp; `PXE berfungsi seperti sistem operasi kecil yang tertanam dalam ROM pada kartu jaringan`. PXE `menyediakan API str yang bisa digunakan oleh BIOS sistem`, sehingga memungkinkan `satu boot loader untuk melakukan booting pada komputer apa pun yang mendukung PXE tanpa perlu menyediakan driver khusus untuk setiap kartu jaringan`.

---

## B. Sistem Manajemen Paket di Linux

&nbsp;&nbsp;&nbsp;&nbsp; Terdapat `dua format paket yang umum digunakan dalam sistem Linux`. Beberapa distribusi seperti `Red Hat, CentOS, SUSE, dan Amazon Linux` menggunakan format `RPM`, sedangkan `Debian dan Ubuntu` menggunakan format `.deb`. Kedua format ini memiliki fungsi yang serupa.

&nbsp;&nbsp;&nbsp;&nbsp; Baik `RPM` maupun `.deb` kini `berfungsi sebagai alat konfigurasi` yang mencakup seluruh proses manajemen perangkat lunak. Pada tingkat dasar, terdapat alat yang digunakan untuk menginstal, menghapus, dan menampilkan informasi paket, yaitu:

- `rpm` untuk sistem berbasis `RPM`
- `dpkg` untuk sistem berbasis `.deb`

&nbsp;&nbsp;&nbsp;&nbsp; Di atas alat dasar tersebut, terdapat sistem yang lebih canggih untuk mencari dan mengunduh paket dari internet, menganalisis ketergantungan antar paket, serta memperbarui semua paket pada sistem:

- `yum (Yellowdog Updater, Modified)` digunakan dalam sistem berbasis `RPM`
- `APT (Advanced Package Tool)` dikembangkan untuk `.deb`, tetapi juga kompatibel dengan `RPM`

---

## C. Manajemen Paket Tingkat Tinggi

&nbsp;&nbsp;&nbsp;&nbsp; Alat manajemen paket tingkat tinggi adalah alat yang paling sering digunakan. Dengan alat ini,  dapat:

- Menginstal, menghapus, dan memperbarui paket
- Mencari paket tertentu
- Melihat daftar paket yang telah diinstal dalam sistem

### C.1 Repositori Paket

&nbsp;&nbsp;&nbsp;&nbsp; Distribusi Linux memiliki repositori perangkat lunak yang bekerja bersama dengan sistem manajemen paket mereka. Secara default,  `sistem manajemen paket akan menunjuk ke satu atau lebih server web atau FTP yang dikelola oleh pengembang distribusi `.

- `Release`: Snapshot konsisten dari semua paket dalam repositori.
- `Komponen`: Subset perangkat lunak dalam suatu rilis.
- `Arsitektur`: Kelas perangkat keras yang dapat menjalankan paket yang sama. Contoh: Fedora 20 dengan arsitektur **i386**.

---

### C.2 APT: Advanced Package Tool

&nbsp;&nbsp;&nbsp;&nbsp; `APT adalah sekumpulan alat untuk mengelola paket dalam sistem berbasis Debian`. Ini adalah sistem manajemen paket yang paling banyak digunakan pada sistem Debian dan turunannya seperti Ubuntu. Beberapa alat dalam APT meliputi:

- `apt-get`: Alat command-line untuk menangani paket (instalasi, penghapusan, dan pembaruan).
- `apt-cache`: Alat untuk mencari dan menampilkan informasi dalam cache paket APT.
- `apt-file`: Alat untuk mencari file di dalam paket.
- `apt-show-versions`: Alat untuk menampilkan versi paket yang diinstal.
- `aptitude`: Antarmuka tingkat tinggi untuk sistem manajemen paket, dengan fitur tambahan dibanding `apt-get`.
- `apt-mirror`: Digunakan untuk mereplikasi repositori paket.

Pada sistem `Ubuntu`, disarankan untuk mengabaikan alat lama `dselect`, karena sudah tidak banyak digunakan.

---

### C.3 yum: Yellowdog Updater, Modified

&nbsp;&nbsp;&nbsp;&nbsp; `yum` adalah manajer paket untuk sistem Linux berbasis `RPM`. Yum melakukan penyelesaian dependensi saat menginstal, memperbarui, dan menghapus paket. Selain itu, `yum` juga dapat mengelola paket dari repositori yang terinstal dan melakukan operasi melalui command-line pada paket individual.

---

## D. Lokalisasi dan Konfigurasi Perangkat Lunak

&nbsp;&nbsp;&nbsp;&nbsp; Menyesuaikan sistem dengan lingkungan lokal atau berbasis cloud adalah salah satu tugas utama dalam administrasi sistem. Menangani masalah lokalisasi dengan cara yang terstruktur dan dapat direproduksi sangat penting untuk menghindari sistem yang sulit dipulihkan setelah terjadi insiden besar.