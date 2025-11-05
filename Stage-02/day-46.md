## Day 46: Deploy an App on Docker Containers

**Challenge:** Deploy a two-container stack (Web + DB) using Docker Compose.

---

### Steps Followed

1. **Create the Docker Compose File**
   ```bash
   vi docker-compose.yml
   ```

2. **Add Configuration**
   ```yaml
   version: "3"
   services:
     web:
       image: php:apache
       container_name: php_apache
       ports:
         - "5004:80"
       volumes:
         - /var/www/html:/var/www/html
       depends_on:
         - db

     db:
       image: mariadb:latest
       container_name: mysql_apache
       ports:
         - "3306:3306"
       volumes:
         - /var/lib/mysql:/var/lib/mysql
       environment:
         MYSQL_DATABASE: database_apache
         MYSQL_USER: appuser
         MYSQL_PASSWORD: QWERTY@123
         MYSQL_ROOT_PASSWORD: R00@123
   ```

3. **Run the Stack**
   ```bash
   docker compose up -d
   ```

4. **Verify Running Containers**
   ```bash
   docker ps
   ```

---
### Result & Insights
✅ Successfully deployed **web (PHP + Apache)** and **database (MariaDB)** containers.  
💡 Learned how to manage multi-service applications using **Docker Compose** for better portability and
