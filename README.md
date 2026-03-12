# Dockerize WordPress with MySQL and Redis

Project ini menjalankan **WordPress CMS menggunakan Docker Compose** dengan tiga container utama:

- WordPress (Web Application)
- MySQL (Database)
- Redis (Object Cache)

Project ini dibuat untuk memahami konsep:

- Multi-container Docker architecture
- Container networking
- Data persistence dengan volumes
- Service dependency menggunakan `depends_on`

---

# Architecture
Browser
│
▼
localhost:8000
│
▼
WordPress Container
│
├── MySQL Container
│
└── Redis Container


WordPress berjalan di container sendiri dan terhubung ke:

- MySQL sebagai database
- Redis sebagai caching layer

Semua container saling terhubung melalui **Docker network internal**.

---

# Technologies Used

- Docker
- Docker Compose
- WordPress
- MySQL
- Redis

---

# Project Structure
wordpress-docker
│
├── docker-compose.yml
├── README.md
│
└── screenshots
├── docker-ps.png
├── wordpress-install.png
├── wordpress-dashboard.png
└── redis-ping.png


---

# Setup Instructions

## 1. Clone Repository
git clone <repository-url>

cd wordpress-docker


---

## 2. Run Docker Compose

Jalankan semua container dengan perintah:


docker compose up -d


Perintah ini akan menjalankan:

- WordPress container
- MySQL container
- Redis container

---

## 3. Verify Containers

Cek apakah semua container sudah berjalan:


docker ps


Container yang harus muncul:

- wordpress
- mysql
- redis

📸 **SCREENSHOT NEEDED**


(SCREENSHOT: hasil menjalankan "docker ps" yang menunjukkan 3 container running)


---

## 4. Access WordPress

Buka browser dan akses:


http://localhost:8000


Akan muncul halaman instalasi WordPress.

📸 **SCREENSHOT NEEDED**


(SCREENSHOT: halaman WordPress installation page di browser)


---

## 5. Install WordPress

Isi form instalasi:

- Site Title
- Username
- Password
- Email

Klik **Install WordPress**.

Setelah instalasi selesai, login ke dashboard.


http://localhost:8000/wp-admin


📸 **SCREENSHOT NEEDED**


(SCREENSHOT: WordPress dashboard setelah login)


---

# Redis Connection Test

Masuk ke Redis container:


docker exec -it wordpress-docker-redis-1 redis-cli


Lalu jalankan:


PING


Output yang diharapkan:


PONG


📸 **SCREENSHOT NEEDED**


(SCREENSHOT: terminal menjalankan redis-cli lalu command PING dengan output PONG)


---

# Docker Compose Services

## WordPress

Menjalankan CMS WordPress dan menghubungkan ke database MySQL.

Environment variables:


WORDPRESS_DB_HOST=mysql
WORDPRESS_DB_NAME=wordpress_db
WORDPRESS_DB_USER=wordpress_user
WORDPRESS_DB_PASSWORD=wordpress_password


---

## MySQL

Digunakan sebagai database WordPress.

Environment variables:


MYSQL_ROOT_PASSWORD=rootpassword
MYSQL_DATABASE=wordpress_db
MYSQL_USER=wordpress_user
MYSQL_PASSWORD=wordpress_password


MySQL menggunakan **volume persistence**:


/var/lib/mysql


Agar data database tidak hilang ketika container restart.

---

## Redis

Redis digunakan sebagai **object cache** untuk meningkatkan performa WordPress.

Redis menyimpan hasil query database di memory sehingga:

- Query database berkurang
- Response website lebih cepat
- Performance meningkat

---

# Docker Concepts Learned

Project ini mengajarkan beberapa konsep penting Docker:

### Multi Container Application

Menjalankan beberapa service dalam satu aplikasi:

- WordPress
- MySQL
- Redis

---

### Container Networking

Docker secara otomatis membuat **internal network** sehingga container dapat saling berkomunikasi.

Contoh:

WordPress dapat mengakses MySQL dengan hostname:


mysql


---

### Volumes (Data Persistence)

Volume digunakan untuk menyimpan data secara permanen.

Contoh:


mysql_data:/var/lib/mysql


Tanpa volume, data database akan hilang saat container dihapus.

---

### depends_on

`depends_on` digunakan agar container WordPress dijalankan setelah container database.

Contoh:


depends_on:

mysql

redis


---

# Questions

## Why do we need volumes for MySQL?

Volumes digunakan untuk memastikan data database disimpan secara persistent. Tanpa volume, data database akan hilang ketika container dihapus atau direstart.

---

## What is the function of depends_on?

`depends_on` memastikan container WordPress dijalankan setelah container MySQL dan Redis dijalankan terlebih dahulu.

---

## How does WordPress connect to MySQL?

WordPress terhubung ke MySQL melalui Docker network internal dengan hostname:


mysql


yang sesuai dengan nama service MySQL di docker-compose.

---

## What are the advantages of using Redis for WordPress?

Redis digunakan sebagai object cache yang memberikan beberapa keuntungan:

- Mengurangi jumlah query database
- Mempercepat loading website
- Meningkatkan performa aplikasi

---

# Author

pvegananda