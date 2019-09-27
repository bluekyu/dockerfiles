# Dockerfiles

Dockerfile repository for my projects (https://github.com/bluekyu)



## Files
```
─ dockerfiles
  ├ linux
  │  ├ base         : Clang & Python image
  │  │ android-sdk  : Android SDK image from base
  │  └ android-ndk  : Android NDK image from Android SDK
  └ windows
     └ msvc16       : Visual Studio 2019 and Clang/LLVM image
```



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
