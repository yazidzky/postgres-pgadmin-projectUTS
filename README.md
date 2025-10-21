# PostgreSQL & pgAdmin4 Docker Setup (postgres-yazidzinky)

Proyek ini menjalankan layanan PostgreSQL dan pgAdmin4 menggunakan Docker Compose sesuai dengan ketentuan tugas. Termasuk pembuatan skema, tabel, user, dan pengujian hak akses.

---

## ✅ Ketentuan Tercapai

1. **PostgreSQL**
   - Container: `postgres_YAZIDZINKY`
   - Versi: 15
   - Port: `22107`
   - Username & password disimpan di `.env`

2. **pgAdmin4**
   - Container: `pgadmin_YAZIDZINKY`
   - Port: `44107`

3. **Skema & Tabel**
   - Skema: `SALAM`
   - Tabel: `mahasiswas`
   - Constraint: Primary Key, Unique, Check

4. **User & Role**
   - `backend_dev`: CRUD semua tabel
   - `bi_dev`: Hanya SELECT
   - `data_engineer`: CREATE, DROP, ALTER, CRUD

---

## 🧱 Struktur Folder

```
postgres-yazidzinky/
├── docker-compose.yml
├── .env
├── init/
│   └── 01-init.sql
└── README.md
```

---

## 🚀 Cara Menjalankan

1. Clone repo ini:
   ```bash
   git clone https://github.com/yourusername/postgres-yazidzinky.git
   cd postgres-yazidzinky
   ```

2. Pastikan Docker & Docker Compose terinstall.

3. Jalankan container:
   ```bash
   docker-compose up -d
   ```

4. Akses:
   - **PostgreSQL**: `localhost:22107`
   - **pgAdmin4**: [http://localhost:44107](http://localhost:44107)
     - Email: `admin@example.com`
     - Password: `admin123`

---

## 🔐 User & Password

| User            | Password       | Role                         |
|-----------------|----------------|------------------------------|
| postgres        | ifunggul       | Superuser                    |
| backend_dev     | backend123     | CRUD semua tabel             |
| bi_dev          | bi123          | Hanya SELECT                 |
| data_engineer   | engineer123    | CREATE, DROP, ALTER, CRUD    |

---

## 🧪 Pengujian Role (DBeaver atau psql)

### 1. backend_dev
```sql
INSERT INTO SALAM.mahasiswas (nim, nama, umur, email)
VALUES ('100', 'yazid', 20, 'zid@example.com');
-- BERHASIL
```

### 2. bi_dev
```sql
SELECT * FROM SALAM.mahasiswas;
-- BERHASIL

INSERT INTO SALAM.mahasiswas (nim, nama, umur, email)
VALUES ('101', 'cici', 21, 'cici@example.com');
-- GAGAL: permission denied
```

### 3. data_engineer
```sql
CREATE TABLE SALAM.test_table (id SERIAL PRIMARY KEY, name TEXT);
-- BERHASIL

DROP TABLE SALAM.test_table;
-- BERHASIL
```

---

## ⚠️ Troubleshooting

### Error: `permission denied for sequence mahasiswas_id_seq`
**Penyebab**: User tidak punya akses ke sequence `SERIAL`.  
**Solusi**: Login sebagai `postgres`, lalu jalankan:
```sql
GRANT USAGE, SELECT ON SEQUENCE SALAM.mahasiswas_id_seq TO backend_dev;
GRANT USAGE, SELECT ON SEQUENCE SALAM.mahasiswas_id_seq TO bi_dev;
```
