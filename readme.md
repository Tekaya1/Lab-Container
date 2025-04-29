<details>
<summary># Exercise 1</summary>

<details>
<summary>## 🐋 Working with Podman</summary>

<details>
<summary>### 1️⃣ Install the Podman package (as root)</summary>

```bash
sudo apt update && sudo apt install -y podman
```

</details>

<details>
<summary>### 2️⃣ Create the `webadmin` user with the password "web" (as root)</summary>

```bash
sudo useradd -m webadmin
echo "web:web" | sudo chpasswd
```

</details>

<details>
<summary>### 3️⃣ Connect via SSH to the `webadmin` account</summary>

```bash
ssh webadmin@localhost
```

</details>

<details>
<summary>### 4️⃣ Search for all `httpd` images (as `webadmin`)</summary>

```bash
podman search httpd
```

</details>

<details>
<summary>### 5️⃣ Pull the `httpd` image (as `webadmin`)</summary>

```bash
podman pull docker.io/library/httpd
```

</details>

<details>
<summary>### 6️⃣ List available images (as `webadmin`)</summary>

```bash
podman images
```

</details>

<details>
<summary>### 7️⃣ Inspect the `httpd` image (as `webadmin`)</summary>

Replace `<IMAGE_ID>` with the actual image ID:
```bash
podman inspect <IMAGE_ID>
```

</details>

<details>
<summary>### 8️⃣ Run a rootless container with the `httpd` image (as `webadmin`)</summary>

```bash
mkdir -p /home/webadmin/web
podman run -d --name web -p 8081:80 -v /home/webadmin/web:/usr/local/apache2/htdocs:Z httpd
```

</details>

<details>
<summary>### 9️⃣ List created and active containers (as `webadmin`)</summary>

```bash
podman ps
```

</details>

</details>

<details>
<summary>## 📁 Managing Web Content</summary>

<details>
<summary>### 🔟 Create a web page named `index.html` in the container (as `webadmin`)</summary>

```bash
echo "Bonjour Tekup" > /home/webadmin/web/index.html
```

</details>

</details>

<details>
<summary>## 🛠️ Container Maintenance</summary>

<details>
<summary>### 1️⃣1️⃣ Generate a systemd service for the container (as `webadmin`)</summary>

```bash
podman generate systemd --name web --files --new
mv container-web.service ~/.config/systemd/user/
```

</details>

<details>
<summary>### 1️⃣2️⃣ Start and enable the service at boot (as `webadmin`)</summary>

```bash
systemctl --user enable container-web.service
systemctl --user start container-web.service
```

</details>

<details>
<summary>### 1️⃣3️⃣ Test the `index.html` page in your browser or locally</summary>

Access `http://localhost:8081` in your browser or use:
```bash
curl http://localhost:8081
```

</details>

<details>
<summary>### 1️⃣4️⃣ Reboot and test the systemd service (as root)</summary>

```bash
sudo reboot
```
After reboot, verify the service:
```bash
sudo systemctl status container-web.service
```

</details>

<details>
<summary>### 1️⃣5️⃣ Remove the container (as `webadmin`)</summary>

Replace `<CONTAINER_ID>` with the actual container ID:
```bash
podman stop <CONTAINER_ID>
podman rm <CONTAINER_ID>
```

</details>

<details>
<summary>### 1️⃣6️⃣ Remove the `httpd` image (as `webadmin`)</summary>

Replace `<IMAGE_ID>` with the actual image ID:
```bash
podman rmi <IMAGE_ID>
```

</details>

</details>

</details>