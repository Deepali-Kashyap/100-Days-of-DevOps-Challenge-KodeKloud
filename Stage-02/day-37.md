## Day 37: Copy File to Docker Container

**Challenge:** Copy a file from the host system into a running Docker container and verify the file transfer.

---

### Steps Followed

1. **Login to Application Server 3**  
   ```bash
   ssh tony@stapp03
   ```
   - Connect to the application server where the container is running.

2. **List Running Containers**  
   ```bash
   docker ps
   ```
   - Displays all active containers and their names.  
   - Identify the container name (in this case, **ubuntu_latest**).

3. **Copy the File to the Container**  
   ```bash
   docker cp /tmp/nautilus.txt.gpg ubuntu_latest:/usr/src/
   ```
   - `docker cp` → Copies files or directories between the host and container.  
   - `/tmp/nautilus.txt.gpg` → Source file on the host.  
   - `ubuntu_latest:/usr/src/` → Destination path inside the container.

4. **Verify the File Inside the Container**  
   ```bash
   docker exec -it ubuntu_latest ls -l /usr/src/
   ```
   - Executes a command inside the running container.  
   - Lists files in `/usr/src/` to confirm the copied file exists.

---

### Outcome
- Successfully copied `nautilus.txt.gpg` from host to `/usr/src/` in the **ubuntu_latest** container.  
- Verified file presence using `docker exec`.  
- Demonstrated file transfer capabilities between host and container environments.
### Key Learnings
- Using `docker cp` to transfer files between host and containers.  
- Executing commands within containers using `docker exec`.  
- Validating file operations inside a running Docker container.  
- Essential for debugging, configuration management, and runtime data updates.
