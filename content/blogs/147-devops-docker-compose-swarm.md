---
title: "DevOps - Step By Step Learning : Part 24 (Docker Compose & Docker Swarm Hands On)"
description: "Let's learn the fundamental DevOps concepts!"
date: "2026-03-08T00:00:00Z"
tags: ["devops" , "docker", "docker-compose", "docker-swarm"]
draft: false
showtoc: false
tocOpen: false
hidemeta: false
comments: true
disableHLJS: false
disableShare: false
hideSummary: false
searchHidden: false
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
ShowCodeCopyButtons: true
cover:
    image: "img/blogs/147-devops-docker-compose.jfif"
    caption: "DevOps Docker Compose & Docker Swarm"
    alt: "DevOps Docker Compose & Docker Swarm"
    relative: true
    hidden: true
---

---
### Other Parts of This Series:
- **Part 23:** [DevOps - Step By Step Learning : Part 23 (Docker Hands On)]({{< ref "blogs/146-devops-docker-hands-on.md" >}})
---

{{< figure
    src="/img/blogs/147-devops-docker-compose.jfif"
    caption="DevOps Docker Compose & Docker Swarm (Photo Credit: Unsplash)"
    align=center
>}}

## Story:

Pure Docker is useful for running a simple standalone application or service. But real-world projects are not always as straightforward and simple as they appear. During development, we constantly require multiple dependencies or services to function, such as a database, cache, message broker, and so on. Rasel realized we needed something to solve this problem. Rasel was looking for a solution that was capable of handling multiple container bootstrapping. And guess what? Rasel discovered that Docker Compose is the solution. That's why, Rasel decided to learn Docker Compose and Docker Swarm in detail.

* * *

## Docker Compose

Docker Compose is a tool for defining and running **multi-container** Docker applications. Instead of writing many docker run commands, you define everything in a single **"docker-compose.yml"** (latest version support **compose.yml**) file - services, networks, volumes, environment variables, build instructions, etc. You then launch the entire stack with: **"docker compose up"**.

### Benefits of Docker Compose

*   **Simplified Management**: Docker Compose uses a docker-compose.yml file (or docker-compose.yaml) to define all thing and then use simplified commands and gives efficient development flow.
*   **Consistent Environment**: Like docker it also gives consistency for multiple container and persist same behaviors across different environment. Thus reduced error also.
*   **Enhanced Collaboration**: The docker-compose.yml file is easy to share with other developers, facilitating collaboration and knowledge sharing.
*   **Portability**: Like docker enhances portability and reduce platform dependency. Also gives more customizable power.
*   **Scalability**: Docker compose gives us the ability to scale our multiple container services add and run. Also possible to work with single container from multiple one of docker compose.
*   **Persistency**: Docker compose make volume mounting or binding easy.
*   **Networking**: Docker compose make manage docker networking easy as well.
*   Env and Config: Has options for Env and Config management.

* * *

### Anatomy of a docker-compose.yml File

```bash
version: "3.9"

x-defaults: &default-settings
  restart: unless-stopped
  networks:
    - backend

services:
  web:
    build:
      context: .
      dockerfile: Dockerfile
    image: myapp:latest
    container_name: my_web_app
    ports:
      - "8080:80"
    volumes:
      - ./src:/app/src     # Live code mount
      - logs:/app/logs     # Named volume
    environment:
      - NODE_ENV=production
      - DB_HOST=db
      - DB_USER=admin
    env_file:
      - .env
    depends_on:
      db:
        condition: service_healthy
    entrypoint: ["sh", "-c"]
    command: ["npm run start"]
    profiles:
      - default
      - prod
    post_start:
      - command: chown -R /data 1001:1001
    pre_stop:
      - command: ./data_flush.sh
    develop:
      watch:
        - path: ./src
          action: rebuild
    healthcheck:
      test: ["CMD-SHELL", "curl -f http://localhost || exit 1"]
      interval: 10s
      timeout: 5s
      retries: 5
    <<: *default-settings

  db:
    image: postgres:15
    container_name: postgres_db
    environment:
      - POSTGRES_USER=admin
      - POSTGRES_PASSWORD=secret
    volumes:
      - pgdata:/var/lib/postgresql/data
    healthcheck:
      test: ["CMD", "pg_isready", "-U", "admin"]
      interval: 10s
      timeout: 5s
      retries: 5
    secrets:
      - db_password
    <<: *default-settings

  redis:
    image: redis:7-alpine
    container_name: redis_cache
    command: ["redis-server", "--appendonly", "yes"]
    volumes:
      - redisdata:/data
    profiles:
      - dev
    <<: *default-settings

  devtools:
    image: node:18
    container_name: dev_cli
    working_dir: /app
    volumes:
      - ./src:/app/src
    command: ["npm", "run", "lint"]
    profiles:
      - dev
    <<: *default-settings

volumes:
  pgdata:
  redisdata:
  logs:

networks:
  backend:
    driver: bridge

secrets:
  db_password:
    file: ./secrets/db_password.txt        
```

---

***1) version***

Specifies the Compose file format version.

```bash
version: "3.9"  # Recommended for compatibility with Docker 20.10+        
```

*   version: "3" is stable and widely supported.
*   3.x versions support Swarm mode (useful if you later move to orchestration).

---

***2) services***

Defines your application containers.

```bash
services:
  web:
    image: nginx
  db:
    image: postgres        
```

*   Each top-level key under services is a separate container.

*Inside the service section following options are available:*

***2.1) build***

Build image from a Dockerfile in the current or custom directory.

```bash
build:
  context: .
  dockerfile: Dockerfile.dev        
```

***2.2) image***

Use an image (from Docker Hub or local).

```bash
image: redis:6-alpine
```

***2.3) container_name***

Give a custom name to the container.

```bash
container_name: my_custom_app        
```

***2.4) ports***

Map host ports to container ports.

```bash
ports:
  - "8080:80"   # host:container        
```

***2.5) volumes***

Mount host directories or Docker volumes.

```bash
volumes:
  - ./data:/var/lib/mysql
  - myvolume:/app/logs        
```

***2.6) environment***

Pass environment variables. Or use a .env file:

```bash
environment:
  - DB_USER=root
  - DB_PASS=secret

# or
env_file: .env        
```

***2.7) depends on***

Set startup order (note: doesn’t wait for service to be ready).

```bash
depends_on:
  - db
```

***2.8) networks***

Connect services to specific Docker networks.

```bash
networks:
  - backend
```

***2.9) entrypoint & commands***

Override the image or Dockerfile's default behavior.

```bash
services:
  app:
    image: myapp
    entrypoint: ["sh", "-c"]
    command: ["npm run start:prod"]        
```

*   Useful for container customization or debugging.

***2.10) restart***

Define restart policy.

```bash
restart: unless-stopped
```

---

***3) volumes***

Define named volumes that persist between runs.

These can be used in services like:

```bash
services:
  db:
    volumes:
      - mydata:/var/lib/mysql        
```

---

***4) networks***

Define user-defined networks for better isolation and control.

```bash
networks:
  backend:
    driver: bridge        
```

Attach to service like:

```bash
services:
  app:
    networks:
      - backend        
```

---

***5) secrets & configs***

Used in Swarm mode for storing sensitive data like API keys, TLS certs, etc.

```bash
secrets:
  my_secret:
    file: ./secret.txt        
```

Use inside service:

```bash
secrets:
  - my_secret
```

---

***6) healthcheck***

Monitor container health.

```bash
healthcheck:
  test: ["CMD", "curl", "-f", "http://localhost:80"]
  interval: 30s
  timeout: 10s
  retries: 3        
```

---

### Advanced Docker Compose Features:

***7) Lifecycle Hook***

Define the operation that can be run after container start and before container stop.

```bash
services:
  app:
    image: backend
    pre_stop:
      - command: ./data_flush.sh
    post_start:
      - command: chown -R /data 1001:1001        
```

---

***8) Service Profile***

Group services into profiles so you can run only certain parts of a stack.

```bash
services:
  app:
    image: myapp
    profiles: ["prod", "default"]

  devtools:
    image: some-debugger
    profiles: ["dev"]        
```

*   docker compose --profile dev up
*   Great for running debug tools, test helpers, or skipping prod-only services.

---

***9) Compose Watch***

Monitors source code and rebuilds/restarts containers on change - no more manual rebuilds!

```bash
services:
  web:
    build: .
    develop:
      watch:
        - path: ./src
          action: rebuild        
```

*   This is a next-gen replacement for hot reloading setups like Nodemon, air.
*   docker compose watch or docker compose up --watch

---

***10) Multi Compose File Setup***

Split your Compose configuration into base + environment-specific overrides:

*   docker-compose.yml # Base config
*   docker-compose.dev.yml # Dev-specific config
*   docker-compose.prod.yml # Prod-specific config

And can be 3 type: (For more info please read the official doc: https://docs.docker.com/compose/how-tos/multiple-compose-files/)

1.  Merge
2.  Extend
3.  Include

---

***11) Extends Common Property***

Reuse common config across services (in Compose v2 format):

```bash
x-common-settings: &defaults
  restart: always
  networks:
    - backend

services:
  app:
    <<: *defaults
    image: myapp        
```

* * *

### Useful Docker Compose Commands

```bash
docker-compose up -d           # Start in background
docker-compose watch           # Reload and rebuild on change
docker-compose down            # Stop & remove all
docker-compose build           # Build images
docker-compose ps              # Show running containers
docker-compose logs -f         # Tail logs
docker-compose exec app bash   # Run a command in container
docker-compose restart app     # Restart specific service        
```

For more details see the official docs: https://docs.docker.com/compose/

* * *

## Docker Swarm

Docker **Swarm** is Docker’s native container orchestration system, allowing you to deploy and manage a cluster of Docker Engines as a single virtual system.

Container **orchestration** is the process of automating the deployment, scaling, networking, and management of containers.

And a **cluster** is a group of computers (physical or virtual machines) connected together to function as a single system.

### Benefits of Swarm

*   **High Availability**: Containers can be replicated across nodes.
*   **Scalability**: Easily scale services up/down.
*   **Rolling Updates**: Deploy updates with zero downtime.
*   **Load Balancing**: Distributes traffic automatically.
*   **Self-healing**: Failed containers are automatically restarted or rescheduled.

---

### Basic Terminology

*   **Node** - A machine (VM or physical) in the Swarm
*   **Manager Node** - Controls the cluster; makes scheduling decisions
*   **Worker Node** - Executes containers based on instructions from manager
*   **Service** - A task or set of tasks (containers) defined by image, scale, network, etc.
*   **Task** - A single container instance
*   **Stack** - A group of services defined using docker-compose.yml (Swarm-aware)

* * *

### Swarm with Native Docker

```bash
# Step 1: Initialize Swarm
docker swarm init   # This makes the current machine a manager node.

# Step 2: Add Worker Nodes
# On each worker machine:
docker swarm join --token <token> <manager-ip>:2377

#You can get the join command using:
docker swarm join-token worker

# Step 3: Deploy a Service
# This runs 3 replicas of Nginx distributed across the cluster.
docker service create --name web --replicas 3 -p 80:80 nginx  

#Step 4: List Services and Nodes
docker service ls 
docker service ps web               # View tasks/containers 
docker node ls                      # View cluster nodes

# Step 5: Scale a Service
docker service scale web=5        
```

* * *

### Swarm with Docker Compose (Stacks)

```bash
version: "3.9"

services:
  web:
    image: nginx:alpine
    ports:
      - "80:80"
    deploy:
      replicas: 2
      placement:
        constraints: [node.role == worker]
      restart_policy:
        condition: on-failure
      update_config:
        parallelism: 1
        delay: 5s
    depends_on:
      - backend

  backend:
    image: myorg/myapp:latest
    environment:
      - DB_HOST=db
      - DB_USER=admin
      - DB_PASS_FILE=/run/secrets/db_password
    secrets:
      - db_password
    deploy:
      replicas: 3
      restart_policy:
        condition: on-failure
    depends_on:
      - db

  db:
    image: postgres:15
    environment:
      - POSTGRES_USER=admin
      - POSTGRES_PASSWORD_FILE=/run/secrets/db_password
    volumes:
      - dbdata:/var/lib/postgresql/data
    secrets:
      - db_password
    deploy:
      placement:
        constraints: [node.role == manager]

volumes:
  dbdata:

secrets:
  db_password:
    external: true        
```

### Summary of Swarm-specific Features Used

*   **deploy**: Swarm-only block for scaling, restart policy, constraint
*   **replicas**: Number of container instances per service
*   **placement**: Control where services run (manager or worker nodes)
*   **secrets**: Secure storage of sensitive data
*   **update_config**: Rolling update config for zero downtime

Now to deploy the services or application using docker swarm follow the following steps:

```bash
# Before deploying, create the secret (stored securely on Swarm managers)
echo "my_secret_db_password" | docker secret create db_password -

# You can verify it
docker secret ls

# Deploy the stack
# mystack is the name of the stack.
# All services will be prefixed with mystack_.
# Make sure you run docker swarm init before deploying.
docker stack deploy -c docker-compose.yml mystack     

# Monitor the deployment
docker stack ls                       # List stacks
docker stack services mystack         # List services in the stack
docker stack ps mystack               # Show running tasks
docker service logs mystack_backend   # Tail logs of a service

# To remove the stack
docker stack rm mystack        
```

* * *

### Swarm Best Practices

*   Always use at least 3 manager nodes (for quorum).
*   Use overlays for cross-node networking.
*   Use stacks for real-world projects.
*   Store secrets using Docker secrets.
*   Monitor via docker service ps, docker node ls, docker events.

For more details see the official docs: https://docs.docker.com/engine/swarm/

* * *

## Summary:

**Docker Compose** is a tool that lets you define and run multi-container applications using a single file called docker-compose.yml. Instead of running individual containers with many docker run commands, Compose allows you to describe your whole app - including services, networks, volumes, and environment settings - in one place. You can start everything with just docker compose up, making it perfect for development and small setups.

**Docker Swarm** is Docker’s built-in system for orchestrating containers across multiple machines. It lets you manage a cluster of Docker engines (called nodes), deploy services that run on them, scale containers up or down, perform rolling updates, and balance traffic automatically. You define your services in a Compose file using special deploy settings and then use docker stack deploy to launch them across the Swarm cluster. Swarm adds high availability, self-healing, and scalability to your containerized applications - all using familiar Docker tools.