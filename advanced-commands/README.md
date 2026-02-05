#### Inspect Container

```bash
[prasanth@localhost ~]# docker inspect my-nginx
[
    {
        "Id": "1f16d9e4ff07...",
        "Created": "2026-02-05T10:22:31.123456789Z",
        "Path": "/docker-entrypoint.sh",
        "Args": ["nginx", "-g", "daemon off;"],
        "State": {
            "Status": "running",
            "Running": true
        }
    }
]
```

> Displays full low-level details of the container

---

#### View Real-Time Resource Usage

```bash
[prasanth@localhost ~]# docker stats
CONTAINER ID   NAME       CPU %     MEM USAGE / LIMIT     MEM %     NET I/O       BLOCK I/O
1f16d9e4ff07   my-nginx   0.02%     2.1MiB / 256MiB       0.82%     1.2kB / 0B    0B / 0B
```

> Monitors live CPU and memory usage

---

#### Execute Command Inside Running Container

```bash
[prasanth@localhost ~]# docker exec -it my-nginx ls /usr/share/nginx/html
index.html
```

> Runs a command inside an active container

---

#### Check Processes Running in Container

```bash
[prasanth@localhost ~]# docker top my-nginx
UID      PID     PPID    C   STIME   TTY   TIME   CMD
root     1234    1210    0   10:25   ?     00:00  nginx: master process
```

> Shows running processes inside container

---

#### View Container File Changes

```bash
[prasanth@localhost ~]# docker diff my-nginx
C /var/cache/nginx
A /var/cache/nginx/client_temp
```

> Lists filesystem changes since container start

---

#### Create Custom Docker Network

```bash
[prasanth@localhost ~]# docker network create app-network
app-network
```

> Creates isolated network for containers

---

#### List Docker Networks

```bash
[prasanth@localhost ~]# docker network ls
NETWORK ID     NAME          DRIVER    SCOPE
a1b2c3d4e5     bridge        bridge    local
f6g7h8i9j0     app-network   bridge    local
```

> Displays available Docker networks

---

#### Run Container with Resource Limits

```bash
[prasanth@localhost ~]# docker run -d \
> --name limited-nginx \
> --memory=256m \
> --cpus=0.5 nginx
4e9dcbfa7f1a...
```

> Restricts CPU and memory usage

---

#### View Docker Daemon Events

```bash
[prasanth@localhost ~]# docker events
2026-02-05T10:30:12 container start 1f16d9e4ff07
2026-02-05T10:31:01 container stop 1f16d9e4ff07
```

> Real-time Docker system activity (advanced monitoring)

---

#### Clean Unused Docker Resources

```bash
[prasanth@localhost ~]# docker system prune
WARNING! This will remove:
  - stopped containers
  - unused networks
  - dangling images
Are you sure you want to continue? [y/N] y
```

> Frees disk space safely

---

#### Aggressive Cleanup (Including Images & Volumes)

```bash
[prasanth@localhost ~]# docker system prune -a --volumes
```

