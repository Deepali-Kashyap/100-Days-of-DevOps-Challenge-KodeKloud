## Day 41: Write a Dockerfile

**Challenge:** Create a custom Docker image that installs Apache and runs it on port **3002**.

---

### Steps Followed

1. **Create a Dockerfile**
   ```bash
   vi Dockerfile
   ```

   **Content:**
   ```dockerfile
   # Use Ubuntu 24.04 as the base image
   FROM ubuntu:24.04

   # Install Apache2
   RUN apt-get update && apt-get install -y apache2

   # Change Apache to listen on port 3002
   RUN sed -i 's/Listen 80/Listen 3002/' /etc/apache2/ports.conf

   # Expose port 3002
   EXPOSE 3002

   # Start Apache service when container runs
   CMD ["apache2ctl", "-D", "FOREGROUND"]
   ```

---

2. **Build the Docker Image**
   ```bash
   docker build -t apache:3002 .
   ```
   - Builds a new image named **apache:3002**
   - Includes Apache configured to listen on **port 3002**

---

3. **Run the Container**
   ```bash
   docker run -d --name apache_3002 -p 3002:3002 apache:3002
   ```
   - Runs the container in background  
   - Maps host port **3002** → container port **3002**

---

4. **Verify Apache Inside the Container**
   ```bash
   docker exec -it apache_3002 ss -tuln | grep 3002
   ```

---
### Result & Insights
✅ Successfully built and deployed a **custom Apache Docker image** on port **3002**.  
💡 Learned how to write a **Dockerfile**, modify configs inside images, and run containers with **custom ports**.
