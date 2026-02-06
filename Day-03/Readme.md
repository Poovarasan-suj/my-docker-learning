# Docker Volumes & Dockerfile – Practical Documentation

---

## 1. Docker Volumes – Why They Are Needed

By default, **containers are stateless**.
When a container is stopped or removed, any data created inside it is **lost**.

Docker volumes are used to:

* Persist data beyond container lifecycle
* Share data between container and host
* Share data between multiple containers

---

## 2. Types of Docker Volumes

Docker supports **three main types** of storage mounts.

---

## 2.1 Docker-Managed Volumes

Docker manages these volumes internally.

**Where stored:**

```
/var/lib/docker/volumes/
```

**Characteristics:**

* Managed completely by Docker
* Independent of host directory structure
* Portable and safe
* Best choice for production

**Why use it:**

* Data persists even if container is deleted
* Cleaner than bind mounts
* Docker handles permissions and paths

**Example use case:**

* Web application data
* Database storage
* Application logs

**Example scenario (practical):**

* Created a Docker volume
* Mounted it to Apache web root
* Modified files
* Restarted and removed container
* Data remained intact

---

## 2.2 Bind Mounts

Bind mounts map a **specific host directory** directly into a container.

**Characteristics:**

* Uses an existing host path
* Fully controlled from host
* Depends on host filesystem
* Less portable

**Why use it:**

* Useful during development
* Immediate file changes
* Easy debugging

**Example use case:**

* Local development
* Testing
* Configuration files

**Example scenario (practical):**

* Host directory `/root/www` mounted to Apache htdocs
* File edited on host
* Browser reflected changes instantly
* Container removed and recreated
* Data still available on host

---

## 2.3 tmpfs Mounts

Temporary storage stored **in memory (RAM)**.

**Characteristics:**

* Data stored in RAM
* Data lost when container stops
* Very fast
* No disk usage

**Why use it:**

* Sensitive data
* Temporary cache
* Session data

**Example use case:**

* Passwords
* Tokens
* Temporary runtime files

---

## 3. Volume Type Comparison

| Feature           | Docker Volume | Bind Mount | tmpfs           |
| ----------------- | ------------- | ---------- | --------------- |
| Managed by Docker | Yes           | No         | Yes             |
| Persistent        | Yes           | Yes        | No              |
| Host dependency   | Low           | High       | None            |
| Performance       | Optimized     | Depends    | Very fast       |
| Production usage  | ✅ Recommended | ⚠ Limited  | ⚠ Special cases |

**Best practice:**

* **Production:** Docker volumes
* **Development:** Bind mounts
* **Sensitive/temporary data:** tmpfs

---

## 4. Dockerfile – What and Why

A **Dockerfile** is a text file that contains instructions to build a Docker image.

**Why Dockerfile is important:**

* Repeatable image builds
* Version controlled
* Preferred over manual container changes
* Industry standard

---

## 5. Dockerfile – Practical Example

### Directory Structure

```
dockerfile-test/
├── Dockerfile
└── index.html
```

---

### Dockerfile Content

```dockerfile
FROM httpd
COPY index.html /usr/local/apache2/htdocs/
```

---

### Explanation

* `FROM httpd`
  Uses Apache HTTP Server as the base image

* `COPY index.html /usr/local/apache2/htdocs/`
  Copies custom web content into Apache web root

---

## 6. Dockerfile vs Container Modification

| Method        | Purpose            | Recommendation  |
| ------------- | ------------------ | --------------- |
| Dockerfile    | Image creation     | ✅ Preferred     |
| docker commit | Snapshot container | ⚠ Learning only |

**Reason:**

* Dockerfile is clean, repeatable, and version-controlled
* `docker commit` is manual and not scalable

---

## 7. Key Understanding

* Containers are temporary by nature
* Volumes provide persistence
* Docker-managed volumes are best for production
* Bind mounts are best for development
* Dockerfile is the correct way to build images

