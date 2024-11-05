Containerization is a method of packaging and deploying applications in a lightweight, portable way, enabling them to run consistently across different environments. It encapsulates an application and its dependencies into a single unit called a *container*, which can be run on any compatible system, regardless of variations in software configurations.

Here's a breakdown of key concepts:

1. **Containers vs. Virtual Machines (VMs)**: Containers are often compared to VMs because both provide isolated environments. However, while VMs emulate entire operating systems, containers share the host OS kernel, making them more lightweight and efficient. This enables faster startup times and lower resource consumption.

2. **Containerization Benefits**:
   - **Portability**: Containers run the same way on any platform with container runtime, making them highly portable across development, testing, and production environments.
   - **Isolation**: Each container operates independently, minimizing conflicts and ensuring that dependencies don’t interfere with other applications.
   - **Efficiency**: Sharing the host OS kernel reduces overhead, so multiple containers can run simultaneously with less resource usage than traditional VMs.
   - **Scalability**: Containers support rapid scaling, as they can be easily replicated or deployed across clusters for load balancing.

3. **Docker and Kubernetes**: Docker is the most popular tool for creating and managing containers. Kubernetes, on the other hand, is an orchestration platform that helps manage large numbers of containers across clusters, enabling automated deployment, scaling, and management.

4. **Use Cases**:
   - **Microservices**: Containers are ideal for microservices architectures, where each service can be deployed independently in its own container.
   - **Continuous Integration/Continuous Deployment (CI/CD)**: Containers simplify the CI/CD pipeline by ensuring consistency across various environments.

In a typical containerized setup, you’d write a Dockerfile to define the container’s contents, build it into an image, and then deploy it on a platform (such as Kubernetes or Docker Swarm) to scale and manage your application.# Docker

# Docker--Guide

Docker is a platform for developing, shipping, and running applications in containers. Here are some commonly used Docker commands:

The `docker version` and `docker info` commands provide detailed information about your Docker installation and environment.

### `docker version`
The `docker version` command shows version details for each component of Docker, including the Docker Engine and CLI. This is useful for verifying the installed version and compatibility information.

```bash
docker version
```

#### Output includes:
- **Client**:
  - `Version`: Docker client version.
  - `API version`: API version compatibility between client and server.
  - `Go version`: Version of Go programming language used to build Docker.
  - `Git commit`: Commit hash for the build.
  - `Built`: Date and time of the build.
  - `OS/Arch`: Operating system and architecture for the client.

- **Server** (Docker Daemon):
  - Similar details as the client section, showing the version and API compatibility of the server.

**Example Output**:
```plaintext
Client:
 Version:           23.0.0
 API version:       1.41
 Go version:        go1.16.6
 Git commit:        abcdef1
 Built:             Fri Jul 2 12:34:56 2023
 OS/Arch:           linux/amd64

Server:
 Engine:
  Version:          23.0.0
  API version:      1.41 (minimum version 1.12)
  Go version:       go1.16.6
  Git commit:       abcdef1
  Built:            Fri Jul 2 12:34:56 2023
  OS/Arch:          linux/amd64
  Experimental:     false
```

### `docker info`
The `docker info` command provides detailed information about the Docker daemon, including the system’s current status, storage drivers, and network configurations. It’s useful for diagnosing issues and understanding system resources.

```bash
docker info
```

#### Output includes:
- **General System Information**:
  - `Containers`: Total containers and their states (running, stopped).
  - `Images`: Total number of images stored.
  - `Storage Driver`: Name of the storage driver in use (e.g., `overlay2`, `aufs`).
  - `Kernel Version`: Linux kernel version (on Linux systems).
  - `Operating System`: OS details.
  - `Architecture`: System architecture.
  - `Docker Root Dir`: Location of Docker storage on disk.

- **Resource Limits**:
  - `CPUs`: Number of CPU cores Docker can access.
  - `Total Memory`: Total memory Docker can use.

- **Security and Network Configurations**:
  - `Cgroup Driver`: Cgroup management driver.
  - `Plugins`: Installed plugins (Network, Volume, etc.).
  - `Network`: Default network configurations.
  - `Registry`: Default image registry (usually Docker Hub).

**Example Output**:
```plaintext
Containers: 5
 Running: 2
 Paused: 0
 Stopped: 3
Images: 10
Storage Driver: overlay2
...
CPUs: 4
Total Memory: 16GiB
...
Docker Root Dir: /var/lib/docker
Debug Mode: false
...
```

### Use Cases
- **`docker version`**: For compatibility checks and ensuring the correct versions of Docker components are installed.
- **`docker info`**: For system diagnostics, resource availability, and Docker environment setup details.

A **Docker container** is a lightweight, standalone, executable package of software that includes everything needed to run an application: code, runtime, libraries, and system tools. Containers are isolated from one another and from the host system, ensuring that applications run consistently across different environments.

Here are some essential commands related to Docker containers:

---

### 1. **Starting and Running Containers**

- **Run a New Container**: 
  ```bash
  docker container run [OPTIONS] IMAGE [COMMAND] [ARG...]
  ```
  - `docker run -d nginx`: Runs an NGINX container in detached mode.
  - `docker run -it ubuntu bash`: Runs an Ubuntu container interactively with a Bash shell.

- **Start a Stopped Container**:
  ```bash
  docker start <container_id or name>
  ```

- **Run Container with Port Mapping**:
  ```bash
  docker run -p <host_port>:<container_port> IMAGE
  ```
  - Example: `docker run -p 8080:80 nginx` maps port 80 in the container to port 8080 on the host.

---

### 2. **Container Management**

- **List Running Containers**:
  ```bash
  docker ps
  ```

- **List All Containers (Running and Stopped)**:
  ```bash
  docker ps -a
  ```

- **Stop a Running Container**:
  ```bash
  docker stop <container_id or name>
  ```

- **Restart a Container**:
  ```bash
  docker restart <container_id or name>
  ```

- **Remove a Stopped Container**:
  ```bash
  docker rm <container_id or name>
  ```

- **Remove All Stopped Containers**:
  ```bash
  docker container prune
  ```

---

### 3. **Inspecting and Accessing Containers**

- **View Detailed Container Information**:
  ```bash
  docker inspect <container_id or name>
  ```

- **View Logs for a Container**:
  ```bash
  docker logs <container_id or name>
  ```

- **Attach to a Running Container** (reconnect to a container’s process):
  ```bash
  docker attach <container_id or name>
  ```

- **Access a Running Container with a Shell**:
  ```bash
  docker exec -it <container_id or name> /bin/bash
  ```
  - `docker exec -it <container_id> /bin/sh` is used for containers with minimal OS environments that lack Bash.

---

### 4. **Container Networking**

- **List Networks**:
  ```bash
  docker network ls
  ```

- **Connect a Container to a Network**:
  ```bash
  docker network connect <network_name> <container_id or name>
  ```

- **Disconnect a Container from a Network**:
  ```bash
  docker network disconnect <network_name> <container_id or name>
  ```

---

### 5. **Saving and Loading Containers**

- **Commit Changes to a Container as a New Image**:
  ```bash
  docker commit <container_id or name> <new_image_name>
  ```

- **Export a Container’s Filesystem as a Tar Archive**:
  ```bash
  docker export <container_id or name> > <filename>.tar
  ```

- **Import a Container’s Filesystem from a Tar Archive**:
  ```bash
  docker import <filename>.tar
  ```

---

### 6. **Container Cleanup**

- **Remove All Containers (Running and Stopped)**:
  ```bash
  docker rm -f $(docker ps -aq)
  ```

- **Remove Unused Containers, Images, and Networks**:
  ```bash
  docker system prune
  ```

---

These commands are fundamental for managing Docker containers, whether it’s starting, stopping, accessing, networking, or cleaning up containers. 

Here are examples of how to run, stop, and remove Docker containers for **nginx**, **httpd** (Apache HTTP Server), and **MySQL**. Each example includes the commands for creating the container, stopping it, and then removing it.

### 1. Nginx Example

**Running the Nginx Container**
```bash
docker container run -d -p 8080:80 --name nginx_server nginx
```
- **Explanation**: This command runs an Nginx container in detached mode (`-d`), mapping port `8080` on the host to port `80` in the container. The container is named `nginx_server`.

**Stopping the Nginx Container**
```bash
docker container stop nginx_server
```
- **Explanation**: This command stops the running Nginx container named `nginx_server`.

**Removing the Nginx Container**
```bash
docker container rm nginx_server
```
- **Explanation**: This command removes the stopped Nginx container named `nginx_server`.

---

### 2. Apache HTTP Server (httpd) Example

**Running the Httpd Container**
```bash
docker container run -d -p 8081:80 --name httpd_server httpd
```
- **Explanation**: This command runs an Apache HTTP Server container in detached mode, mapping port `8081` on the host to port `80` in the container. The container is named `httpd_server`.

**Stopping the Httpd Container**
```bash
docker container stop httpd_server
```
- **Explanation**: This command stops the running Apache HTTP Server container named `httpd_server`.

**Removing the Httpd Container**
```bash
docker container rm httpd_server
```
- **Explanation**: This command removes the stopped Apache HTTP Server container named `httpd_server`.

---

### 3. MySQL Example

**Running the MySQL Container**
```bash
docker container run -d -p 3307:3306 --name mysql_server -e MYSQL_ROOT_PASSWORD=my-secret-pw mysql
```
- **Explanation**: This command runs a MySQL container in detached mode, mapping port `3307` on the host to port `3306` in the container. The container is named `mysql_server`, and the root password for MySQL is set to `my-secret-pw` using the `MYSQL_ROOT_PASSWORD` environment variable.

**Stopping the MySQL Container**
```bash
docker container stop mysql_server
```
- **Explanation**: This command stops the running MySQL container named `mysql_server`.

**Removing the MySQL Container**
```bash
docker container rm mysql_server
```
- **Explanation**: This command removes the stopped MySQL container named `mysql_server`.

---

### Summary of Commands

| Service | Run Command | Stop Command | Remove Command |
|---------|-------------|--------------|----------------|
| Nginx   | `docker container run -d -p 8080:80 --name nginx_server nginx` | `docker container stop nginx_server` | `docker container rm nginx_server` |
| Httpd   | `docker container run -d -p 8081:80 --name httpd_server httpd` | `docker container stop httpd_server` | `docker container rm httpd_server` |
| MySQL   | `docker container run -d -p 3307:3306 --name mysql_server -e MYSQL_ROOT_PASSWORD=my-secret-pw mysql` | `docker container stop mysql_server` | `docker container rm mysql_server` |

