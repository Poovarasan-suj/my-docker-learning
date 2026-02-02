# Docker Intermediate Guide – Images, Architecture & Lifecycle

## 1. Creating a Custom Image from a Container (`docker commit`)

Sometimes we make changes **inside a running container** (files, configuration, installed packages). To preserve this state, Docker allows us to create a **new image from that container**.

### What `docker commit` does

* Takes a snapshot of the current container state
* Creates a **new Docker image** from it
* Useful for learning and quick backups

### Concept

```
Running Container → docker commit → Custom Image
```

### Example flow

* Run a container
* Modify content inside it
* Commit it into a new image with a tag

> ⚠️ Note: In real projects, **Dockerfile** is preferred over `docker commit`, but `commit` is excellent for learning and quick experiments.

---

## 2. Docker Image Backup (Offline Transfer)

Docker images can be backed up and transferred **without internet**.

### Saving an image

* Converts a Docker image into a `.tar` file
* Useful for air‑gapped environments

### Concept

```
Docker Image → docker save → image.tar
```

### Use cases

* Backup
* Transfer between servers
* Offline environments

---

## 3. Restoring an Image (`docker load`)

A saved image can be restored on the same or another system.

### What `docker load` does

* Loads an image from a `.tar` file
* Restores it into Docker image storage

### Concept

```
image.tar → docker load → Docker Image
```

After loading, the image behaves like any other image and can be used to run containers.

---

## 4. Image Transfer Methods

### 4.1 Without Internet (Offline)

* Use `docker save`
* Transfer `.tar` using SCP or physical copy
* Use `docker load` on target system

### 4.2 With Internet (Docker Hub)

* Requires Docker Hub account
* Image must be tagged properly

#### Image tagging format

```
username/image-name:version
```

### Flow

```
Local Image → tag → login → push → pull
```

This allows sharing images globally.

---

## 5. Docker Architecture (How Docker Works Internally)

Docker follows a **client–server architecture**.

### Components

#### 1. Docker Client

* Where commands are executed (`docker run`, `docker ps`)
* Sends requests to Docker daemon

#### 2. Docker Daemon (dockerd)

* Runs on the Docker host (OS)
* Responsible for:

  * Managing images
  * Managing containers
  * Networking
  * Storage

#### 3. Docker Registry

* Stores Docker images
* Example: Docker Hub
* Accessed only when needed

### Architecture Flow

```
Docker CLI → Docker Daemon → (Optional) Docker Registry
```

### Important note

* Commands like `docker ps`, `docker start` → ❌ No internet
* Commands like `docker pull`, `docker push` → ✅ Internet required

---

## 6. Docker Container Lifecycle

A container goes through multiple states during its lifetime.

### Lifecycle Stages

1. **Create** – Container is created
2. **Running** – Container is executing
3. **Paused** – Container is frozen
4. **Stopped** – Container execution stopped
5. **Deleted** – Container removed

---

## 7. Pause vs Stop (Very Important Difference)

### Pause

* Container process is frozen
* Memory remains allocated
* CPU execution paused
* Resume is very fast

Use when:

* Temporary halt
* Quick resume needed

---

### Stop

* Container process is terminated
* Memory is released
* Container state saved
* Restart takes slightly longer

Use when:

* Container not needed for some time
* Resource cleanup required

---

## 8. Image vs Container (Revision)

| Image         | Container          |
| ------------- | ------------------ |
| Blueprint     | Running instance   |
| Read-only     | Writable           |
| Can be shared | Temporary          |
| Created once  | Created many times |

---

## 9. Key Takeaways (Quick Revision)

* `docker commit` → create image from container
* `docker save` → offline image backup
* `docker load` → restore image
* Docker Hub → online image sharing
* Docker uses client–server architecture
* Containers have a defined lifecycle
* Pause ≠ Stop

---
