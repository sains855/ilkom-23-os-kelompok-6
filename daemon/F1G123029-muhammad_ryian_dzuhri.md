# MENJALANKAN DAEMON PROCESS DI LARAVEL

## Deskripsi
Dokumentasi ini menjelaskan cara membuat dan menggunakan skrip untuk menjalankan dan menghentikan server main.py sebagai daemon.

## Langkah-langkah

### 1. Salin Proyek Laravel
Buat file service di dalam ubuntu anda dengan mengetikkan
```bash
$ sudo touch /etc/systemd/system/ryian.service
```

### 2. Membuat Skrip Daemon Di Dalam ryian.service
```bash
[Unit]
Description=Python Project Service
After=network.target

[Service]
WorkingDirectory=/home/ryiandzuhri/venv/project
Environment="PYTHONPATH=/home/ryiandzuhri/venv/project"
ExecStart=/home/ryiandzuhri/venv/project/bin/uvicorn main:app --reload --port 7080
Restart=always
User=ryiandzuhri

[Install]
WantedBy=multi-user.target
```

### 3. Menjalankan dan Menghentikan Server
```bash
$ sudo systemctl daemon-reload 
$ sudo systemctl enable ryian.service 
$ sudo systemctl start ryian.service
$ sudo systemctl status ryian.service
```

### 4. Screenshot
Tampilan Proses Menjalankan Script Yang Sudah Berjalan
![Deskripsi Gambar](https://drive.google.com/file/d/19EPyI0yE8Hzc9Ww7ju8_NSW9ZxXhEKQE/view?usp=sharing)


Tampilan Web
![Deskripsi Gambar](https://drive.google.com/file/d/1CN0ws147vVozS94QqxKa_SE25iVSIicd/view?usp=sharing)

