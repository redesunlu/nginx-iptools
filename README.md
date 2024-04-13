# nginx-iptools
Upstream image of nginx-bookworm with the addition of some basic network tools for our labs

## Building and pushing the image to the 'docentetyr' Docker Hub repository
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

