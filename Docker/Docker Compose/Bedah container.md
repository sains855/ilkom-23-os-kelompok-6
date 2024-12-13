# 1. Command ps aux
Menampilkan semua proses yang sedang berjalan di dalam container. Ini berguna untuk menganalisis aplikasi atau proses yang sedang dijalankan dalam container.

```
ps aux
```
![image](https://github.com/user-attachments/assets/ed86f2fb-e410-4512-9b10-c570d8345c3e)

# 2. Command inspect
Command ini memberikan informasi rinci tentang container, termasuk konfigurasi jaringan, mounts, environment variables, dan lainnya.

```
docker inspect af2dec0cfe9b
```
![image](https://github.com/user-attachments/assets/b26972a1-f6ef-4f64-b243-603a32014c02)

# 3. Command logs
Untuk melihat log yang dihasilkan oleh container. Ini berguna untuk debugging atau melihat output aplikasi yang berjalan di dalam container.
 
 ```
docker logs af2dec0cfe9b
````
![image](https://github.com/user-attachments/assets/89ca7dd4-930c-4d6b-baa8-30b8e72de641)

# 4. Command masuk ke container
Untuk masuk dan melakukan modifikasi file didalam container
```
docker exec -it af2dec0cfe9b /bin/bash
ls
```
![image](https://github.com/user-attachments/assets/6e579f2e-e00c-4dc1-b0e2-73469b4293c6)


# Comand
```ps aux``` adalah perintah di Linux/Unix yang digunakan untuk menampilkan daftar semua proses yang sedang berjalan di sistem. Berikut penjelasan singkat mengenai setiap bagian dari perintah ini:

- ```ps```
Singkatan dari process status, digunakan untuk menampilkan informasi tentang proses yang berjalan.
- ```a```
Menampilkan semua proses yang dimiliki oleh semua pengguna (bukan hanya proses dari user yang menjalankan perintah).
- ```u```
Menyajikan output dalam format yang lebih user-friendly, termasuk informasi tentang pengguna (user), penggunaan CPU dan memori, waktu jalannya proses, dan perintah yang dijalankan.
- ```x```
Menampilkan semua proses, termasuk proses yang tidak terhubung ke terminal (detached processes).

```ls``` adalah singkatan dari list, yang merupakan perintah di Linux/Unix untuk menampilkan daftar file dan direktori di dalam suatu folder.
