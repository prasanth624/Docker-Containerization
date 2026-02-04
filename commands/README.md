#### Check Docker Version
```bash
[prasanth@localhost ~]# docker --version
Docker version 26.1.3, build b72abbb
```

> Verifies Docker is installed and running

#### Pull Nginx Image

```bash
[prasanth@localhost ~]# docker pull nginx
Using default tag: latest
latest: Pulling from library/nginx
0c8d55a45c0d: Pull complete
173e7a5d3717: Pull complete
2711d25abbb0: Pull complete
359cde133485: Pull complete
acc398fdf80e: Pull complete
bc4d011570c3: Pull complete
1eb69ddd819c: Pull complete
Digest: sha256:9dd288848f4495869f76676e419ae2d767ca99fece2ec37ec0261f9fdaab5204
Status: Downloaded newer image for nginx:latest
docker.io/library/nginx:latest
```

> Downloads the official Nginx image

#### List Docker Images

```bash
[prasanth@localhost ~]# docker images
REPOSITORY   TAG      IMAGE ID       CREATED         SIZE
nginx        latest   248d2326f351   35 hours ago    161MB
```

> Shows all locally available Docker images

#### Run Hello-World Container

```bash
[prasanth@localhost ~]# docker run hello-world
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
17eec7bbc9d7: Pull complete
Digest: sha256:05813aedc15fb7b4d732e1be879d3252c1c9c25d885824f6295cab4538cb85cd
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.
```

> Confirms Docker daemon and container execution

#### Run Nginx Container

```bash
[prasanth@localhost ~]# docker run -d -p 8080:80 --name my-nginx nginx
1f16d9e4ff074beca3859e31df654d698db450f00be773bfb28a3e7955fc50d5
```

> Starts Nginx in detached mode with port mapping

#### List Running Containers

```bash
[prasanth@localhost ~]# docker ps
CONTAINER ID   IMAGE   COMMAND                  CREATED         STATUS                  PORTS                  NAMES
1f16d9e4ff07   nginx   "/docker-entrypoint.…"   2 seconds ago   Up Less than a second   0.0.0.0:8080->80/tcp   my-nginx
```

> Displays currently running containers

#### List All Containers

```bash
[prasanth@localhost ~]# docker ps -a
CONTAINER ID   IMAGE        COMMAND   CREATED         STATUS                    NAMES
1f16d9e4ff07   nginx        ...       2 seconds ago   Up                        my-nginx
cce590127ebf   hello-world  "/hello"  4 seconds ago   Exited (0) 1 second ago   quizzical_banzai
```

> Shows all running, stopped, and exited containers

---
