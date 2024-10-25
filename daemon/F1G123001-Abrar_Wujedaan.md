# Mendemonstrasikan pembuatan dameon process

dalam hal ini saya akan memaparkan tahapan pembuatan daemon process

## 1. Buat directori untuk script
masuk sebagai superuser, lalu jalankan perintah
```bash
$ sudo mkdir -p /opt/uji_daemon
cd /opt/uji_daemon

#Buat script daemon
sudo nano uji_daemon.sh
```

## 2. masukan file script kedalam  monitoring_daemon.sh
```bash
# Fungsi logging
log_message() {
    echo "$(date '+%Y-%m-%d %H:%M:%S') - $1" >> "$LOG_FILE"
}

# Fungsi untuk mengecek apakah proses sudah berjalan
check_process() {
    if [ -f "$PID_FILE" ]; then
        pid=$(cat "$PID_FILE")
        if ps -p "$pid" > /dev/null 2>&1; then
            return 0
        fi
    fi
    return 1
}

# Fungsi untuk memonitor sistem
monitor_system() {
    while true; do
        # CPU Usage
        cpu_usage=$(top -bn1 | grep "Cpu(s)" | awk '{print $2}')
        log_message "CPU Usage: $cpu_usage%"

        # Memory Usage
        memory_usage=$(free -m | awk 'NR==2{printf "%.2f%%", $3*100/$2}')
        log_message "Memory Usage: $memory_usage"

        # Disk Usage
        disk_usage=$(df -h / | awk 'NR==2{print $5}')
        log_message "Disk Usage: $disk_usage"

        # Process Count
        process_count=$(ps aux | wc -l)
        log_message "Total Processes: $process_count"

        sleep 300  # Monitor setiap 5 menit
    done
}

# Fungsi start daemon
start_daemon() {
    if check_process; then
        echo "Daemon sudah berjalan dengan PID: $(cat $PID_FILE)"
        exit 1
    fi

    # Buat direktori kerja jika belum ada
    mkdir -p "$WORK_DIR"
    
    # Buat file log jika belum ada
    touch "$LOG_FILE"
    
    # Start monitoring dalam background
    monitor_system &
    
    # Simpan PID
    echo $! > "$PID_FILE"
    
    log_message "Daemon started with PID: $!"
    echo "Daemon started. PID: $!"
}

# Fungsi stop daemon
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

# Fungsi restart daemon
restart_daemon() {
    stop_daemon
    sleep 2
    start_daemon
}

# Fungsi status daemon
status_daemon() {
    if check_process; then
        echo "Daemon berjalan dengan PID: $(cat $PID_FILE)"
        echo "Log terakhir:"
        tail -n 5 "$LOG_FILE"
    else
        echo "Daemon tidak berjalan"
    fi
}

# Parse argumen command line
case "$1" in
    start)
        start_daemon
        ;;
    stop)
        stop_daemon
        ;;
    restart)
        restart_daemon
        ;;
    status)
        status_daemon
        ;;
    *)
        echo "Penggunaan: $0 {start|stop|restart|status}"
        exit 1
        ;;
esac

exit 0
```
## 3. Berikan permission
```bash
$ sudo chmod +x monitoring_daemon.sh
```
## 4. Isi file.service (iam.service) dengan konfigurasi berikut
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
$ sudo chmod 644 /etc/systemd/system/cyber.service
```
## 6. Menjalankan file Service
```bash
#reload daemon
$ sudo systemctl daemon-reload

# Enable service agar start saat boot
sudo systemctl enable cyber.service

#start service
sudo systemctl start cyber.service

#cek status 
sudo sytemctl status cyber.service
```
## 7. Mlihat log service
```bash
$ sudo journal -u cyber.service
```

## 8. Memberhentikan server
```bash
sudo systemctl start cyber.service
```

adapun tampilan dari daemon:
![Gambar dari Google Drive](https://drive.google.com/uc?id=1-zoh4KzSn_M5i9UGRCnEHFuaMbLmhOWc)
