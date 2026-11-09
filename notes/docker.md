# Docker

## Containers

```bash
docker ps -a                          # list all containers
docker stop $(docker ps -q)           # stop all running containers
docker rm -f <container_id>           # force remove container
docker logs -f --tail 100 <container> # stream recent logs
```

## Cleanup & Prune

```bash
docker system prune -af               # purge unused containers, networks, images
docker volume prune -f                # purge dangling volumes
```

## Quick Ephemeral Run

```bash
docker run --rm -it -p 3306:3306 -e MYSQL_ROOT_PASSWORD=root mysql:8.4
```
