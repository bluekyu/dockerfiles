# Dockerfiles

![linux-actions-svg](https://github.com/bluekyu/dockerfiles/workflows/Linux%20Images/badge.svg)

Dockerfile repository for my projects (https://github.com/bluekyu)

| Images            | Notes                                      | Status                                               |
| :---------------: | :----------------------------------------: | :--------------------------------------------------: |
| linux-base        | Clang & Python image                       | [![badge-image-linux-base]][link-dockerhub]          |
| linux-android-sdk | Android SDK image from base                | [![badge-image-linux-android-sdk]][link-dockerhub]   |
| linux-android-ndk | Android NDK image from Android SDK         | [![badge-image-linux-android-ndk]][link-dockerhub]   |
| windows-msvc16    | Visual Studio 2019 and Clang/LLVM image    |                                                      |



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



[badge-image-linux-base]: https://images.microbadger.com/badges/image/bluekyu/dockerfiles:linux-base.svg
[badge-image-linux-android-sdk]: https://images.microbadger.com/badges/image/bluekyu/dockerfiles:linux-android-sdk.svg
[badge-image-linux-android-ndk]: https://images.microbadger.com/badges/image/bluekyu/dockerfiles:linux-android-ndk.svg
[link-dockerhub]: https://hub.docker.com/r/bluekyu/dockerfiles
