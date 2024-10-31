# Panduan Pembuatan Daemon Process
Pada tulisan ini, saya akan memaparkan langkah-langkah pembuatan proses daemon.

## Buat file .service
Masuk sebagai superuser, lalu jalankan perintah:
```bash
$ sudo touch /etc/systemd/system/musar.service
```

## Penulisan script konfigurasi .service
Buka file yang baru saja dibuat dan tuliskan konfigurasi berikut:

```bash
 [Unit]
Description=Contoh Daemon

[Service]
Restart=always
WorkingDirectory=/home/musar
Environment="PYTHONPATH=/home/musar"
ExecStart=/home/musar/myenv/bin/uvicorn main:app --reload --port 7080

[Install]
WantedBy=multi-user.target

```

## Jalankan Perintah Daemon

```bash
$ sudo systemctl daemon-reload
$ sudo systemctl start musar.service
$ sudo systemctl status musar.service
```

## Bukti daemon telah berjalan
![Bukti daemon](https://drive.google.com/uc?export=download&id=1SdEr7ZLIgYVQQLvAqRiSYESsKIss89jx)

Tampilan web:
![Bukti tampilan web](https://drive.google.com/uc?export=download&id=16gnM7fVXVVnJ9P9zSH0chIcOniVP5ytJ)
