# Dockerfile
Sirve para crear una imagen siguiendo una serie de instrucciones

FROM: Para descargar una imagen: imagen : version_imagen
```shell
FROM ubuntu:14.04
```

RUN: Ejecutar comandos (apt-get, yum install)

ENV: Para variables de entorno

En este ejemmplo vemos como se inicia un servicio nginx con:
```shell
root@ubuntu-s-1vcpu-1gb-intel-sfo3-01:/home/website# cat Dockerfile
FROM nginx:latest

WORKDIR /usr/share/nginx/html

COPY . .
```
Lo que hace es crear una imagen nginx, la ultima version: FROM nginx:latest
luego se define el directorio de trabajo donde se ejecuta cualquier comando de accion como: RUN, CMD, ADD, COPY
Despues copia todo el contenido de la direccion actual donde se encuentra el Dockerfile, que en este caso tiene: about, index, services
```shell
root@ubuntu-s-1vcpu-1gb-intel-sfo3-01:~# cd /home/website/
root@ubuntu-s-1vcpu-1gb-intel-sfo3-01:/home/website# ls
Dockerfile  about.html  index.html  services.html
root@ubuntu-s-1vcpu-1gb-intel-sfo3-01:/home/website#
```

To build the Dockerfile:
```shell
root@ubuntu-s-1vcpu-1gb-intel-sfo3-01:/home/website# docker build -t websitebuilt .
Sending build context to Docker daemon  4.608kB
Step 1/3 : FROM nginx:latest
 ---> 62d49f9bab67
Step 2/3 : WORKDIR /usr/share/nginx/html
 ---> Running in 8a9728afb509
Removing intermediate container 8a9728afb509
 ---> ea0d1e698fec
Step 3/3 : COPY . .
 ---> 64dd0fc98714
Successfully built 64dd0fc98714
Successfully tagged websitebuilt:latest
root@ubuntu-s-1vcpu-1gb-intel-sfo3-01:/home/website#
```

To be sure image websitebuilt were created:
```shell
root@ubuntu-s-1vcpu-1gb-intel-sfo3-01:/home/website# docker images
REPOSITORY     TAG       IMAGE ID       CREATED          SIZE
websitebuilt   latest    64dd0fc98714   46 seconds ago   133MB
nginx          latest    62d49f9bab67   3 days ago       133MB
root@ubuntu-s-1vcpu-1gb-intel-sfo3-01:/home/website#
```

Until here we have the image created but not the container
```shell
root@ubuntu-s-1vcpu-1gb-intel-sfo3-01:~# docker ps -a
CONTAINER ID   IMAGE     COMMAND                  CREATED       STATUS       PORTS                                   NAMES
ef5613acd594   nginx     "/docker-entrypoint.…"   4 hours ago   Up 4 hours   0.0.0.0:3000->80/tcp, :::3000->80/tcp   website
```
To run the container using the recently created image websitebuilt:
```shell
root@ubuntu-s-1vcpu-1gb-intel-sfo3-01:~# docker run -p 7000:80 -d --name websiteapp websitebuilt
6ba79df6f00e48b651eff2bc6a2ded06df19f4488c233c6180e1f8ebe1a8d1a8
```
- port: 7000 externally, 
- internally port: 80
- -d: run in background
- container name: websiteapp (name doesnt accept uppercase)
- the last variable is the image name: website build

![nginx_7000](https://user-images.githubusercontent.com/48032479/115093645-00a03500-9ee9-11eb-9a7d-5c0c12b84653.gif)

Optionally we can remove the current container
```shell
root@ubuntu-s-1vcpu-1gb-intel-sfo3-01:~# docker ps
CONTAINER ID   IMAGE          COMMAND                  CREATED          STATUS          PORTS                                   NAMES
6ba79df6f00e   websitebuilt   "/docker-entrypoint.…"   23 minutes ago   Up 23 minutes   0.0.0.0:7000->80/tcp, :::7000->80/tcp   websiteapp
ef5613acd594   nginx          "/docker-entrypoint.…"   4 hours ago      Up 4 hours      0.0.0.0:3000->80/tcp, :::3000->80/tcp   website
root@ubuntu-s-1vcpu-1gb-intel-sfo3-01:~# docker stop websiteapp
websiteapp
root@ubuntu-s-1vcpu-1gb-intel-sfo3-01:~# docker rm websiteapp
websiteapp
root@ubuntu-s-1vcpu-1gb-intel-sfo3-01:~# docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED       STATUS       PORTS                                   NAMES
ef5613acd594   nginx     "/docker-entrypoint.…"   4 hours ago   Up 4 hours   0.0.0.0:3000->80/tcp, :::3000->80/tcp   website
root@ubuntu-s-1vcpu-1gb-intel-sfo3-01:~#
```

