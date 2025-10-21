# PostgreSQL + pgAdmin4 – Containerised Lab

Penyiapan lingkungan PostgreSQL & pgAdmin4 dengan Docker Compose

## 🧱 Prasyarat
- Docker 20.10+  
- Docker Compose 2.0+  
- Port **22107** & **44107** belum dipakai

## 🚀 Menjalankan layanan
```bash
# clone repo 
https://github.com/yazidzky/postgres-pgadmin-projectUTS.git

# duplikat .env
cd .env

# nyalakan
docker compose up -d
```

## 📡 Akses
| Layanan   | URL / Alamat               | Kredensial default              |
|-----------|----------------------------|----------------------------------|
| pgAdmin4  | http://localhost:44107     | admin@example.com / admin        |
| PostgreSQL | `localhost:22107`         | postgres / ifunggul (lihat .env) |

## 🧪 Verifikasi
1. Buka pgAdmin → Add New Server →  
   Host: `postgres_YAZIDZINKY`, Port: `5432`, User: `postgres`, Password: `ifunggul`  
2. Buka DBeaver → New Connection → Host `localhost`, Port `22107`, credential sama.

## 🗃️ Skema & Objek
Skema `SALAM` beserta tabel `mahasiswas` dibuat otomatis lewat script:
```bash
docker exec -i postgres_YAZIDZINKY psql -U postgres < sql/01_create_schema_and_table.sql
```

## 👥 User & Hak Akses
Jalankan script kedua:
```bash
docker exec -i postgres_YAZIDZINKY psql -U postgres < sql/02_create_users_and_grant.sql
```

| User            | Password      | Peran |
|-----------------|---------------|-------|
| backend_dev     | backend123    | CRUD semua tabel |
| bi_dev          | bi123         | Read-only |
| data_engineer   | engineer123   | DDL + CRUD |

## 📂 Struktur Repo
```
.
├── docker-compose.yml
├── .env
├── init/
│   ├── 01-init.sql
└── README.md
```

## 🛑 Berhenti / Bersihkan
```bash
docker compose down       # stop container
docker compose down -v    # stop + hapus volume (data ikut hilang)
```

## 📄 Lisensi
Bebas digunakan untuk keperluan pendidikan.
```

Sesuaikan username GitHub dan nama repo lalu push.
