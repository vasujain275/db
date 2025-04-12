# RabbitMQ Setup Using Docker

## To start the RabbitMQ instance

```bash
docker compose up
```

## To access the RabbitMQ Management UI

1. Open your web browser and go to http://localhost:15672
2. Login with the following credentials:
   - Username: rabbituser
   - Password: rabbitpass123

## Connection Details for Applications

- Host: rabbitmq (when connecting from other containers) or localhost (from host machine)
- Port: 5672 (AMQP) / 15672 (HTTP API)
- Virtual Host: / (default)
- Username: rabbituser
- Password: rabbitpass123

## Common Maintenance Commands

To access RabbitMQ CLI:

```bash
docker exec -it RabbitMQContainer rabbitmqctl <command>
```

To list queues:

```bash
docker exec -it RabbitMQContainer rabbitmqctl list_queues
```

To add a new user:

```bash
docker exec -it RabbitMQContainer rabbitmqctl add_user <username> <password>
```

Note: Replace `<command>` with any valid rabbitmqctl command
