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
![Gambar dari Google Drive](https://drive.google.com/file/d/1pc9xJzHXlNxnNYowJiaBw2FGIgRwebak/view?usp=sharing)

2.	Instal paket docker
```bash
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```
![Gambar dari Google Drive](https://drive.google.com/file/d/1ebIAxptbWTtUlw5-Fd8uLVQohD7zUQmg/view?usp=sharing)

