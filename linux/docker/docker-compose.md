# Docker Compose
These commands can be used within the directory, the `docker-compose.yml` file resides in.

## Start all containers
```bash
docker-compose up
```

Append `-d` if you want to run the containers in the background.

## Stop and remove all containers
```bash
docker-compose down
```

## Restart a single container/service
```bash
docker-compose restart <service-name>
```
