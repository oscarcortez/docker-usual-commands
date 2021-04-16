# docker-usual-commands

available images:

https://hub.docker.com/

list containers
```bash
docker ps
docker ps -a # even the turned off
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
docker ps -aq
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
