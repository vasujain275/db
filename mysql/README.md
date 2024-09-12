# MySQL Docker Setup

This project sets up a MySQL database with Adminer (a database management tool) using Docker Compose.

## Components

1. MySQL Database
2. Adminer (Database management tool)

## Setup Instructions

1. Ensure you have Docker and Docker Compose installed on your system.
2. Save the provided `docker-compose.yml` file in your project directory.
3. Open a terminal, navigate to the project directory, and run:
   ```
   docker-compose up -d
   ```

## Access Information

### MySQL Database

- **Host**: localhost
- **Port**: 3306
- **Root Username**: root
- **Root Password**: rootpassword
- **Database Name**: mydb
- **Regular User**: mysql
- **Regular User Password**: mysql123

To access the MySQL shell, use the following command:

```
docker exec -it MySQLCont mysql -u root -p
```

When prompted, enter the root password: `rootpassword`

### Adminer

- **URL**: http://localhost:8080
- **Server**: mysql_db
- **Username**: root
- **Password**: rootpassword

## Additional Commands

- To stop the containers:
  ```
  docker-compose down
  ```
- To view container logs:
  ```
  docker-compose logs
  ```
- To restart containers:
  ```
  docker-compose restart
  ```

## Notes

- Data is persisted in a Docker volume named `mysql_db`.
- Make sure ports 3306 and 8080 are not in use by other applications on your system.
- For security in a production environment, consider changing the default passwords and not exposing the MySQL port (3306) publicly.
