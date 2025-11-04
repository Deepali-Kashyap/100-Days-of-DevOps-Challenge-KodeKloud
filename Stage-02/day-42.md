## Day 43: Docker Ports Mapping

**Challenge:** Deploy an Nginx container and expose it on a custom host port using Docker port mapping.

---
### Steps Followed

1. **Pull the Nginx Alpine Image**  
   ```bash
   docker pull nginx:alpine
   ```
2. **Run the Container with Port Mapping**  
   ```bash
   docker run -d --name news -p 6100:80 nginx:alpine
   ```
   - `-d` → runs in detached mode  
   - `--name news` → names the container  
   - `-p 6100:80` → maps host port **6100** to container port **80**

---
### Result & Insights
✅ Successfully deployed a running Nginx container accessible on **http://<server-ip>:6100**  
💡 Learned how Docker **port mapping (-p)** connects host and container ports, enabling external access to containerized web services.
