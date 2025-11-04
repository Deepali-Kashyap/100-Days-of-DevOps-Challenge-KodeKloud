## Day 36: Deploy Nginx Container on Application Server

**Challenge:** Deploy and verify an Nginx container using the lightweight `nginx:alpine` image on Application Server 3.

---

### Steps Followed

1. **Login to Application Server 3**  
   ```bash
   ssh tony@stapp03
   ```
   - Connect to the target server where the container will be deployed.  
   *(Replace `stapp03` with your actual hostname or IP address if different.)*

2. **Verify Docker Installation and Status**  
   ```bash
   docker --version
   systemctl status docker
   ```
   - Checks if Docker is installed and running.

   If Docker is not running:
   ```bash
   sudo systemctl start docker
   ```

3. **Pull the Nginx Alpine Image**  
   ```bash
   docker pull nginx:alpine
   ```
   - Downloads the lightweight, production-ready Nginx image based on Alpine Linux.

4. **Run the Nginx Container**  
   ```bash
   docker run -d --name nginx_3 nginx:alpine
   ```
   - `-d` → Runs the container in detached mode (background).  
   - `--name nginx_3` → Assigns a custom name to the container.  
   - `nginx:alpine` → Specifies the image to use.

5. **Verify the Container Status**  
   ```bash
   docker ps
   ```
   - Lists running containers to confirm that `nginx_3` is active and healthy.

---

### Outcome
- Nginx container named **nginx_3** successfully deployed using the `nginx:alpine` image.  
- Verified Docker service status and confirmed container is running.  
- Application server ready to serve web traffic via the containerized Nginx instance.
### Key Learnings
- Running containers using Docker CLI.  
- Using lightweight images like `nginx:alpine` for optimized deployment.  
- Managing container lifecycle and verifying service status.  
- Building a foundation for containerized web server deployments.
