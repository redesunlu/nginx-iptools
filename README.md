# nginx-iptools
Upstream image of nginx-bookworm with the addition of some basic network tools for our labs

## Multiplatform image - Building and pushing the image to the 'docentetyr' Docker Hub repository
```commandline
$ docker login -u docentetyr
Password: <enter password>
$ docker buildx create --name nginx-builder --use
 nginx-builder
$ docker buildx inspect --bootstrap  # Check builder instance
[+] Building 2.2s (1/1) FINISHED
[ ... build process ...]
Name:          nginx-builder
Driver:        docker-container
Last Activity: 2024-04-20 01:31:36 +0000 UTC

Nodes:
Name:      nginx-builder0
Endpoint:  desktop-linux
Status:    running
Buildkit:  v0.13.1
Platforms: linux/arm64, linux/amd64, linux/amd64/v2, linux/riscv64, linux/ppc64le, linux/s390x, linux/386, linux/mips64le, linux/mips64, linux/arm/v7, linux/arm/v6
Labels:
 org.mobyproject.buildkit.worker.executor:         oci
 org.mobyproject.buildkit.worker.hostname:         448c249bb0f6
 org.mobyproject.buildkit.worker.network:          host
 org.mobyproject.buildkit.worker.oci.process-mode: sandbox
 org.mobyproject.buildkit.worker.selinux.enabled:  false
 org.mobyproject.buildkit.worker.snapshotter:      overlayfs
GC Policy rule#0:
 All:           false
 Filters:       type==source.local,type==exec.cachemount,type==source.git.checkout
 Keep Duration: 48h0m0s
 Keep Bytes:    488.3MiB
GC Policy rule#1:
 All:           false
 Keep Duration: 1440h0m0s
 Keep Bytes:    5.588GiB
GC Policy rule#2:
 All:        false
 Keep Bytes: 5.588GiB
GC Policy rule#3:
 All:        true
 Keep Bytes: 5.588GiB

$ docker buildx build --platform linux/amd64,linux/arm64 -t docentetyr/nginx-iptools --push .  # Build and push to the docker repository
[+] Building 66.6s (11/11) FINISHED
[ ... build process ...]
$ docker buildx rm nginx-builder
nginx-builder removed
```

## Single platform - Building and pushing the image to the 'docentetyr' Docker Hub repository
```comandline
$ docker build -t nginx-iptools .
[ ... build process ...]

$ docker login -u docentetyr
Password: <enter password>

$ docker tag nginx-iptools:latest docentetyr/nginx-iptools:latest
$ docker image ls                                                  
REPOSITORY                         TAG       IMAGE ID       CREATED         SIZE
docentetyr/nginx-iptools           latest    34d6c4e80cae   9 minutes ago   213MB
nginx-iptools                      latest    34d6c4e80cae   9 minutes ago   213MB
[...]

$ docker push docentetyr/nginx-iptools:latest 
The push refers to repository [docker.io/docentetyr/nginx-iptools]
26409981223d: Pushed 
fc62225e7890: Mounted from library/nginx 
75960f7ec704: Mounted from library/nginx 
4a4c3fe4d6e7: Mounted from library/nginx 
c4484f227d5e: Mounted from library/nginx 
2ee294939e65: Mounted from library/nginx 
87a8a3a2ab9c: Mounted from library/nginx 
1f00ff201478: Mounted from library/nginx 
latest: digest: sha256:62522a61895c673bd56d889e0050b4c694f50174104c6f180b0cfc636322a4d1 size: 1990
```