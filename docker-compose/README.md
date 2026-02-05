#### What is Docker Compose?

**Docker Compose** is a tool used to **define and run multi-container Docker applications** using a single YAML file (`docker-compose.yml`).
With one command, you can start, stop, and manage all services together.

---

#### Why Docker Compose?

* Run **multiple containers** (web, DB, cache) easily
* One configuration file
* Simplifies **local development & testing**
* Reproducible environments
* Easier than running many `docker run` commands

---

#### Key Components of Docker Compose

* **Services** – Containers (app, database, cache, etc.)
* **Networks** – Communication between services
* **Volumes** – Persistent data storage
* **Configs & Secrets** – Externalized configuration

---

#### Common Docker Compose Commands

```bash
docker compose up
docker compose up -d
docker compose down
docker compose ps
docker compose logs
docker compose build
docker compose restart
docker compose exec web sh
```

---

#### Example: Python App + MySQL (Real-World)

```yaml
version: "3.9"

services:
  app:
    build: .
    container_name: python_app
    ports:
      - "8000:8000"
    depends_on:
      - db
    environment:
      - DB_HOST=db
      - DB_USER=root
      - DB_PASSWORD=root

  db:
    image: mysql:8.0
    container_name: mysql_db
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: root
      MYSQL_DATABASE: appdb
    volumes:
      - db_data:/var/lib/mysql

volumes:
  db_data:
```

---

#### Networking in Docker Compose

* All services are on the **same default network**
* Services communicate using **service names**

  ```text
  app → db (hostname)
  ```

---

#### Volumes in Docker Compose

```yaml
volumes:
  db_data:
```

* Persists data even if containers are deleted
* Common for databases

---

#### Environment Variables

#### Inline

```yaml
environment:
  - DEBUG=true
```

#### From `.env` file

```yaml
env_file:
  - .env
```

