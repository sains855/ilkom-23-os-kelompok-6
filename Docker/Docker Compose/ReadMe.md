# Apa Itu Docker Engine?
Docker Engine adalah platform perangkat lunak yang memungkinkan Anda membuat, mengelola, dan menjalankan container. Ini menyediakan lingkungan yang terisolasi untuk menjalankan aplikasi.

Komponen utama Docker Engine:

- Docker Daemon: Layanan yang berjalan di latar belakang untuk mengelola container.
- Docker CLI: Antarmuka baris perintah untuk berinteraksi dengan Docker.
- Docker Registry: Tempat penyimpanan gambar Docker, seperti Docker Hub.

Docker Engine digunakan untuk menjalankan dan mengelola container secara individu. Misalnya, Anda dapat menjalankan aplikasi web atau database dengan hanya satu perintah menggunakan Docker CLI.

# Apa itu Docker Compose?

Docker Compose adalah alat untuk mendefinisikan dan menjalankan aplikasi multi-container. Anda menggunakan file YAML untuk mengonfigurasi layanan aplikasi Anda, seperti web server, database, dan aplikasi backend. Alat ini sangat berguna untuk pengelolaan aplikasi kompleks dengan beberapa layanan yang saling terhubung.

Komponen utama Docker Compose:
- File docker-compose.yml: File konfigurasi untuk mendefinisikan layanan aplikasi.
- Docker CLI Command untuk Compose: Perintah untuk mengelola layanan yang didefinisikan di docker-compose.yml.

# Apa itu WSL?

Windows Subsystem for Linux (WSL) adalah fitur pada Windows yang memungkinkan pengguna menjalankan distribusi Linux, seperti Ubuntu, secara native di Windows tanpa menggunakan mesin virtual.

Fitur Utama WSL:
- Integrasi dengan Windows: Anda dapat menjalankan aplikasi Linux secara bersamaan dengan aplikasi Windows.
- Efisiensi Sumber Daya: Tidak memerlukan virtualisasi penuh sehingga lebih hemat sumber daya dibandingkan dengan Virtual Machine.
- Dukungan Docker: WSL 2 menyediakan kernel Linux yang mendukung Docker secara native.

# WSL dengan Docker Engine menggunakan Ubuntu

Docker Engine dapat digunakan dengan WSL 2 untuk menjalankan container di lingkungan Linux seperti Ubuntu secara langsung di Windows. Dengan menggunakan WSL 2, integrasi antara Windows dan Linux menjadi lebih mudah dan efisien.

**Docker Engine pada WSL: Docker Engine berjalan di dalam distribusi Linux seperti Ubuntu yang diinstal di WSL. Hal ini memberikan pengalaman asli menjalankan aplikasi Linux tanpa memerlukan mesin virtual tambahan.**
Manfaat:
- Performa yang optimal karena kernel Linux WSL 2 mendukung container secara native.
- Kemampuan untuk mengelola container Docker langsung dari distribusi Ubuntu di WSL tanpa memerlukan Docker Desktop.
- Akses mudah antara file sistem Windows dan Linux melalui direktori /mnt.

**Dengan pendekatan ini, pengembang dapat memanfaatkan keunggulan Docker Engine dan WSL untuk membangun dan mengelola aplikasi modern dengan lebih efisien.Menggunakan Ubuntu di WSL**
- Distribusi Ubuntu di WSL memberikan lingkungan Linux yang sepenuhnya kompatibel untuk pengembangan perangkat lunak. Anda dapat:
- Menginstal paket Linux dengan apt.
- Mengakses file Windows dari Linux menggunakan /mnt/c/.
- Menjalankan server web atau database untuk pengembangan aplikasi.

Dengan memahami konsep Docker Engine, Docker Compose, dan WSL Ubuntu, pengembangan aplikasi modern dapat dilakukan dengan lebih efisien dan fleksibel. Dokumentasi ini dapat disesuaikan lebih lanjut untuk kebutuhan spesifik proyek Anda.

