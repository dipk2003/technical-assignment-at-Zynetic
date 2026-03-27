# ⚡ High-Scale Energy Ingestion Engine

A real-time energy data ingestion engine for processing smart meter and EV telemetry data at scale. Handles 14.4M+ records/day from 10,000+ devices. Built with NestJS, TypeScript, and PostgreSQL.

![NestJS](https://img.shields.io/badge/NestJS-10-E0234E?logo=nestjs&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-98%25-blue?logo=typescript&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-Database-4169E1?logo=postgresql&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-Containerized-2496ED?logo=docker&logoColor=white)

---

## ✨ Features

- **Polymorphic Ingestion** — Handles both meter (AC energy) and vehicle (DC energy) telemetry
- **Dual-Store Strategy** — Hot tables for operational reads, cold tables for historical analytics
- **Upsert Patterns** — Out-of-order event handling with timestamp guards
- **Real-Time Correlation** — Links meters to vehicles for cross-device analytics
- **Bounded Analytics** — 24-hour performance metrics with indexed queries
- **High Scale** — Designed for 14.4M+ records/day from 10,000+ devices
- **Docker Ready** — Full containerization with Docker Compose

---

## 🛠️ Tech Stack

| Technology | Purpose |
|---|---|
| NestJS 10 | Node.js backend framework |
| TypeScript | Type-safe development |
| PostgreSQL | Primary database |
| Docker + Docker Compose | Containerization |
| class-validator | Request validation |
| class-transformer | Data transformation |

---

## 📡 API Endpoints

| Method | Endpoint | Description |
|---|---|---|
| `POST` | `/v1/ingest` | Ingest energy telemetry data |
| `PUT` | `/v1/links` | Map vehicle to meter |
| `GET` | `/v1/analytics/performance/:vehicleId` | 24h performance metrics |
| `GET` | `/v1/status/vehicle/:vehicleId` | Latest vehicle status |
| `GET` | `/v1/status/meter/:meterId` | Latest meter status |

---

## 📁 Project Structure

```
technical-assignment-at-Zynetic/
├── src/
│   ├── main.ts             # App entry point
│   ├── config/             # Configuration management
│   ├── ingestion/          # Core ingestion logic
│   ├── services/           # Business logic
│   ├── controllers/        # API endpoints
│   └── models/             # Data models
├── db/migrations/          # PostgreSQL migrations
├── Dockerfile
├── docker-compose.yml
├── .env.example
├── tsconfig.json
└── package.json
```

---

## 🚀 Quick Start

### With Docker (Recommended)

```bash
git clone https://github.com/dipk2003/technical-assignment-at-Zynetic.git
cd technical-assignment-at-Zynetic
docker compose up --build
```

API listens on `http://localhost:3000`

### Manual Setup

```bash
npm install
npm run start:dev    # Development with hot-reload
npm run build        # Compile TypeScript
npm run start        # Production
```

### Environment Variables

```env
DATABASE_URL=postgresql://user:password@localhost:5432/energy_db
USE_DATABASE_POOLER=true
```

---

## 🏗️ Architecture

```
Telemetry Data (Meters + EVs)
    ↓
POST /v1/ingest
    ↓
┌─────────────────────────────────┐
│  Polymorphic Parser             │
│  (AC meter vs DC vehicle)       │
└─────────────┬───────────────────┘
              ↓
┌─────────────────────────────────┐
│  Dual Store                     │
│  Hot Table → Latest state       │
│  Cold Table → Full audit trail  │
└─────────────┬───────────────────┘
              ↓
GET /v1/analytics → Indexed range scans
```

---

Made with ❤️ by [Dipanshu Pandey](https://github.com/dipk2003)