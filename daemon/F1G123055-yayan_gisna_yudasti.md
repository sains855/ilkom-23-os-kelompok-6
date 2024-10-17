# PEMBUATAN DAEMON SERVICE SERVER LARAVEL
 Panduan ini menjelaskan langkah-langkah untuk membuat server Laravel menggunakan skrip shell kustom dan mengkonfigurasi service systemd untuk mengelolanya.
 ## Langkah-Langkah Membuat Laravel Service 

 ### Langkah Pertama
 Membuat skrip laravel-server.sh pada folder /home/yaya/laravel-server dengan perintah terminal 
 ```
 nano /home/yaya/laravel-serve/laravel-server.sh
 ```
 Masukkan skrip di bawah ini :
 ```
  #!/bin/bash
 
 cd /home/yaya/laravel-server

 php -S localhost:8000
 ```

 ### Langkah Kedua
 Melakukan pemberian hak akses pada file laravel-server.sh
 ```
 chmod +x /home/yaya/laravel-serve/laravel-server.sh
 ```
 ### Langkah Ketiga
 Membuat skrip laravel.service pada folder /etc/systemd/system dengan perintah terminal
 ```
 sudo nano /etc/systemd/system/laravel.service
 ```
 Masukkan skrip di bawah ini :
 ```
 [Unit]
 
 Description=Laravel Development Server
 After=network.target
  
 [Service]
 
 ExecStart=/home/yaya/laravel-serve/laravel-server.sh
 Restart=always
  
 [Install]
 
 WantedBy=multi-user.target
 ```
 ### Langkah Keempat
 Melakukan pengaktifan laravel.service
 ```
 sudo systemctl daemon-reload
 sudo systemctl start laravel
 sudo systemctl enable laravel
 sudo systemctl status laravel
 ```
 ### Screenshot
 ![screen laravel](https://github.com/user-attachments/assets/52f85ed0-3a24-421e-9c49-9d45aff1ecd6)

