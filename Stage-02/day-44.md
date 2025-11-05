## Day 44: Write a Docker Compose File

**Challenge:** Create a Docker Compose configuration to deploy an Apache HTTP server container with port and volume mappings.

---

### Steps Followed

1. **Navigate to the Docker Directory**
   ```bash
   cd /opt/docker
   ```

2. **Create the Docker Compose File**
   ```bash
   vi docker-compose.yml
   ```

   **Content:**
   ```yaml
   version: '3'
   services:
     webserver:
       image: httpd:latest
       container_name: httpd
       ports:
         - "5001:80"
       volumes:
         - /opt/finance:/usr/local/apache2/htdocs
   ```

---

3. **Start the Container Using Docker Compose**
   ```bash
   docker-compose up -d
   ```

4. **Verify the Container is Running**
   ```bash
   docker ps
   ```

---
### Result & Insights
✅ Successfully launched an **Apache (httpd)** container using **Docker Compose**.  
💡 Learned how to define **services**, **port mapping**, and **volume bindings** in a single YAML configuration for automated deployment.
