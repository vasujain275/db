# Postgress Database Setup Using Docker

# To get the instance up and running -
```zsh
docker compose up
```

# To access psql command - 
```zsh
docker exec -it containerName psql -U Username -W dbName
```

# To access Adminer

- `System` : PostgresSQL
- `Server` : postgres_db
- `Username` : postgres
- `Password` : postgres123
- `Database` : dbName
