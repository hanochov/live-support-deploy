# Live Support – Docker Setup

This repository contains the deployment setup for the **Live Support system** (API and Dashboard) using **Docker Compose**.  
It automatically pulls both submodules:

- **Backend (API):** .NET 8 / SQLite / SignalR  
- **Frontend (Dashboard):** Vite / React / TypeScript / MUI  

---

## Run the system (standard setup)

Run the following commands in **CMD**, **PowerShell**, or any terminal:

```bash
git clone --recurse-submodules https://github.com/hanochov/live-support-deploy.git
cd live-support-deploy
docker compose up -d --build
```

After a few moments:

- Backend is available at: http://localhost:8080/health  
- Swagger UI:  http://localhost:8080/swagger
- Frontend is available at: http://localhost:8081  

---

## Reset the database (optional)

If an old SQLite database already exists and you want to re-run the initial seed data, run:


docker compose down --volumes --rmi all
docker compose up -d --build --force-recreate


This removes the old `/data/app.db` volume and triggers a new migration and seed.

---

## Requirements

Before running the project, make sure the following are installed:

```bash
docker --version
docker compose version
git --version
```

Also verify that **Docker Desktop is running**.

**Important:**
- Ensure that both containers (`livesupport-api` and `livesupport-web`) are in the **running** state (green "Play" icon) in Docker Desktop.  
- Verify that the **Dev Environment** in Docker Desktop is active.  
- If one of the containers is stopped, click the **Play** icon next to it to start it manually.

---

## Project structure

```
live-support-deploy/
 ├── docker-compose.yml        # Compose configuration for API and Web
 ├── .env                      # Environment variables (project name, etc.)
 ├── live-support/             # Backend (.NET)
 ├── support-dashboard/        # Frontend (React)
 └── README.md                 # This file
```

---

## Additional notes

- The first build may take several minutes while Docker downloads and builds images.  
- If the **web** service is waiting for the **api**, this is normal until the API health check passes.  
- To view logs, run:
  ```bash
  docker logs livesupport-api
  docker logs livesupport-web
  ```
- You can manage and monitor containers directly from **Docker Desktop → Containers tab**.
