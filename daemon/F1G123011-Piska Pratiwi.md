# DEMONSTRASI DAEMON PADA LARAVEL
Didalam panduan ini terdapat penjelasan mengenai langkah-langkah serve laravel
# langkah-langkah membuat serve laravel
# langkah pertama 
membuat skrip laravel_server pada folder */home/piska/laravel_server* dengan melalui perintah terminal 

"nano /home/piska/laravel-serve/laravel_server.php"

memasukkan skrip dibawah ini:
"#!/bin/bash"

"cd /home/piska/laravel_server"

"php -S localhost:8001"

# langkah kedua
Melakukan pemberian hak akses pada file laravel_server.php

"chmod -R 777 /home/piska/laravel-server"

kemudian untuk memberikan hak akses folder secara langsung

# langkah ketiga
membuat service systemd yang menjelankan skrip laravel serve

"sudo nano /etc/systemd/system/laravel.service"

memasukkan skrip dibawah ini:

"[unit]"

"Description=Laravel Development Server"

"[Service]"

"ExecStart=/home/piska/laravel-serve/laravel_server.php"

"Restart=always"

"[Install]"

"WantedBy=multi-user.target"

# langkah keempat
reload systemd untuk mengaktifkan laravel.service

"sudo systemctl daemon-reload"

"sudo systemctl start laravel"

"sudo systemctl enable laravel"

"sudo sytemctl status laravel"

menunjukkan status laravel.service aktif
![Screenshot 2024-10-23 153104](https://github.com/user-attachments/assets/6716d699-7aba-4719-b3ce-94d5c03d939d)

# langkah kelima
menginstall laravel kedalam folder /home/piska/laravel-server dengan menggunakan perintah

"composer create-project laravel/laravel:^10.0 sistem-operasi"
# screenshoot 
mengakses laravel dengan memasukkan arahan url localhost:8001/sistem-operasi/public/index.php karena kita akan megakses index.php
![Screenshot 2024-10-31 193045](https://github.com/user-attachments/assets/7a4ff0c3-b764-4ad5-af3e-5f6f3056637f)
