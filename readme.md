# Exercise 1

## 🐋 Working with Podman

### 🔍 Search for the `httpd` image
```bash
podman search httpd
```

### 📥 Pull the `httpd` image
```bash
podman pull docker.io/library/httpd
```

### 📋 List available images
```bash
podman images
```

### 🔎 Inspect the image
Replace `<IMAGE_ID>` with the actual image ID:
```bash
podman inspect <IMAGE_ID>
```

### 🚀 Run a container with the `httpd` image
```bash
podman run -d --name web -p 8081:80 -v /home/webadmin/web:/usr/local/apache2/htdocs:Z httpd
```

### 📂 List running containers
```bash
podman ps
```

### 📂 List all containers (including stopped ones)
```bash
podman ps -a
```

### ⏹️ Stop a container
Replace `<CONTAINER_ID>` with the actual container ID:
```bash
podman stop <CONTAINER_ID>
```

### 🗑️ Remove a container
Replace `<CONTAINER_ID>` with the actual container ID:
```bash
podman rm <CONTAINER_ID>
```

## 📁 Managing Web Content

### 📂 Create a directory for web content
```bash
mkdir -p /home/webadmin/web
```

### ✏️ Add content to the web server
```bash
echo "Bonjour Tekup" > /home/webadmin/web/index.html
```

## 🛠️ Container Maintenance

### 🐚 Access the container's shell
```bash
podman exec -it web /bin/bash
```

### 🔄 Enable lingering for the `webadmin` user
```bash
loginctl enable-linger webadmin
```

### 📜 Check logs for the container service
```bash
journalctl | grep container-web.service
```