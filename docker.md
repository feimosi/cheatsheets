# Docker

## Suspend all running containers
```sh
docker kill $(docker ps -q)
```

## Remove all containers
```sh
docker rm $(docker ps -a -q)
```

## Remove all images
```sh
docker images -q | xargs docker rmi
```

## Login via SSH
```sh
docker exec -i -t <container_id> bash
```

# Docker Compose

## Run a container

```sh
docker-compose -f docker-compose-dev.yml run -d --service-ports --rm --no-deps api npm start
```

* `-d` - Detached mode: Run container in the background
* `-rm` - Remove container after run. Ignored in detached mode
* `--no-deps` - Don't start linked services
* `--service-ports` - Run command with the service's ports enabled and mapped to the host

## Restart a container

```sh
docker-compose restart api
```

## Kill a container

```sh
docker-compose kill api
```

## Remove Dangling Docker Images

```sh
docker system prune
```

In older versions of Docker (and this still works today), you can delete dangling images on their own by running `docker rmi -f $(docker images -f "dangling=true" -q)`.

But with newer versions of Docker (1.13+) there’s an even better command called `docker system prune` which will not only remove dangling images but it will also remove all stopped containers, all networks not used by at least 1 container, all dangling images and build caches.
