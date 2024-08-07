# PostgreSQL Database Setup Using Docker

## To get the instance up and running

docker compose up

## To access psql command

docker exec -it PostgresCont psql -U postgres -W dbName

## To access pgAdmin

1. Open your web browser and go to http://localhost:8432
2. Login with the following credentials:

   - Email: admin@example.com
   - Password: admin

3. To add a new server in pgAdmin:
   - Click "Add New Server"
   - In the "General" tab:
     - Name: Choose any name for your server
   - In the "Connection" tab:
     - Host name/address: postgres_db
     - Port: 5432
     - Maintenance database: postgres
     - Username: postgres
     - Password: postgres123

Note: Replace dbName with your actual database name if you've created one.
