# RustFS Setup Using Docker

A Docker Compose setup for [RustFS](https://github.com/RustFS/RustFS) — a high-performance, S3-compatible distributed object storage built in Rust (MinIO alternative).

## Prerequisites

- Docker and Docker Compose installed on your system

## Quick Start

```bash
docker compose up -d
```

This will start:
- RustFS S3 API on port 9000
- RustFS Console on port 9001

## Accessing RustFS

1. Open your web browser and navigate to: **http://localhost:9001**
2. Login with:
   - **Access Key:** rustfsadmin
   - **Secret Key:** rustfsadmin123

## S3 API

Point any S3 client at `http://localhost:9000` with the credentials above. Example with AWS CLI:

```bash
aws --endpoint-url http://localhost:9000 s3 ls
```

## Default Credentials

- **Access Key:** rustfsadmin
- **Secret Key:** rustfsadmin123

## Data Persistence

Data is persisted in the `rustfs_data` Docker volume, mounted at `/data` inside the container.

## Notes

- Ports 9000/9001 conflict with MinIO — don't run both at the same time
- The container runs as non-root user `rustfs` (UID 10001); if you switch to a bind mount instead of the named volume, `chown -R 10001:10001` the host directory first
- Change `RUSTFS_ACCESS_KEY` / `RUSTFS_SECRET_KEY` before exposing the server to a network
