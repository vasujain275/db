# PostgreSQL 18 Database Setup Using Docker

A Docker Compose setup for PostgreSQL 18 with pgAdmin 4 for easy database management.

## Prerequisites

- Docker and Docker Compose installed on your system

## Quick Start

### Start the services

```bash
docker compose up -d
```

This will start:
- PostgreSQL 18 (Alpine) on port 5432
- pgAdmin 4 on port 8432

### Stop the services

```bash
docker compose down
```

### Stop and remove all data

```bash
docker compose down -v
```

## Accessing PostgreSQL

### Via psql command line

Access the PostgreSQL command line interface:

```bash
docker exec -it PostgresCont psql -U postgres
```

To connect to a specific database:

```bash
docker exec -it PostgresCont psql -U postgres -d dbName
```

### Via pgAdmin Web Interface

1. Open your web browser and navigate to: **http://localhost:8432**

2. Login with these credentials:
   - **Email:** admin@example.com
   - **Password:** admin

3. Add a new server connection:
   - Click **"Add New Server"** (or right-click "Servers" → "Register" → "Server")
   
   - **General Tab:**
     - Name: `Local PostgreSQL` (or any name you prefer)
   
   - **Connection Tab:**
     - Host name/address: `postgres_db`
     - Port: `5432`
     - Maintenance database: `postgres`
     - Username: `postgres`
     - Password: `postgres123`
   
   - Click **"Save"**

## Default Credentials

### PostgreSQL
- **User:** postgres
- **Password:** postgres123
- **Default Database:** postgres

### pgAdmin
- **Email:** admin@example.com
- **Password:** admin

## Creating a New Database

### Using psql

```bash
docker exec -it PostgresCont psql -U postgres -c "CREATE DATABASE mydb;"
```

### Using pgAdmin

1. Connect to the server (see above)
2. Right-click on "Databases" → "Create" → "Database"
3. Enter your database name and click "Save"

## Data Persistence

Data is persisted in Docker volumes:
- `postgres_db` - PostgreSQL data
- `pgadmin_data` - pgAdmin configuration and settings

These volumes will persist even after stopping the containers.

## Health Check

The PostgreSQL container includes a health check that verifies the database is ready to accept connections. pgAdmin will wait for PostgreSQL to be healthy before starting.

## Customization

To change default passwords or ports, edit the `docker-compose.yml` file:

- PostgreSQL password: Update `POSTGRES_PASSWORD`
- PostgreSQL port: Change `"5432:5432"` to `"<your-port>:5432"`
- pgAdmin port: Change `"8432:80"` to `"<your-port>:80"`
- pgAdmin credentials: Update `PGADMIN_DEFAULT_EMAIL` and `PGADMIN_DEFAULT_PASSWORD`

## Troubleshooting

### Check container logs

```bash
# PostgreSQL logs
docker logs PostgresCont

# pgAdmin logs
docker logs PgAdminCont
```

### Check container status

```bash
docker compose ps
```

### Restart services

```bash
docker compose restart
```

## Notes

- The PostgreSQL 18 Alpine image is used for a smaller footprint
- Services are set to restart unless manually stopped
- pgAdmin is configured in desktop mode for easier local development
