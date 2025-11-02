## Day 21: Set Up Git Repository on Storage Server

**Challenge:** Configure and initialize a Git bare repository on the storage server to enable centralized version control and collaboration.

---

### Steps Followed

1. Login to the Storage Server  
   ```bash
   ssh natasha@ststor01
   ```

2. Install Git  
   ```bash
   sudo yum install git -y
   ```
   - Installs Git package required for source code management.

3. Create Repository Directory  
   ```bash
   sudo mkdir -p /opt/demo.git
   ```
   - Creates a directory where the shared Git repository will be stored.

4. Initialize a Bare Repository  
   ```bash
   sudo git init --bare /opt/demo.git
   ```
   - Initializes a **bare Git repository**.  
   - Bare repositories are used for **remote collaboration**, not direct code editing.  
   - This allows multiple users to **clone**, **push**, and **pull** code changes safely.

---

### Outcome
- Git successfully installed on the storage server.  
- `/opt/demo.git` initialized as a **bare repository** ready for remote access.  
- Repository structure correctly configured for collaborative development.  

### Key Learnings
- Understanding the difference between standard and bare Git repositories.  
- Setting up a remote Git repo for team collaboration.  
- Basic Git administrative setup using command-line tools.  
- Preparing infrastructure for version-controlled project management.
