Your notes are correct, but they are scattered. Here's a clean **interview + practical version** that is easy to remember.

---

# Docker Compose

## What is Docker Compose?

Docker Compose is used to manage **multiple Docker containers** using a single YAML file.

Instead of starting each container one by one, we define all containers in **docker-compose.yml** and manage them with a single command.

### Interview Answer

> Docker Compose is a tool used to define and run multi-container Docker applications. If my project has multiple containers like Nginx, Application, Database, Redis, Jenkins, etc., I don't start each container manually. I define everything inside a `docker-compose.yml` file and use commands like `docker compose up` and `docker compose down` to start or stop the complete application.

---

# Why Docker Compose?

Suppose your application has

* Application Container
* MySQL Container
* Redis Container
* Nginx Container
* Prometheus Container

Without Compose

```
docker run ...
docker run ...
docker run ...
docker run ...
docker run ...
```

With Compose

```
docker compose up -d
```

Everything starts automatically.

To stop

```
docker compose down
```

---

# Example

Create Dockerfiles

```
nano Dockerfile.dev
cp Dockerfile.dev Dockerfile.prod
cp Dockerfile.dev Dockerfile.staging
```

docker-compose.yml

```yaml
version: "3.8"

services:

  dev:
    build:
      context: .
      dockerfile: Dockerfile.dev
    container_name: dev_container

  prod:
    build:
      context: .
      dockerfile: Dockerfile.prod
    container_name: prod_container

  staging:
    build:
      context: .
      dockerfile: Dockerfile.staging
    container_name: staging_container
```

Run

```
docker compose up
```

Stop

```
docker compose down
```

---

# Important Docker Compose Commands

Start containers

```
docker compose up
```

Run in background

```
docker compose up -d
```

Stop containers

```
docker compose stop
```

Start stopped containers

```
docker compose start
```

Restart

```
docker compose restart
```

Stop and remove everything

```
docker compose down
```

Build images

```
docker compose build
```

View running containers

```
docker compose ps
```

View logs

```
docker compose logs
```

Follow logs

```
docker compose logs -f
```

---

# Installing Docker Compose Plugin

```
mkdir -p ~/.docker/cli-plugins

curl -SL https://github.com/docker/compose/releases/latest/download/docker-compose-linux-x86_64 \
-o ~/.docker/cli-plugins/docker-compose

chmod +x ~/.docker/cli-plugins/docker-compose

docker compose version
```

---

# Important Keywords in docker-compose.yml

## services

Defines all containers.

Example

```yaml
services:

  app:

  db:

  redis:
```

---

## build

Build image from Dockerfile.

```yaml
build:
  context: .
  dockerfile: Dockerfile.dev
```

---

## image

Pull image from Docker Hub.

```yaml
image: postgres:15-alpine
```

---

## container_name

Assign custom container name.

```yaml
container_name: app_container
```

---

## ports

Map host port to container port.

```
HOST:CONTAINER
```

Example

```yaml
ports:
  - "8080:80"
```

Meaning

```
Browser → localhost:8080

Inside container → Port 80
```

---

## volumes

Used for persistent storage or code sharing.

Example

```yaml
volumes:
  - ./app:/usr/src/app
```

or

```yaml
volumes:
  - db-data:/var/lib/postgresql/data
```

---

## environment

Pass environment variables.

```yaml
environment:
  POSTGRES_USER: admin
  POSTGRES_PASSWORD: admin123
```

---

## depends_on

Starts one service after another.

Example

```yaml
depends_on:
  db:
```

With health check

```yaml
depends_on:
  db:
    condition: service_healthy
```

Meaning

App starts only after Database becomes healthy.

---

## healthcheck

Checks whether container is healthy.

Example

```yaml
healthcheck:
  test: ["CMD","curl","-f","http://localhost"]
  interval: 15s
  timeout: 5s
  retries: 3
```

---

## networks

Allows containers to communicate.

Example

```yaml
networks:
  - front-tier
  - back-tier
```

---

## restart

Restart policy.

```yaml
restart: always
```

or

```yaml
restart: no
```

---

# What is Seed Service?

### Interview Answer

Seeding means inserting initial or default data into a database automatically.

Suppose your application needs:

* Default Admin User
* Sample Products
* Categories
* Default Roles

Instead of manually inserting data every time, we create a **seed container**.

Example

```yaml
seed:
  build: ./seed-data
  profiles: ["seed"]

  depends_on:
    vote:
      condition: service_healthy

  restart: "no"
```

Run seed only when required

```
docker compose --profile seed up
```

The seed container:

* Starts once
* Inserts initial data into the database
* Stops automatically

---

# Example Voting Application

Clone project

```bash
git clone https://github.com/dockersamples/example-voting-app.git

cd example-voting-app

docker compose up -d
```

This project starts multiple services:

* vote (Frontend)
* result (Results UI)
* worker (Processes votes)
* redis (Message queue)
* postgres (Database)
* seed (Optional database seeding)

All services are connected using Docker Compose networks and managed with a single command.

---

# Practical Interview Explanation

> "In my projects, I use Docker Compose whenever multiple containers are involved. For example, an application may require an application container, PostgreSQL database, Redis cache, and Nginx. Instead of running each container individually using multiple `docker run` commands, I define all services in a `docker-compose.yml` file. Then I start the complete environment using `docker compose up -d` and stop it using `docker compose down`. Docker Compose also allows me to define networks, volumes, environment variables, health checks, service dependencies, and optional seed containers to initialize the database."

This explanation is concise, practical, and suitable for DevOps interviews.
