```sh
docker kill $(docker ps -q)
```

```sh
docker rm $(docker ps -a -q)
```

```sh
docker exec -i -t <container_id> bash
```
