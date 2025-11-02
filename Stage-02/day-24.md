## Day 24: Git Create Branches

**Challenge:** Create and verify a new branch in a Git repository on the storage server for version control and feature isolation.

---

### Steps Followed

1. Login to the Storage Server  
   ```bash
   ssh natasha@ststor01
   ```

2. Navigate to the Repository Directory  
   ```bash
   cd /usr/src/kodekloudrepos/apps
   ```
   - Move to the directory where the Git repository is located.

3. Switch to the Master Branch  
   ```bash
   git checkout master
   ```
   - Ensures that you are working from the latest version of the main branch before creating a new one.

4. Create a New Branch  
   ```bash
   git checkout -b xfusioncorp_master
   ```
   - Creates and switches to a new branch named **xfusioncorp_master**.

5. Verify Branch Creation  
   ```bash
   git branch
   ```
   - Displays a list of all branches.  
   - Confirms the new branch `xfusioncorp_master` has been successfully created and is currently checked out.

---

### Outcome
- New Git branch `xfusioncorp_master` created successfully from the master branch.  
- Verified branch structure using `git branch`.  
- Repository ready for isolated feature development or configuration changes.  
### Key Learnings
- Creating and managing Git branches for version control.  
- Understanding branch-based workflows in Git.  
- Ensuring safe and isolated development environments.  
- Using `git checkout` effectively to switch or create branches.
