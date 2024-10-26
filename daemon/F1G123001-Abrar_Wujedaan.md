# Mendemonstrasikan pembuatan dameon process

dalam hal ini saya akan memaparkan tahapan pembuatan daemon process

## 1. Buat directori untuk script
masuk sebagai superuser, lalu jalankan perintah
```bash
sudo mkdir -p /opt/uji_daemon
cd /opt/uji_daemon

#Buat script daemon
sudo nano uji_daemon.sh
```

## 2. masukan file script kedalam  uji_daemon.sh
```bash
#!/bin/bash

# Variabel
WORK_DIR="/opt/uji_daemon"
LOG_FILE="$WORK_DIR/uji.log"
PID_FILE="/var/run/uji_daemon.pid"

# Fungsi untuk mencatat log
log_message() {
    echo "$(date '+%Y-%m-%d %H:%M:%S') - $1" >> "$LOG_FILE"
}

# Mengecek apakah daemon sudah berjalan
check_process() {
    if [ -f "$PID_FILE" ]; then
        pid=$(cat "$PID_FILE")
        if ps -p "$pid" > /dev/null 2>&1; then
            return 0
        fi
    fi
    return 1
}

# Fungsi monitoring
monitor_system() {
    while true; do
        cpu_usage=$(top -bn1 | grep "Cpu(s)" | awk '{print $2}')
        memory_usage=$(free -m | awk 'NR==2{printf "%.2f%%", $3*100/$2}')
        disk_usage=$(df -h / | awk 'NR==2{print $5}')
        process_count=$(ps aux | wc -l)

        log_message "CPU Usage: $cpu_usage%"
        log_message "Memory Usage: $memory_usage"
        log_message "Disk Usage: $disk_usage"
        log_message "Total Processes: $process_count"

        sleep 300  # Interval 5 menit
    done
}

# Fungsi untuk memulai daemon
start_daemon() {
    if check_process; then
        echo "Daemon sudah berjalan dengan PID: $(cat $PID_FILE)"
        exit 1
    fi

    mkdir -p "$WORK_DIR"
    touch "$LOG_FILE"

    monitor_system &
    echo $! > "$PID_FILE"

    log_message "Daemon started with PID: $!"
    echo "Daemon started. PID: $!"
}

# Fungsi untuk menghentikan daemon
stop_daemon() {
    if ! check_process; then
        echo "Daemon tidak berjalan"
        exit 1
    fi

    pid=$(cat "$PID_FILE")
    kill "$pid"
    rm -f "$PID_FILE"
    log_message "Daemon stopped"
    echo "Daemon stopped"
}

# Fungsi untuk me-restart daemon
restart_daemon() {
    stop_daemon
    sleep 2
    start_daemon
}

# Fungsi untuk status daemon
status_daemon() {
    if check_process; then
        echo "Daemon berjalan dengan PID: $(cat $PID_FILE)"
        echo "Log terakhir:"
        tail -n 5 "$LOG_FILE"
    else
        echo "Daemon tidak berjalan"
    fi
}

# Menjalankan perintah berdasarkan argumen
case "$1" in
    start) start_daemon ;;
    stop) stop_daemon ;;
    restart) restart_daemon ;;
    status) status_daemon ;;
    *) echo "Usage: $0 {start|stop|restart|status}"; exit 1 ;;
esac

exit 0
```
## 3. Berikan permission
```bash
$ sudo chmod +x monitoring_daemon.sh
```
## 5. Buat File Service di Systemd
```bash
sudo nano /etc/systemd/system/cyber.service
```

## 4. Isi file.service (cyber.service) dengan konfigurasi berikut
```bash
[Unit]
Description=System uji Daemon
After=network.target

[Service]
Type=forking
ExecStart=/opt/uji_daemon/uji_daemon.sh start
ExecStop=/opt/uji_daemon/uji_daemon.sh stop
PIDFile=/var/run/uji_daemon.pid
Restart=always

[Install]
WantedBy=multi-user.target
```
## 5. Berikan permission
```bash
sudo chmod 644 /etc/systemd/system/cyber.service
```
## 6. Menjalankan file Service
```bash
#reload daemon
sudo systemctl daemon-reload

# Enable service agar start saat boot
sudo systemctl enable cyber.service

#start service
sudo systemctl start cyber.service

#cek status 
sudo sytemctl status cyber.service
```
## 7. Melihat log service
```bash
$ sudo journal -u cyber.service
```

## 8. Memberhentikan server
```bash
sudo systemctl start cyber.service
```

adapun tampilan dari daemon:
![Gambar dari Google Drive](https://drive.google.com/uc?id=1-zoh4KzSn_M5i9UGRCnEHFuaMbLmhOWc)
