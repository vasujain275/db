# Weaviate Docker Setup

This project sets up a local [Weaviate](https://weaviate.io/) vector database using Docker Compose.

## Components

1. Weaviate Vector Database

## Setup Instructions

1. Ensure you have Docker and Docker Compose installed.
2. Save the provided `docker-compose.yml` file in this folder.
3. Open a terminal in this directory and run:

```bash
docker compose up -d
```

## Access Information

### Weaviate

- **HTTP API**: http://localhost:8080
- **gRPC API**: localhost:50051

### Example Meta Check

```bash
curl http://localhost:8080/v1/meta
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

- Data is persisted in the Docker volume `weaviate_data`.
- Anonymous access is enabled for local development only.
- If you want to use vectorizer or generative modules, extend the compose file with the required module services and environment variables.
