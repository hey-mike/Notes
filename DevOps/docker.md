### Stop all containers
docker stop $(docker ps -a -q)
### Delete all containers
docker rm $(docker ps -a -q)
### Delete all images
docker rmi $(docker images -q)

 If you need to go inside the container you can use the exec command:
```
# Enter the container
$ docker exec -it <container id> /bin/bash
```

## Production *docker-compose*

```
$ docker-compose build web
$ docker-compose up --no-deps -d web
```
This will first rebuild the image for `web` and then stop, destroy, and recreate just the web service. The `--no-deps` flag prevents Compose from also recreating any services which `web` depends on.


truncate -s 0 /var/lib/docker/containers/*/*-json.log
