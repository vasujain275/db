# Qdrant Vector Database with Docker Compose

This repository contains a simple Docker Compose setup for running [Qdrant](https://qdrant.tech/) with persistent storage.

---

## Prerequisites

- Docker Engine ≥ 19.03
- Docker Compose ≥ 1.27
- (Optional) `make` for convenience commands

---

## Getting Started

1. **Clone or copy** this folder to your machine.

2. **Start Qdrant**

   ```bash
   docker-compose up -d
   ```

   - Pulls the latest `qdrant/qdrant` image
   - Exposes ports:
     - `6333` for REST API & Web UI
     - `6334` for gRPC API

3. **Verify**
   ```bash
   docker-compose ps
   ```
   You should see the `qdrant` service running.

---

## Accessing Qdrant

- **REST API** & **Web UI**:  
  http://localhost:6333
  - Dashboard at `/dashboard`
- **gRPC API**:  
  `localhost:6334`

---

## Persistent Storage

Data is stored in the Docker volume `qdrant_storage`, which maps to `/qdrant/storage` inside the container. Even if you recreate or upgrade the service, your collections and points remain intact.

- **Inspect volume location** (host):
  ```bash
  docker volume inspect yourfolder_qdrant_storage
  ```

---

## Common Commands

- **Stop and remove containers** (preserves data):
  ```bash
  docker-compose down
  ```
- **Stop, remove, and delete volumes** (dangerous—data loss):
  ```bash
  docker-compose down -v
  ```
- **View logs**:
  ```bash
  docker-compose logs -f qdrant
  ```
