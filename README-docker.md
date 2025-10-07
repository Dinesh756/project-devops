# Docker and docker-compose for Job-Web-Application

This repository now includes Dockerfiles for `backend` and `frontend` and a `docker-compose.yml` to run a local stack with MongoDB.

Quick steps (PowerShell):

1. Build and start everything:

```powershell
docker-compose up --build
```

2. Open the frontend at http://localhost:5173
3. Backend API: http://localhost:3001/api

Notes:
- The compose file uses a local `mongo` service and sets `MONGO_URI` to `mongodb://mongo:27017/jobdb`. If you prefer Atlas, replace the value in `backend/.env`.
- Backend Dockerfile performs a TypeScript build and runs `dist/server.js` on port 3001.
- Frontend is built with Vite and served by nginx; nginx proxies `/api` to `http://backend:3001/api/`.
- On Windows use PowerShell and ensure Docker Desktop is running.

If you want me to also add a healthcheck, improved production optimizations, or a `.env.example`, tell me which variables you want exposed.
