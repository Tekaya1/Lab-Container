# Exercise 1

## 🐋 Working with Podman

### 1️⃣ Install the Podman package (as root)
```bash
sudo apt update && sudo apt install -y podman
```

### 2️⃣ Create the `webadmin` user with the password "web" (as root)
```bash
sudo useradd -m webadmin
echo "web:web" | sudo chpasswd
```

### 3️⃣ Connect via SSH to the `webadmin` account
```bash
ssh webadmin@localhost
```

### 4️⃣ Search for all `httpd` images (as `webadmin`)
```bash
podman search httpd
```

### 5️⃣ Pull the `httpd` image (as `webadmin`)
```bash
podman pull docker.io/library/httpd
```

### 6️⃣ List available images (as `webadmin`)
```bash
podman images
```

### 7️⃣ Inspect the `httpd` image (as `webadmin`)
Replace `<IMAGE_ID>` with the actual image ID:
```bash
podman inspect <IMAGE_ID>
```

### 8️⃣ Run a rootless container with the `httpd` image (as `webadmin`)
```bash
mkdir -p /home/webadmin/web
podman run -d --name web -p 8081:80 -v /home/webadmin/web:/usr/local/apache2/htdocs:Z httpd
```

### 9️⃣ List created and active containers (as `webadmin`)
```bash
podman ps
```

## 📁 Managing Web Content

### 🔟 Create a web page named `index.html` in the container (as `webadmin`)
```bash
echo "Bonjour Tekup" > /home/webadmin/web/index.html
```

## 🛠️ Container Maintenance

### 1️⃣1️⃣ Generate a systemd service for the container (as `webadmin`)
```bash
podman generate systemd --name web --files --new
mv container-web.service ~/.config/systemd/user/
```

### 1️⃣2️⃣ Start and enable the service at boot (as `webadmin`)
```bash
systemctl --user enable container-web.service
systemctl --user start container-web.service
```

### 1️⃣3️⃣ Test the `index.html` page in your browser or locally
Access `http://localhost:8081` in your browser or use:
```bash
curl http://localhost:8081
```

### 1️⃣4️⃣ Reboot and test the systemd service (as root)
```bash
sudo reboot
```
After reboot, verify the service:
```bash
sudo systemctl status container-web.service
```

### 1️⃣5️⃣ Remove the container (as `webadmin`)
Replace `<CONTAINER_ID>` with the actual container ID:
```bash
podman stop <CONTAINER_ID>
podman rm <CONTAINER_ID>
```

### 1️⃣6️⃣ Remove the `httpd` image (as `webadmin`)
Replace `<IMAGE_ID>` with the actual image ID:
```bash
podman rmi <IMAGE_ID>
```