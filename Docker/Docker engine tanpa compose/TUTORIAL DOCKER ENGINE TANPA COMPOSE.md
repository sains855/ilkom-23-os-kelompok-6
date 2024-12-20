LANGKAH-LANGKAH MENJALANKAN DOCKER DI LINUX

# BUAT FOLDER DOCKER:
```bash
$ mkdir project-docker
```
# BERPINDAH KE FOLDER:
```bash
$ cd project-docker
```
# BUAT DOCKERFILE
```bash
$ touch Dockerfile
```
# MENGEDIT ISI DOCKERFILe
```bash
$ nano Dockerfile
```
# ISI DOCKERFILE
```bash
# Gunakan image dasar PHP dengan Apache
FROM php:8.1-apache

# Salin file PHP dari direktori lokal ke dalam container
COPY ./html /var/www/html

# Expose port 80 untuk akses HTTP
EXPOSE 80
```
# BUAT FOLDER TEMPAT HTML
```bash
$ mkdir html
```
# BUAT FILE INDEX DI DALAM FOLDER HTML:
```bash
$ touch html/index.php
```
# MENGEDIT ISI FILE INDEX YANG ADA DI DIDALAM FOLDER HTML:
```bash
$ nano html/index.php
```

# ISI FILE index.php:
```bash
<?php
session_start();

if ($_SERVER['REQUEST_METHOD'] == 'POST') {
    // Data username dan password yang valid (hardcoded)
    $valid_username = 'user';
    $valid_password = 'password123';

    // Ambil input dari form
    $username = $_POST['username'];
    $password = $_POST['password'];

    // Verifikasi login
    if ($username === $valid_username && $password === $valid_password) {
        $_SESSION['logged_in'] = true;
        $_SESSION['username'] = $username;
        header('Location: dashboard.php'); // Redirect ke halaman dashboard
        exit;
    } else {
        $error_message = 'Username atau password salah!';
    }
}
?>
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Login</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f9;
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
        }
        .login-container {
            background: #ffffff;
            padding: 20px 30px;
            border-radius: 8px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
            width: 300px;
        }
        .login-container h1 {
            text-align: center;
            margin-bottom: 20px;
            color: #333;
        }
        .login-container label {
            font-weight: bold;
            display: block;
            margin: 10px 0 5px;
        }
        .login-container input[type="text"],
        .login-container input[type="password"] {
            width: 100%;
            padding: 8px;
            margin-bottom: 15px;
            border: 1px solid #ccc;
            border-radius: 4px;
            box-sizing: border-box;
        }
        .login-container button {
            width: 100%;
            background-color: #4CAF50;
            color: white;
            border: none;
            padding: 10px;
            border-radius: 4px;
            cursor: pointer;
        }
        .login-container button:hover {
            background-color: #45a049;
        }
        .error-message {
            color: red;
            font-size: 0.9em;
            margin-bottom: 10px;
            text-align: center;
        }
    </style>
</head>
<body>
    <div class="login-container">
        <h1>Login</h1>
        <?php if (isset($error_message)): ?>
            <p class="error-message"><?php echo $error_message; ?></p>
        <?php endif; ?>
        <form method="POST" action="">
            <label for="username">Username</label>
            <input type="text" id="username" name="username" required>
            <label for="password">Password</label>
            <input type="password" id="password" name="password" required>
            <button type="submit">Login</button>
        </form>
    </div>
</body>
</html>
```

#  BANGUN Docker Image:
```bash
$ docker build -t project-docker-app .
```

# MENJALANKAN KONTAINER:
```bash
$ docker run -d -p 8080:80 project-docker-app
```

# AKSES APLIKASI DI BROWSER
http://localhost:8080

# MENAMPILKAN STATUS DOCKER TELAH BERJALAN
![Gambar dari Google Drive](https://drive.google.com/uc?id=12NLMAnNNc2o4ju9ZbKoWTbcAppS3lx0q)


# MENAMPILKAN BUKTI DOCKER BERJALAN
![Gambar dari Google Drive](https://drive.google.com/uc?id=18SoGVEs0fM5MMhYNyZEfev36c0AZVkrh)


# MENGHENTIKAN KONTAINER YANG BERJALAN
```bash
$ docker stop id-container
```

# MELAKUKAN PEMBATASAN MEMORI
```bash
$ docker run --memory=512m --memory-swap=1g id-image
```
# BUKTI STATUS PEMBATASAN MEMORI
![Gambar dari Google Drive](https://drive.google.com/uc?id=15umxrrN7PMx2QR5ffjbma01yx0NoXZhI)

# MELAKUKAN FASE BEDAH CONTAINER
## 1. Command ps aux
Menampilkan semua proses yang sedang berjalan di dalam container. Ini berguna untuk menganalisis aplikasi atau proses yang sedang dijalankan dalam container.
```bash
$ docker exec -it <container_id> ps aux
```
### Bukti Percobaan ps aux
![Gambar dari Google Drive](https://drive.google.com/uc?id=1Od4LyCy3pSf0kxKsvZPDx2O9PBaU_WK7)

## 2. Command inspect
Command ini memberikan informasi rinci tentang container, termasuk konfigurasi jaringan, mounts, environment variables, dan lainnya.
```bash
$ docker inspect <container_id>
```
## Bukti percobaan inspect
![Gambar dari Google Drive](https://drive.google.com/uc?id=1bG1u3Gn-BMfRI82Iatzh06V_ndUP5GD2)

## 3. Command logs
Untuk melihat log yang dihasilkan oleh container. Ini berguna untuk debugging atau melihat output aplikasi yang berjalan di dalam container.
```bash
$ docker logs <container_id>
```
## Bukti percobaan logs
![Gambar dari Google Drive](https://drive.google.com/uc?id=1V1H19zapeWlpew8xY_Sst6rYtvkuVoSG)

## 4.Command masuk ke container
Untuk masuk dan melakukan modifikasi file didalam container
```bash
$ docker exec -it <container_id> /bin/bash
```
## Bukti percobaan masuk ke container
![Gambar dari Google Drive](https://drive.google.com/uc?id=1J-rrirh8qHUhIdPJquC78tvwaGBt5P2w)

## 5. Membatasi CPU
Untuk membatasi jumlah CPU yang dialokasikan ke kontainer saat menjalankan dengan pengaturan tertentu.
```bash
$ docker run -d --name my-container --cpus="2.0" my-image
```
## Bukti percobaan membatasi cpu ke container
![Gambar dari Google Drive](https://drive.google.com/uc?export=view&id=12sPlfAy1cw69Vtsd21bau2daukCbgv-8)



