# Simple Docker commands
For single container usage.

## List all running containers
```bash
docker ps
```
The `-a` option lists all stopped containers as well, `-q` only the container Id's.

## Run command in container
```bash
docker exec -it <container-name> <command>

# as long as bash is installed in the container, this command is
# very useful if you want to enter a container for debugging:
docker exec -it <container-name> bash
```

## Get details about a container
```bash
docker inspect <container-name>
```
You can extract information about labels, IP addresses, mounted volumes, etc. here. Its possible to filter the output.

## Stop a container
```bash
docker stop <container-name>
```

## Remove a stopped container
```bash
docker rm <container-name>
```
Use `-f` to delete a running container.

## List locally available images
```bash
docker images
```

## Remove all containers
```bash
docker rm $(docker ps -aq)
```

## Delete all local images
```bash
docker rmi $(docker images -q)
```

## Create new network
```bash
docker network create -d <network type> <network name>
```
