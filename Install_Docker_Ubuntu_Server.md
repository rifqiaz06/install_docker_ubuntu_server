## Apa Itu Docker dan Kenapa Penting untuk DevOps?

Docker adalah platform open-source yang memungkinkan developer dan DevOps engineer untuk mengemas aplikasi beserta semua dependensinya ke dalam satu unit yang disebut **container**.

Dengan Docker, aplikasi bisa berjalan **secara konsisten** di berbagai environment — dari laptop developer, server staging, hingga production.

---

## Kenapa Docker Banyak Digunakan?

- **Ringan:** Tidak butuh OS penuh seperti Virtual Machine
- **Cepat:** Startup container hanya dalam hitungan detik
- **Portable:** Bisa dijalankan di mana saja selama ada Docker Engine
- **Konsisten:** Eliminasi "it works on my machine" problem
- **Automation-friendly:** Cocok banget untuk CI/CD pipeline

---

## Konsep Infrastruktur Docker (Simplified)

Bayangkan infrastruktur Docker seperti ini:

```
+----------------------------+
|      Docker Engine        |   ← Software utama di OS (Ubuntu)
+----------------------------+
|  Container 1: NGINX       |   ← Web Server
|  Container 2: MySQL       |   ← Database
|  Container 3: Redis       |   ← Cache Layer
+----------------------------+
```

Setiap container:

- Dibuat dari **Docker Image**
- Bisa dijalankan, dihentikan, dan dihancurkan kapan saja
- Terisolasi tapi tetap bisa berkomunikasi satu sama lain (via network Docker)

---

## Apa Itu Docker Compose?

Docker Compose adalah tools yang membantu kita menjalankan **multi-container application** dengan satu file YAML dan satu perintah.

Contoh: Lo bisa jalankan `nginx`, `php`, `mysql`, `redis` semua sekaligus dengan file `docker-compose.yml`.

---

## Kapan Harus Pakai Docker?

- Saat ingin develop aplikasi di environment yang konsisten
- Ketika deploy aplikasi ke cloud / server
- Dalam CI/CD pipeline (testing, staging, production)
- Saat mau belajar DevOps secara praktikal

---

Dengan pemahaman ini, sekarang kita lanjut ke cara instalasi Docker dan Compose di Ubuntu!

# Cara Install Docker & Docker Compose di Ubuntu 22.04 (Step-by-Step untuk Pemula DevOps)

Docker adalah salah satu tools wajib bagi para DevOps Engineer dan developer modern. Dengan Docker, kita bisa membungkus aplikasi dan semua dependensinya ke dalam satu wadah (container) yang bisa dijalankan di mana saja, tanpa khawatir beda OS atau library.

Pada artikel ini, kita akan membahas **instalasi Docker dan Docker Compose di Ubuntu Server 22.04**, lengkap dengan tips dan simulasi mini project.

---

## Langkah 1: Persiapan Instalasi Docker

Pertama-tama, pastikan server kamu up to date:

```bash
sudo apt update && sudo apt install ca-certificates curl gnupg -y
```

Kemudian, tambahkan key GPG resmi Docker dan konfigurasi repositori-nya:

```bash
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg

echo   "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg]   https://download.docker.com/linux/ubuntu   $(lsb_release -cs) stable" |   sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

---

## Langkah 2: Instalasi Docker Engine

Setelah repositori sudah ditambahkan, lanjutkan dengan instalasi Docker:

```bash
sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin -y
```

Verifikasi instalasi:

```bash
docker --version
docker compose version
```

---

## Langkah 3: Menjalankan Docker Tanpa `sudo`

Secara default, Docker hanya bisa dijalankan oleh root. Agar lebih nyaman, kita bisa tambahkan user saat ini ke grup `docker`.

```bash
sudo usermod -aG docker $USER
newgrp docker
```

> **Tips:** Jangan jalankan Docker sebagai root untuk alasan keamanan dan kenyamanan development.

---

## Langkah 4: Tes Docker dengan Hello World

Mari kita pastikan Docker bisa menjalankan container:

```bash
docker run hello-world
```

Kalau instalasi sukses, kamu akan melihat pesan dari Docker yang menyatakan semuanya berjalan lancar.

---

---

## Langkah 5: Simulasi Project Nginx dengan Docker Compose

Docker Compose digunakan untuk menjalankan beberapa container sekaligus dengan satu perintah.

Contoh sederhana:

```yaml
# docker-compose.yml
version: "3.8"
services:
  web:
    image: nginx:latest
    ports:
      - "8080:80"
```

Jalankan dengan:

```bash
docker compose up -d
```

Akses aplikasi di browser:

```
http://[IP-Server]:8080
```

---

## Best Practice & Tips

- Pisahkan file `docker-compose.yml` untuk tiap project
- Selalu cek versi image terbaru dari Docker Hub
- Backup konfigurasi dan gunakan `.env` file untuk settingan dinamis

---

## Referensi & Lanjutan

- [Instalasi Docker di Ubuntu (Resmi)](https://docs.docker.com/engine/install/ubuntu/)
- [Docker Compose Docs](https://docs.docker.com/compose/)
- [Contoh Project Docker Compose](https://github.com/docker/awesome-compose)

---

## Kesimpulan

Dengan mengikuti langkah-langkah di atas, kamu sekarang sudah bisa menjalankan aplikasi berbasis Docker di Ubuntu Server 22.04. Ini adalah pondasi awal sebelum masuk ke topik-topik lanjutan seperti:

- CI/CD Pipeline
- Reverse Proxy (NGINX + Docker)
- Monitoring Container
- dan Infrastructure as Code (seperti Terraform)
