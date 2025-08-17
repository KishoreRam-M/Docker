# Docker Commands Study Guide – Real-Time Reference

## 1. Check Docker Version

**Command:**

```bash
sudo docker --version
```

**What:** Displays the installed Docker version.
**Where:** Host machine (terminal).
**How it works:** Queries Docker CLI to show client version.
**Example:**

```bash
Docker version 24.0.1, build a12345
```

---

## 2. List Docker Volumes

**Command:**

```bash
sudo docker volume ls
```

**What:** Shows all Docker volumes.
**Where:** Host machine.
**How it works:** Lists persistent storage used by containers.
**Use Case:** Check volumes storing database data.
**Example:**

```bash
DRIVER    VOLUME NAME
local     my_db_volume
```

---

## 3. Help on Docker Commands

**Command:**

```bash
sudo docker <command> --help
```

**What:** Shows usage and options for any Docker command.
**Where:** Host machine.
**How:** Opens CLI documentation for quick reference.
**Example:**

```bash
sudo docker run --help
```

---

## 4. Docker Disk Usage

**Command:**

```bash
sudo docker system df
```

**What:** Shows disk space used by images, containers, and volumes.
**Where:** Host.
**Use Case:** Monitor storage before cleanup.

---

## 5. Docker Real-Time Events

**Command:**

```bash
sudo docker system events
```

**What:** Streams real-time Docker events (container start, stop, image pull).
**Where:** Host terminal.
**Use Case:** Debug container lifecycle in real-time.

---

## 6. System Prune (Cleanup)

**Command:**

```bash
sudo docker system prune
```

**What:** Deletes unused containers, networks, images, and caches.
**Where:** Host.
**Use Case:** Free disk space.

---

## 7. Image / Container Cleanup

**Command:**

```bash
sudo docker image prune
sudo docker container prune
```

**What:** Removes unused images or stopped containers.
**Where:** Host.
**Use Case:** Maintain disk hygiene.

---

## 8. Container Resource Stats

**Command:**

```bash
sudo docker stats
```

**What:** Shows real-time CPU, memory, and network usage of containers.
**Where:** Host terminal.
**Use Case:** Performance monitoring.

---

## 9. Create Container

**Command:**

```bash
sudo docker create <image_name>
```

**What:** Creates a container without starting it.
**Where:** Host.
**Use Case:** Prepare container for later execution.

---

## 10. Run Container

**Command:**

```bash
sudo docker run <image_name>
```

**What:** Creates and starts a container.
**Where:** Host.
**Use Case:** Launch web server, database, or any app.
**Example:**

```bash
sudo docker run -d --name web1 httpd
```

---

## 11. List Running Containers

**Command:**

```bash
sudo docker ps
```

**What:** Lists currently running containers.
**Where:** Host.
**Use Case:** Check active services.

---

## 12. List All Containers

**Command:**

```bash
sudo docker ps -a
```

**What:** Shows all containers (running + stopped).
**Where:** Host.

---

## 13. Run Container in Background with Name

**Command:**

```bash
sudo docker run -d --name web1 httpd
```

**What:** Starts container in detached mode and assigns a name.
**Use Case:** Host multiple containers with easy reference.

---

## 14. Access Container Shell

**Command:**

```bash
docker exec -it <container_name> /bin/sh
```

**What:** Opens an interactive shell inside a running container.
**Use Case:** Debug or modify container files.

---

## 15. Copy Files To/From Container

**Command:**

```bash
docker cp <source> <container_name>:<destination>
```

**What:** Copies files between host and container.

---

## 16. Stop Container

**Command:**

```bash
docker stop <container_name>
```

**What:** Stops a running container.

---

## 17. Remove Container

**Command:**

```bash
sudo docker rm <container_name>
```

**What:** Deletes a stopped container.

---

## 18. View Container Logs

**Command:**

```bash
sudo docker logs <container_name>
```

**What:** Displays logs from a container.
**Use Case:** Debug application inside container.

---

## 19. Start Container

**Command:**

```bash
sudo docker start -ai <container_name>
```

**What:** Starts a container (attach mode optionally).

---

## 20. Inspect Running Processes

**Command:**

```bash
sudo docker top <container_name>
```

**What:** Lists processes running inside a container.
