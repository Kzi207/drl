# DRL2

He thong quan ly diem ren luyen, diem danh va minh chung anh.

Du an duoc tach thanh 2 phan:

- frontend: React + Vite (UI + proxy API)
- backend: Express + TypeScript + PostgreSQL (Neon) + Cloudflare R2

## Muc tieu

- Sinh vien tu cham diem ren luyen va upload minh chung
- Ban can su lop/BCH duyet diem theo quy trinh
- Quan tri vien quan ly lop, sinh vien, hoc ky, backup

## Cau truc thu muc

- frontend/: giao dien va proxy
- backend/: API, DB layer, migration, backup
- backend/database/drl.sql: schema SQL tong hop (PostgreSQL)

## Yeu cau he thong

- Node.js 18+
- npm
- Tai khoan Neon PostgreSQL
- Bucket Cloudflare R2 (neu dung upload minh chung)

## Huong dan chay local

### Buoc 1 - Cai package

Tai root project:

```bash
npm --prefix backend install
npm --prefix frontend install
```

### Buoc 2 - Cau hinh environment

Backend (backend/.env):

- API_KEY
- NEON_DATABASE_URL
- R2_ENDPOINT
- R2_ACCESS_KEY_ID
- R2_SECRET_ACCESS_KEY
- R2_BUCKET_NAME
- R2_PUBLIC_BASE_URL
- PAYLOAD_ENCRYPTION_KEY (tuy chon)

Frontend (frontend/.env):

- VITE_API_BASE=http://localhost:3004
- VITE_API_KEY=... (giong backend API_KEY)
- VITE_PAYLOAD_ENCRYPTION_KEY=... (neu bat ma hoa payload)
- VITE_PAYLOAD_ENCRYPTION_SCOPE=auth (khuyen nghi de nhe he thong)

### Buoc 3 - Khoi tao schema

Chay schema tong hop:

```bash
psql "$NEON_DATABASE_URL" -f backend/database/drl.sql
```

Neu ban da dung script setup hien tai:

```bash
npm --prefix backend run build:db
```

### Buoc 4 - Chay backend

```bash
npm --prefix backend start
```

Kiem tra:

```bash
curl -H "x-api-key: YOUR_API_KEY" http://localhost:3004/status
```

### Buoc 5 - Chay frontend

```bash
npm --prefix frontend run dev
```

Mo trinh duyet tai:

- http://localhost:3000

## Scripts nhanh

Backend:

- npm --prefix backend start
- npm --prefix backend run dev
- npm --prefix backend run typecheck

Frontend:

- npm --prefix frontend run dev
- npm --prefix frontend run build
- npm --prefix frontend run lint

## Xu ly loi thuong gap

- Loi port dang bi chiem (EADDRINUSE):
	- backend: kiem tra cong 3004
	- frontend: kiem tra cong 3000 va websocket 24678
- Loi upload anh 404/500:
	- kiem tra cau hinh R2 va API proxy
- Loi API key:
	- dam bao VITE_API_KEY va backend API_KEY giong nhau

## Tai lieu chi tiet

- Backend docs: backend/README.md
- API docs: backend/API_DOCUMENTATION.md
- Database notes: backend/database/README.md

## Quy tac git

- Khong commit file .env
- Khong commit node_modules, backup, upload runtime
- Da cau hinh san trong .gitignore root va backend/.gitignore
