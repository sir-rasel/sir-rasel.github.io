---
title: "DevOps - Step By Step Learning : Part 22 (Introduction of Containerization Tool Docker)"
description: "Let's learn the fundamental DevOps concepts!"
date: "2026-03-06T00:00:00Z"
tags: ["devops" , "docker"]
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
    image: "img/blogs/145-devops-docker.jfif"
    caption: "DevOps Docker Containerization"
    alt: "DevOps Docker Containerization"
    relative: true
    hidden: true
---

---
### Other Parts of This Series:
- **Part 20:** [DevOps - Step By Step Learning : Part 20 (Hands On Networking Commands, Practically Connect The Theory)]({{< ref "blogs/144-devops-networking-practical.md" >}})
---

{{< figure
    src="/img/blogs/145-devops-docker.jfif"
    caption="DevOps Docker Containerization (Photo Credit: Unsplash)"
    align=center
>}}

## Story:

Rasel felt more comfortable and confident after learning the fundamentals. Now he thought it was time to start learning DevOps tools. But where should he start? There are numerous tools that are commonly used in DevOps practice. Then he made the decision to start with Docker. Because as a software engineer he faced numerous challenges when installing, running, and building software and its dependencies. And the well-known issue **"It works on my machine"** always arises. As far as he knew, Docker, or container technology, solved this type of problem. That is why he decided to learn containerization first.

* * *

## What is a Container?

*   A container is a lightweight, standalone, executable software package that includes everything needed to run a piece of software, Like: code, runtime, libraries, dependencies, environment variables, and config files.
*   It runs consistently across different environments (dev, test, production) regardless of the underlying infrastructure.
*   Containers share the host OS kernel, making them much more efficient than virtual machines.

## What is Meant by Containerization?

*   Containerization is the process of packaging an application and its dependencies into a container (Image: A snapshot/blueprint of your app).
*   It allows developers to build once and run anywhere.
*   It ensures consistency, scalability, and portability of applications across different systems, different machines.

## Why Do We Need Containers? What Problems Do They Solve?

***Problems Solved by Containers:***

*   **"It works on my machine" issue**: Containers ensure the environment is the same everywhere. For every infra and every developer machine.
*   **Dependency hell**: Each container has its own dependencies, avoiding conflicts.
*   **Inefficient resource usage in VMs**: Containers are lightweight and start faster.
*   **Scalability**: Containers can be easily scaled up or down.
*   **Portability**: Share and run your containerized app anywhere with Docker or Kubernetes support.

### Difference Between Bare Metal, VMs, and Containers

**1. Bare Metal**

*   Direct use of physical hardware.
*   No abstraction layer.
*   Best performance but less flexibility.
*   Manual setup and configuration.

**2. Virtual Machines (VMs)**

*   Each VM runs a full guest OS on virtualized hardware.
*   Run with the help of Hypervisor.
*   Heavyweight; includes OS, drivers, and app.
*   Takes minutes to start.
*   Better isolation but consumes more resources.

**3. Containers**

*   Share the host OS kernel; only package what’s needed to run the app.
*   Lightweight and faster to start (seconds).
*   Consumes less memory and CPU.
*   Portable and efficient for DevOps and microservices.

## Why Do We Need Containers When We Already Have VMs?

*   **Faster startup time** – containers launch in seconds.
*   **Lower overhead** – no need to boot a full OS per app.
*   **Higher density** – more containers can run on the same hardware.
*   **Better developer experience** – consistent environments, easy CI/CD integration.
*   **Microservices-friendly** – containers are ideal for splitting apps into microservices.

## Popular Containers as Examples

*   **Docker** – The most widely used container platform.
*   **Containerd** – A container runtime used by Docker and Kubernetes.
*   **CRI-O** – Lightweight runtime for Kubernetes.
*   **LXC (Linux Containers)** – Early form of Linux containerization.
*   **Podman** – Daemonless container engine compatible with Docker images.

## What is OCI (Open Container Initiative)? Why Do We Need It?

*   The **Open Container Initiative (OCI)** is a standardization body under the Linux Foundation.
*   It defines standard specs for container runtime and image formats.
*   Ensures containers work consistently across platforms (e.g., Docker, Podman, CRI-O).
*   Prevents vendor lock-in and promotes interoperability.
*   Kubernetes latest version only support the OCI standard container.

## Explain Docker as a Container

*   Docker is a container platform that makes it easy to create, deploy, and run applications in containers.
*   It uses a Docker Engine to run and manage containers.

**Features:**

*   Dockerfile to define container behavior
*   Docker CLI/GUI to manage containers
*   Docker Hub to share images
*   Docker Compose to manage multi-container apps

## A Basic Dockerfile with Explanation

```bash
# Use a base image
FROM node:18

# Set working directory inside the container
WORKDIR /app

# Copy app files to the container
COPY package*.json ./
RUN npm install

COPY . .

# Expose port
EXPOSE 3000

# Command to run the app
CMD ["node", "app.js"]        
```


### Explanation:

*   FROM node:18: Uses Node.js 18 image as the base.
*   WORKDIR /app: Sets the working directory inside the container.
*   COPY package*.json ./: Copies dependency files.
*   RUN npm install: Installs dependencies.
*   COPY . .: Copies the rest of the app files.
*   EXPOSE 3000: Declares port 3000 to be used.
*   CMD ["node", "app.js"]: Command that runs the app when the container starts.

***In this part, we just understand and familiarize with the containerization concept. We will explore and learn Docker in details in up coming parts, Insha Allah.***

* * *

## Summary:

A **container** is a lightweight package that includes your app and everything it needs to run (like code, libraries, settings). It runs the same anywhere—on your laptop, a server, or the cloud.

**Containerization** is the process of putting your app and its environment into a container. This makes your app portable, consistent, and easy to deploy or scale.

Think of a container like a **sealed lunchbox**: everything your meal (app) needs is inside, so it tastes the same no matter where you open it.