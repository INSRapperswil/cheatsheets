# Docker-Machine Commands
A few commands for docker-machine to create a local Swarm Cluster

## Create new virtual machine
```bash
sudo docker-machine create <vm name>
```

## Execute SSH commands in a vm
```bash
docker-machine ssh <vm name> "<command>"
```

## Shell environment
To use the docker cli in your terminal window
```bash
eval $(docker-machine env <vm name>)
```
