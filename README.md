# Docker Files

## Cheetsheet
See https://www.digitalocean.com/community/tutorials/how-to-remove-docker-images-containers-and-volumes

### Build
```sh
cd [IMAGE]
docker build -t [IMAGE] .
```

### Run
```sh
docker run --rm -it [IMAGE] /bin/bash
```

### Images
#### Remove dangling images
```sh
docker images purge
```

#### To remove all images which are not used by existing containers
```sh
docker image prune -a
```

#### Remove all images
```sh
docker rmi $(docker images -a -q)
```

### Containers
#### Stop and remove all containers
```sh
docker stop $(docker ps -a -q)
docker rm $(docker ps -a -q)
```
