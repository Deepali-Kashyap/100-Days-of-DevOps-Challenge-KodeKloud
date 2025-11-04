## Day 39: Create a Docker Image From Container

**Challenge:** Create a new Docker image from a running container and verify the new image is available locally.

---

### Steps Followed

1. **Login to Application Server 2**  
   ```bash
   ssh steve@stapp02
   ```
   - Connect to the server where the container is running.

2. **List Running Containers**  
   ```bash
   docker ps
   ```
   - Confirms that the container `ubuntu_latest` is active and available.

3. **Create a New Image from the Running Container**  
   ```bash
   docker commit ubuntu_latest media:datacenter
   ```
   - `docker commit` captures the current state of the container and saves it as a new image.  
   - `media:datacenter` represents the new repository name and tag.

4. **Verify the New Docker Image**  
   ```bash
   docker images
   ```
  - Confirms that the new image (`media:datacenter`) was successfully created from the container.

---
## Result & Insights
✅ Created a new Docker image **media:datacenter** from the running container **ubuntu_latest**.  
✅ Verified its successful creation using `docker images`.  
💡 Learned how `docker commit` helps capture container states and convert them into reusable images for further deployment or backup..
