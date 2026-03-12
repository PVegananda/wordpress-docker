# 🚀 WordPress Docker Stack
### WordPress + MySQL + Redis using Docker Compose

![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![WordPress](https://img.shields.io/badge/WordPress-21759B?style=for-the-badge&logo=wordpress&logoColor=white)
![MySQL](https://img.shields.io/badge/MySQL-00758F?style=for-the-badge&logo=mysql&logoColor=white)
![Redis](https://img.shields.io/badge/Redis-D82C20?style=for-the-badge&logo=redis&logoColor=white)

---

## 📚 About This Project

Project ini menjalankan **WordPress CMS menggunakan Docker Compose** dengan tiga container:

- Docker
- WordPress
- MySQL
- Redis

Tujuan project ini adalah memahami konsep:

- Multi-container Docker
- Docker networking
- Volume persistence
- Service dependency (`depends_on`)
- Redis caching

---

## 🏗 System Architecture

Browser  
↓  
localhost:8000  
↓  
WordPress Container  
↙              ↘  
MySQL        Redis  

---

## 📂 Project Structure

```
wordpress-docker
│
├── docker-compose.yml
├── README.md
│
└── screenshots
    ├── docker-ps.png
    ├── wordpress-install.png
    ├── wordpress-dashboard.png
    └── redis-test.png
```

---

## ⚙️ Setup

### 1. Run Docker

```
docker compose up -d
```

### 2. Check Containers

```
docker ps
```

(SCREENSHOT: hasil command `docker ps` dengan 3 container running)

---

## 🌐 Access WordPress

Buka di browser:

```
http://localhost:8000
```

(SCREENSHOT: WordPress installation page)

---

## 🧑‍💻 Login WordPress

Setelah install WordPress:

```
http://localhost:8000/wp-admin
```

(SCREENSHOT: WordPress dashboard)

---

## ⚡ Redis Test

Masuk ke Redis container:

```
docker exec -it wordpress-docker-redis-1 redis-cli
```

Lalu jalankan:

```
PING
```

Output yang diharapkan:

```
PONG
```

(SCREENSHOT: Redis CLI dengan output PONG)

---

## 🐳 Services

### WordPress
Menjalankan CMS WordPress.

### MySQL
Database untuk WordPress.

### Redis
Digunakan sebagai cache untuk meningkatkan performa WordPress.

---

## ❓ Questions

### Why do we need volumes for MySQL?
Volume memastikan data database tetap tersimpan walaupun container dihapus atau restart.

### What is the function of depends_on?
`depends_on` memastikan WordPress dijalankan setelah MySQL dan Redis.

### How does WordPress connect to MySQL?
WordPress menggunakan hostname service Docker:

```
mysql
```

### What are the advantages of Redis for WordPress?
Redis memberikan caching sehingga:

- Query database berkurang
- Website lebih cepat
- Server load lebih rendah

---

## 👨‍💻 Author

Sherlock
