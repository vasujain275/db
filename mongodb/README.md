# Start local mongodb

### When `docker-compose.yml` is in the root folder

```bash
docker compose up
```

# Connection string

```bash
mongodb://<username>:<password>@localhost:27017
```

# Connect using MongoDB Compass GUI client

- Download [MongoDB Compass](https://www.mongodb.com/products/tools/compass)
- Enter the above connection string with correct `username` and `password` and hit connect
- That's it you are good to go now!

# Access the mongo shell via docker

**Run the following command to enable mongo shell:**

```bash
docker compose run mongo mongosh -u root -p example --host mongo
```

- `run` will run the command that we enter
- `mongo` is the container name that we have entered in docker compose file. This is the container in which we want to `run` the command
- `mongosh --host mongo` is the command that we want to `run`, to enter into the mongo shell
- we entered `--host mongo` because we cannot connect to `localhost:27017` inside the docker environment we need to enter host as the container name
- `-u root` this is the username that we have provided in the compose file with `MONGO_INITDB_ROOT_USERNAME: root` env var
- `-p example` this is the password that we have provided in the compose file with `MONGO_INITDB_ROOT_PASSWORD: example` env var

After running this you will see the following output:

```bash
Current Mongosh Log ID: 65916c87334d0c4c484182d6
Connecting to:          mongodb://<credentials>@mongo:27017/?directConnection=true&appName=mongosh+1.10.1
Using MongoDB:          6.0.8
Using Mongosh:          1.10.1

For mongosh info see: https://docs.mongodb.com/mongodb-shell/

------
   The server generated these startup warnings when booting
   2023-12-31T13:14:21.738+00:00: vm.max_map_count is too low
------

test>
```

Now, run `show dbs` and you will get the list of dbs as follows:

```bash
test> show dbs
admin   100.00 KiB
config  108.00 KiB
local    72.00 KiB
```

Now, you can run mongodb related commands here
