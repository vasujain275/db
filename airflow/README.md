# Apache Airflow Docker Setup

This project sets up a local [Apache Airflow](https://airflow.apache.org/) instance using Docker Compose.

## Components

1. Airflow Webserver
2. Airflow Scheduler
3. Airflow Metadata Database (PostgreSQL)

## Setup Instructions

1. Ensure you have Docker and Docker Compose installed.
2. Save the provided `docker-compose.yml` file in this folder.
3. Open a terminal in this directory and run:

```bash
docker compose up -d
```

## Access Information

### Airflow UI

- **URL**: http://localhost:8088
- **Username**: admin
- **Password**: admin

### Metadata Database

- **Host**: localhost
- **Port**: 5433
- **User**: airflow
- **Password**: airflow
- **Database**: airflow

## Stop the Services

```bash
docker compose down
```

To remove the persisted data volume as well:

```bash
docker compose down -v
```

## Notes

- DAGs are mounted from `./dags`.
- Logs are persisted in `./logs`.
- Plugins are mounted from `./plugins`.
- The setup uses `LocalExecutor` for a simple local deployment.
