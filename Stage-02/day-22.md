## Day 22: Clone Git Repository on Storage Server

**Challenge:** Clone an existing Git repository from a local path on the storage server and verify that the repository has been successfully copied.

---

### Steps Followed

1. Login to the Storage Server  
   ```bash
   ssh natasha@ststor01
   ```

2. Switch to Root User  
   ```bash
   sudo su -
   ```

3. Navigate to the Target Directory  
   ```bash
   cd /usr/src/kodekloudrepos
   ```
   - This is where the repository clone will be stored.

4. Clone the Git Repository  
   ```bash
   git clone /opt/apps.git
   ```
   - Clones the existing **bare repository** `/opt/apps.git` into the current directory.  
   - Creates a working copy for development or deployment.

5. Verify the Cloned Repository  
   ```bash
   ls -l /usr/src/kodekloudrepos
   ```
   - Ensures the repository (`apps`) has been cloned successfully.

### Outcome
- Repository `/opt/apps.git` cloned successfully to `/usr/src/kodekloudrepos`.  
- Verified that the directory contains the cloned repository files.  
- Ready for future commits, modifications, or deployment.  

### Key Learnings
- Cloning repositories from local storage paths using Git.  
- Understanding the difference between bare and working repositories.  
- Verifying cloned repositories for proper setup and accessibility.  
- Managing Git-based code distribution within a controlled environment.
