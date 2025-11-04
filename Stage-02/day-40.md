## Day 40: Docker EXEC Operations

**Challenge:** Access a running Docker container, install Apache, change its default port, and verify the configuration.

---

### Steps Followed

1. **Login to App Server 2**  
   ```bash
   ssh steve@stapp02
   ```

2. **Check Running Containers**  
   ```bash
   docker ps
   ```
   - Note the container ID or name of the running instance.

3. **Access the Container Shell**  
   ```bash
   docker exec -it <container_ID> /bin/bash
   ```

4. **Update Package List (Inside Container)**  
   ```bash
   apt-get update
   ```

5. **Install Apache2**  
   ```bash
   apt install -y apache2
   ```

6. **Change Apache Port (80 → 3000)**  
   - Edit ports configuration:
     ```bash
     vi /etc/apache2/ports.conf
     ```
     Replace:
     ```
     Listen 80
     ```
     With:
     ```
     Listen 3000
     ```
   - Edit virtual host configuration:
     ```bash
     vi /etc/apache2/sites-available/000-default.conf
     ```
     Update:
     ```
     <VirtualHost *:3000>
     ```

7. **Restart Apache Service**  
   ```bash
   service apache2 restart
   ```

8. **Verify Apache Listening on Port 3000**  
   ```bash
   netstat -tuln | grep 3000
   ```

---
### Result & Insights
✅ Successfully accessed the container shell using `docker exec`.  
✅ Installed and configured Apache2 inside the container.  
✅ Modified Apache to run on **port 3000** and verified it’s actively listening.  
💡 Learned to manage services inside containers interactively, edit configuration files, and perform full-stack operations within an active Docker environment.
