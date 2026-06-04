# MinIO Docker Setup

This project sets up a local [MinIO](https://min.io/) object storage server using Docker Compose.

## Components

1. MinIO Object Storage
2. MinIO Console

## Setup Instructions

1. Ensure you have Docker and Docker Compose installed.
2. Save the provided `docker-compose.yml` file in this folder.
3. Open a terminal in this directory and run:

```bash
docker compose up -d
```

## Access Information

### MinIO

- **S3 API**: http://localhost:9000
- **Console**: http://localhost:9001
- **Username**: minioadmin
- **Password**: minioadmin123

### Example Health Check

```bash
curl http://localhost:9000/minio/health/live
```

## Stop the Services

```bash
docker compose down
```

To remove the persisted data volume as well:

```bash
docker compose down -v
```

## Notes

- Data is persisted in the Docker volume `minio_data`.
- The console is exposed on port `9001`.
- For production, change the default credentials and use secure transport.
