# **Mastering Docker Container Layers for Beginners**

---

## **1️⃣ Basic Concept**

**Docker Image**:

* Think of it as a **recipe or template**.
* Immutable (cannot be changed once created).
* Contains all files, libraries, and dependencies your app needs.

**Docker Container**:

* Think of it as a **running instance** of that image (like an object from a class).
* Mutable layer on top of image layers where changes happen.

**Why It Matters**:

* Efficient storage (shared base layers).
* Fast deployments.
* Isolation from host system.

**Analogy**:

* **Image** = “Blueprint of a house”
* **Container** = “The house built from that blueprint”
* **Changes in container** = repainting walls, adding furniture (only affect this house)

---

## **2️⃣ Docker Layer Breakdown**

Docker images are built **layer by layer**. Each command in a Dockerfile creates a **new layer**.

### **Layer Types:**

| Layer Type          | Description                                      | Mutability |
| ------------------- | ------------------------------------------------ | ---------- |
| Base Layer          | Starts from an official image (e.g., `centos:7`) | Read-only  |
| Intermediate Layers | Added by Dockerfile commands like `RUN`, `COPY`  | Read-only  |
| Container Layer     | Where your running container stores changes      | Read/Write |

### **Visual Diagram**

```
[Container Layer]   <- Read/Write (changes live here)
-------------------
[Intermediate Layer 2] <- Read-only
-------------------
[Intermediate Layer 1] <- Read-only
-------------------
[Base Layer: centos:7] <- Read-only
```

✅ **Key Point:** You **cannot change base or intermediate layers**, only the **container layer** is mutable.

---

## **3️⃣ Read-Only vs Read/Write**

| Layer                      | Behavior                                                |
| -------------------------- | ------------------------------------------------------- |
| Base / Intermediate Layers | **Read-only** – shared across containers, cannot modify |
| Container Layer            | **Read/Write** – only affects this container            |

**Example**:

* Run a container from an image, install `vim`.
* `vim` exists only inside this container’s **read/write layer**, not in the base image.

---

## **4️⃣ Commands & Examples**

### **Step 1: Start from a Base Image**

```dockerfile
FROM centos:7
```

* Creates **Base Layer (read-only)** from CentOS 7.

### **Step 2: Add Intermediate Layers**

```dockerfile
RUN yum install -y wget
RUN yum install -y git
```

* Each `RUN` creates a **new read-only layer**.

### **Step 3: Inspect Layers**

```bash
docker build -t myimage:latest .
docker history myimage:latest
```

* Shows all layers, commands, and size.

### **Step 4: Run a Container**

```bash
docker run -it myimage:latest bash
```

* Anything you change here (create files, install packages) goes into **container layer**.

### **Step 5: Check Container Changes**

```bash
touch /tmp/hello.txt
ls /tmp
```

* `/tmp/hello.txt` exists only in this **container**, not in the base image.

---

## **5️⃣ Hands-On Exercise: Build & Inspect Layers**

1. **Create Dockerfile**

```dockerfile
# Step 1: Base Layer
FROM centos:7

# Step 2: Intermediate Layers
RUN yum install -y wget
RUN yum install -y git

# Step 3: Add a file
COPY hello.sh /hello.sh
RUN chmod +x /hello.sh
```

2. **Build Image**

```bash
docker build -t layered-example .
```

3. **Inspect Image Layers**

```bash
docker history layered-example
```

4. **Run Container**

```bash
docker run -it layered-example bash
```

5. **Add Files in Container**

```bash
echo "Hello Docker" > /tmp/inside-container.txt
ls /tmp
```

✅ Changes exist **only in container layer**.

---

## **6️⃣ Real-World Analogies**

* **Shared base layers**:

  * Dev, Test, and Prod containers can use same `python:3.11` image.
  * Saves storage and network bandwidth.

* **Intermediate layers**:

  * Like building a cake step-by-step: base = sponge, intermediate = frosting layers.
  * Each step is frozen in time (cannot change past layers).

* **Container layer**:

  * Like putting toppings on your own slice of cake — only your slice changes.

---

## **7️⃣ Tips for Beginners**

1. **Minimize Layers**: Use fewer `RUN` commands to reduce image size.
2. **Use `.dockerignore`**: Avoid copying unnecessary files.
3. **Rebuild smartly**: Only changed layers are rebuilt.
4. **Understand Read/Write**: Never expect changes in container to affect the base image.
5. **Linux Commands Needed**: `ls`, `touch`, `echo`, `chmod`, `yum`, `cat`

---

## **8️⃣ Summary Diagram: Layers & Flow**

```
Dockerfile Commands
-------------------
FROM centos:7   --> Base Layer (Read-only)
RUN yum install wget  --> Intermediate Layer (Read-only)
RUN yum install git   --> Intermediate Layer (Read-only)
COPY hello.sh         --> Intermediate Layer (Read-only)

Container Starts
----------------
Container Layer (Read/Write)
- Add files
- Install temp packages
- Changes exist only here
