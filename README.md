# Trello Lite Backend Take-Home

Legacy System & Migration Challenge (Laravel ? Nest.js)

## Context (ringkas)
- Bangun legacy backend (Laravel) dan migrasi ke Nest.js dengan perilaku API yang konsisten.
- Domain: Users ? Projects ? Tasks (status pending|in_progress|done, optional due_date), kepemilikan per-user wajib.
- Fokus evaluasi: arsitektur, authz/authn, relasi DB, validasi/error handling, konsistensi API, dokumentasi, mindset migrasi/compatibility.

## Struktur Repo
- `laravel/` (legacy, MySQL) — selesai: Sanctum, CRUD Projects/Tasks, Swagger, JSON seragam.
- `nestjs/` (migrated, PostgreSQL) — JWT, CRUD Projects/Tasks, Swagger, JSON seragam, port berbeda (3001) agar paralel dengan Laravel.
- Root `.gitignore` menjaga `.env`, `vendor`, `node_modules`, `dist` tidak ter-commit.

## Jalankan Laravel (legacy)
```bash
cd laravel
cp .env.example .env   # isi kredensial MySQL
composer install
php artisan key:generate
php artisan migrate
php artisan serve       # http://127.0.0.1:8000
```
Auth header: `Authorization: Bearer {token}`  
Swagger: UI `http://127.0.0.1:8000/docs`, YAML `http://127.0.0.1:8000/docs/swagger.yaml`  
Test: `php artisan test`

## Jalankan Nest.js (migrated)
```bash
cd nestjs
cp .env.example .env   # isi kredensial Postgres, JWT_SECRET acak
npm install
npm run start:dev      # http://127.0.0.1:3001
```
Base API: `http://127.0.0.1:3001/api`  
Swagger: `http://127.0.0.1:3001/docs`  
Auth header: `Authorization: Bearer {token}`  
Test: `npm run test`

## Business & Deliverables (sesuai brief)
- Dua sistem dengan domain sama; klien tidak boleh rusak saat migrasi.
- Auth/authorization konsisten; user hanya akses datanya sendiri.
- Skema relasi: User ? Projects ? Tasks (status pending|in_progress|done, optional due_date).
- Keduanya harus terdokumentasi (README, env, migrations, Swagger). No frontend.

## Git Hygiene
- `.env`/secret diabaikan; gunakan `.env.example`.
- `vendor/`, `node_modules/`, `dist/` di-ignore. Commit hanya source, migrations, docs, contoh env.
