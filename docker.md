# Docker

## Suspend all running containers
```sh
docker kill $(docker ps -q)
```

## Remove all containers
```sh
docker rm $(docker ps -a -q)
```

## Login via SSH
```sh
docker exec -i -t <container_id> bash
```
