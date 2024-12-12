# INSTALL DOCKER ENGINE DI UBUNTU
Metode instalasi : gunakan repository apt

Sebelum menginstal Docker Engine pada mesin host baru, siapkan terlebih dahulu repositori apt Docker. Setelah itu, instal Docker langsung dari repositori tersebut

1.	Siapkan docker repository apt
# Tambahkan  Docker's official GPG key:
```bash
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc
```
# Tambahkan repositori ke sumber Apt:
```bash
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```
![WhatsApp Image 2024-12-12 at 21 19 08_8b458e6c](https://github.com/user-attachments/assets/ff999484-6502-4ac1-8e80-ed1136a75109)

2.	Instal paket docker
```bash
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```
![WhatsApp Image 2024-12-12 at 21 30 46_0096876f](https://github.com/user-attachments/assets/54aa057f-f0d0-433b-abc9-d02b867e37d0)

3.	Verifikasi bahwa instalasi berhasil dengan menjalankan image hello-world:
```bash
sudo docker run hello-world
```
![WhatsApp Image 2024-12-12 at 21 38 37_f163b4dd](https://github.com/user-attachments/assets/e53ff4c5-7c7d-482c-93da-71fe9e06f279)
