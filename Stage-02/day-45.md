## Day 45: Resolve Dockerfile Issues

**Challenge:** Fix syntax errors in a Dockerfile and successfully build and run the image.

---

### Steps Followed

1. **Correct the Dockerfile Syntax**
   - Fixed formatting and command structure as per Dockerfile best practices.

2. **Build the Image**
   ```bash
   docker build -t httpd .
   ```

3. **Run the Container**
   ```bash
   docker run -d --name mycontainer -p 8080:8080 httpd:latest
   ```

---

### Result & Insights
✅ Dockerfile built successfully after corrections.  
💡 Gained clarity on **Dockerfile syntax** and **container deployment workflow**.
