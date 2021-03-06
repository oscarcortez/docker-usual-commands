# publish-push-create-repository

create the image to be pushed to docker hub: oscarkortez/website
```shell
root@ubuntu-s-1vcpu-1gb-intel-sfo3-01:/home/website# docker build -t oscarkortez/website .
Sending build context to Docker daemon  4.608kB
Step 1/3 : FROM nginx:latest
 ---> 62d49f9bab67
Step 2/3 : WORKDIR /usr/share/nginx/html
 ---> Using cache
 ---> ea0d1e698fec
Step 3/3 : COPY . .
 ---> Using cache
 ---> 64dd0fc98714
Successfully built 64dd0fc98714
Successfully tagged oscarkortez/website:latest
root@ubuntu-s-1vcpu-1gb-intel-sfo3-01:/home/website#
root@ubuntu-s-1vcpu-1gb-intel-sfo3-01:/home/website# docker images
REPOSITORY            TAG       IMAGE ID       CREATED       SIZE
websitebuilt          latest    64dd0fc98714   3 hours ago   133MB
oscarkortez/website   latest    64dd0fc98714   3 hours ago   133MB
nginx                 latest    62d49f9bab67   3 days ago    133MB
```

Now login with you docker hub account: https://hub.docker.com/
```shell
root@ubuntu-s-1vcpu-1gb-intel-sfo3-01:/home/website# docker login
Login with your Docker ID to push and pull images from Docker Hub. If you don't have a Docker ID, head over to https://hub.docker.com to create one.
Username: oscarkortez
Password:
WARNING! Your password will be stored unencrypted in /root/.docker/config.json.
Configure a credential helper to remove this warning. See
https://docs.docker.com/engine/reference/commandline/login/#credentials-store

Login Succeeded
root@ubuntu-s-1vcpu-1gb-intel-sfo3-01:/home/website#
```


Push the image to docker hub
```shell
root@ubuntu-s-1vcpu-1gb-intel-sfo3-01:/home/website# docker push oscarkortez/website
Using default tag: latest
The push refers to repository [docker.io/oscarkortez/website]
40bd3d63ac39: Pushed
64ee8c6d0de0: Mounted from library/nginx
974e9faf62f1: Mounted from library/nginx
15aac1be5f02: Mounted from library/nginx
23c959acc3d0: Mounted from library/nginx
4dc529e519c4: Mounted from library/nginx
7e718b9c0c8c: Mounted from library/nginx
latest: digest: sha256:9726cdfda44f7245cddd036f1f11418ebd24000ac57f627e7e5f4e2354a2c96a size: 1777
root@ubuntu-s-1vcpu-1gb-intel-sfo3-01:/home/website#
```

![Image 2](https://user-images.githubusercontent.com/48032479/115098802-0bb28f80-9f00-11eb-88aa-88a3474ce8e6.gif)


remove all available images and containers to be sure
```shell
root@ubuntu-s-1vcpu-1gb-intel-sfo3-01:/home/website# docker rm $(docker ps -aq) -f
ef5613acd594
root@ubuntu-s-1vcpu-1gb-intel-sfo3-01:/home/website#
root@ubuntu-s-1vcpu-1gb-intel-sfo3-01:/home/website#
root@ubuntu-s-1vcpu-1gb-intel-sfo3-01:/home/website# docker rmi $(docker images -aq) -f
Untagged: websitebuilt:latest
Untagged: oscarkortez/website:latest
Untagged: oscarkortez/website@sha256:9726cdfda44f7245cddd036f1f11418ebd24000ac57f627e7e5f4e2354a2c96a
Deleted: sha256:64dd0fc98714cb05ac34a2788f38ca04fc9d8869b2199168e71f5c707301c0b8
Deleted: sha256:01f2a8fb37b63ef55269f7b2c3c2ae4601eaf311579edfcada1d1c681f28bb81
Deleted: sha256:ea0d1e698fec483a640e789554c609bed0eaabe3bc44af3bfbf349d28599f13d
Untagged: nginx:latest
Untagged: nginx@sha256:75a55d33ecc73c2a242450a9f1cc858499d468f077ea942867e662c247b5e412
Deleted: sha256:62d49f9bab67f7c70ac3395855bf01389eb3175b374e621f6f191bf31b54cd5b
Deleted: sha256:3444fb58dc9e8338f6da71c1040e8ff532f25fab497312f95dcee0f756788a84
Deleted: sha256:f85cfdc7ca97d8856cd4fa916053084e2e31c7e53ed169577cef5cb1b8169ccb
Deleted: sha256:704bf100d7f16255a2bc92e925f7007eef0bd3947af4b860a38aaffc3f992eae
Deleted: sha256:d5955c2e658d1432abb023d7d6d1128b0aa12481b976de7cbde4c7a31310f29b
Deleted: sha256:11126fda59f7f4bf9bf08b9d24c9ea45a1194f3d61ae2a96af744c97eae71cbf
Deleted: sha256:7e718b9c0c8c2e6420fe9c4d1d551088e314fe923dce4b2caf75891d82fb227d
Error response from daemon: conflict: unable to delete ea0d1e698fec (cannot be forced) - image has dependent child images
Error: No such image: 64dd0fc98714
root@ubuntu-s-1vcpu-1gb-intel-sfo3-01:/home/website# docker images
REPOSITORY   TAG       IMAGE ID   CREATED   SIZE
root@ubuntu-s-1vcpu-1gb-intel-sfo3-01:/home/website#
root@ubuntu-s-1vcpu-1gb-intel-sfo3-01:/home/website#
root@ubuntu-s-1vcpu-1gb-intel-sfo3-01:/home/website# docker ps -a
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
root@ubuntu-s-1vcpu-1gb-intel-sfo3-01:/home/website#
```

execute this command: docker push oscarkortez/website:tagname

![Image 4](https://user-images.githubusercontent.com/48032479/115098946-e5d9ba80-9f00-11eb-809f-c7f8be345193.gif)


```shell
root@ubuntu-s-1vcpu-1gb-intel-sfo3-01:~# docker images
REPOSITORY   TAG       IMAGE ID   CREATED   SIZE
root@ubuntu-s-1vcpu-1gb-intel-sfo3-01:~#
```

Pull the current image
```shell
root@ubuntu-s-1vcpu-1gb-intel-sfo3-01:~# docker pull oscarkortez/website
Using default tag: latest
latest: Pulling from oscarkortez/website
f7ec5a41d630: Pull complete
aa1efa14b3bf: Pull complete
b78b95af9b17: Pull complete
c7d6bca2b8dc: Pull complete
cf16cd8e71e0: Pull complete
0241c68333ef: Pull complete
50571d0eaf48: Pull complete
Digest: sha256:9726cdfda44f7245cddd036f1f11418ebd24000ac57f627e7e5f4e2354a2c96a
Status: Downloaded newer image for oscarkortez/website:latest
docker.io/oscarkortez/website:latest
root@ubuntu-s-1vcpu-1gb-intel-sfo3-01:~# 
```

review the current images:
```shell
root@ubuntu-s-1vcpu-1gb-intel-sfo3-01:~# docker images
REPOSITORY            TAG       IMAGE ID       CREATED       SIZE
oscarkortez/website   latest    64dd0fc98714   4 hours ago   133MB
root@ubuntu-s-1vcpu-1gb-intel-sfo3-01:~#
```

we notice the container doesnt exist yet
```shell
root@ubuntu-s-1vcpu-1gb-intel-sfo3-01:~# docker ps -a
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```
run the container
```shell
root@ubuntu-s-1vcpu-1gb-intel-sfo3-01:~# docker run -d -p 3000:80 --name sitioweb oscarkortez/website
571e9651f855376eb3fb57a6b2085b2ec0548ff11183eac9177ffd679fe58e6e
```

![Image 5](https://user-images.githubusercontent.com/48032479/115099466-06574400-9f04-11eb-9c28-5061ae5faf7c.gif)

```shell
root@ubuntu-s-1vcpu-1gb-intel-sfo3-01:~# docker ps -a
CONTAINER ID   IMAGE                 COMMAND                  CREATED         STATUS         PORTS                                   NAMES
571e9651f855   oscarkortez/website   "/docker-entrypoint.???"   5 minutes ago   Up 5 minutes   0.0.0.0:3000->80/tcp, :::3000->80/tcp   sitioweb
```
