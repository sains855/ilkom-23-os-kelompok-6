# MENJALANKAN DAEMON PROCESS DI LARAVEL
 dalam panduan ini menjelaskan tentang langkah-langkah serve laravel

 ## langkah-langkah membuat larvel serve
 ### langkah yang pertama
 Membuat skrip laravel-server.sh pada folder**/home/wraningsih/laravel-server** dengan perintah terminal
  ```
 nano /home/wraningsih/laravel-serve/laravel-server.sh
 ```
masukan skrip di bawah ini:
```
 #!/bin/bash
 
 cd /home/yaya/laravel-server

 php -S localhost:8001
 ```

 ### Langkah Kedua
 Melakukan pemberian hak akses pada file **laravel-server.sh**

 ```
 chmod -R 777 /home/yaya/laravel-server
 ```

untuk memberikan hak akses folder secara langsung

### langkah ke tiga
membuat service systemd yang akan menjalankan skrip laravel serve.
 ```
 sudo nano /etc/systemd/system/laravel.service
 ```
masukkan skrip di bawah ini:
 ```
 [Unit]
 
 Description=Laravel Development Server
 After=network.target
  
 [Service]
 
 ExecStart=/home/wraningsih/laravel-serve/laravel.sh
 Restart=always
  
 [Install]
 
 WantedBy=multi-user.target
 ```
### langkah keempat
reload systemd untuk mengaktifkan **laravel.service**
 ```
 sudo systemctl daemon-reload
 sudo systemctl start laravel
 sudo systemctl enable laravel
 sudo systemctl status laravel
 ```
menunjukkan status **laravel.service** aktif
![Screenshot 2024-10-22 105437](https://github.com/user-attachments/assets/9ae9e2c5-cc03-41bc-bffa-e2ecaf068716)

### langkah kelima
menginstal laravel kedalam folder **/home/wraningsih/laravel-server** dengan perintah
 ```
 composer create-project laravel/laravel:^10.0 sistem-operasi
 ```

### screenshoot
mengakses laravelnya dengan memasukkan arahan ke url  **localhost:8001/sistem-operasi/public/index.php**  karena kita harus mengakses  **index.php**

<img width="643" alt="Screenshot 2024-10-19 150934" src="https://github.com/user-attachments/assets/cecc3a77-52ba-40a6-9659-caa87349963d">
