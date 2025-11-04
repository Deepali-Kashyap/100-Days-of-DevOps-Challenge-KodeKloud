## Day 38: Pull Docker Image

**Challenge:** Pull a Docker image from a registry, verify the download, and retag it for versioning or naming consistency.

---

### Steps Followed

1. **Login to the Required Server**  
   ```bash
   ssh tony@stapp01
   ```
   - Connect to the server where you will manage Docker images.

2. **Pull the Docker Image**  
   ```bash
   docker pull image_name
   ```
   - Downloads the specified image from Docker Hub (or a private registry).  
   - Example:  
     ```bash
     docker pull nginx:alpine
     ```

3. **Verify Available Docker Images**  
   ```bash
   docker images
   ```
   - Lists all locally available Docker images with their repository, tag, and image ID.  
   - Confirms that the image has been successfully pulled.

4. **Retag the Pulled Image**  
   ```bash
   docker tag old_name new_name
   ```
   - Creates a new tag (alias) for an existing image.  
   - Example:  
     ```bash
     docker tag nginx:alpine myrepo/nginx:latest
     ```
   - Useful for organizing images or preparing them for push to a private registry.

---

### Outcome
- Successfully pulled the specified Docker image from the registry.  
- Verified its presence in local storage using `docker images`.  
- Retagged the image for versioning or repository consistency.
### Key Learnings
- Pulling Docker images from registries using `docker pull`.  
- Listing and managing local images with `docker images`.  
- Retagging images to align with deployment or registry naming conventions.  
- Essential workflow for managing image versions in CI/CD pipelines.
