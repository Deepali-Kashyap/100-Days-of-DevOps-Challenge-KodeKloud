## Day 47: Docker Python App

**Challenge:** Create a Dockerfile for a Python-based application, build the image, and run the container with proper port mapping.

---

### Steps Followed

1. **Create a Dockerfile**
   ```bash
   vi Dockerfile
   ```

2. **Add the Following Content**
   ```dockerfile
   FROM python:3.9
   WORKDIR /app
   COPY src/ /app/
   RUN pip install --no-cache-dir -r requirements.txt
   EXPOSE 8082
   CMD ["python", "server.py"]
   ```

3. **Build the Image**
   ```bash
   docker build -t nautilus/python-app .
   ```

4. **Run the Container**
   ```bash
   docker run -d --name pythonapp_nautilus -p 8093:6100 nautilus/python-app
   ```

   ✅ Creates a container **pythonapp_nautilus**  
   🔁 Maps **host port 8093 → container port 6100**

5. **Test the Application**
   ```bash
   curl http://localhost:8093/
   ```

---
### Result & Insights
✅ Successfully built and deployed the **Python application container**.  
💡 Reinforced understanding of **Dockerfile structure**, **image building**, and **port mapping** for Python-based services.
