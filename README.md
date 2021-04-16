# docker-usual-commands

available images:

https://hub.docker.com/

list containers
```bash
root@ubuntu-s-1vcpu-1gb-intel-sfo3-01:~# docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS          PORTS                                   NAMES
ef5613acd594   nginx     "/docker-entrypoint.…"   50 minutes ago   Up 50 minutes   0.0.0.0:3000->80/tcp, :::3000->80/tcp   website

docker ps -a # even the containers are not running
```

edit global variables:
```bash
nano ~/.bashrc
```

set a global variable:
```bash
export GLOBAL_VARIABLE_NAME="im a variable"
```

list all ids of containers
```bash
root@ubuntu-s-1vcpu-1gb-intel-sfo3-01:~# docker ps -aq
ef5613acd594
root@ubuntu-s-1vcpu-1gb-intel-sfo3-01:~#
```

stop a container running
```bash
docker stop [id]
```

remove a container that is not running
```bash
$  docker rm [id]
```

remove an image
```bash
docker rmi
```

remove all containers: docker rm $(docker ps -aq)
```bash
:~# docker ps -a
CONTAINER ID   IMAGE     COMMAND                  CREATED       STATUS                      PORTS     NAMES
c44d391769f1   nginx     "/docker-entrypoint.…"   3 hours ago   Exited (0) 14 minutes ago             website
root@ubuntu-s-1vcpu-1gb-intel-sfo3-01:~# docker rm $(docker ps -aq)
c44d391769f1
:~# docker ps -a
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
root@ubuntu-s-1vcpu-1gb-intel-sfo3-01:~#
```

when I use "docker run" it execute an image but if the image is not in the environment, its downloaded from docker hub
in this example we are creating a new container nxing with the code we created recently in /home/website, internally run in port 80 but outside it runs in port 3000
se esta copiando del directorio actual a /usr/share/nginx/html directory y el nombre del container se llamara website (--name), la imagen que se correra es nginx
la -d es para que corra en segundo plano
```bash
:/home/website# docker run -d -p 3000:80 -v $(pwd):/usr/share/nginx/html --name website nginx
ef5613acd59441fbb754ca7699a8454995cf88d8bdcfa283fc8d7516f0a8e45a
```
To create a container with readonly permissions (:ro)
```bash
:/home/website# docker run -d -p 3000:80 -v $(pwd):/usr/share/nginx/html:ro --name website nginx
```

to execute a linux command: create a new file (touch)
```bash
docker exec -d ubuntu_bash touch /tmp/newFile.txt
```

to access to a container like a new session: (bash)
```bash
root@ubuntu-s-1vcpu-1gb-intel-sfo3-01:/home/website# docker exec -it website bash
root@ef5613acd594:/#
```
navigate and review into a container:
```bash
root@ef5613acd594:/# cd /usr/share/nginx/html/
root@ef5613acd594:/usr/share/nginx/html# ls
about.html  index.html
root@ef5613acd594:/usr/share/nginx/html#
```
