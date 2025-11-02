## Day 25: Git Merge Branches

**Challenge:** Create a new branch, make changes, and merge it back into the master branch on the storage server to practice Git branching and merging operations.

---

### Steps Followed

1. Login to the Storage Server  
   ```bash
   ssh natasha@ststor01
   ```

2. Navigate to the Repository Directory  
   ```bash
   cd /usr/src/kodekloudrepos/cluster
   ```

3. Switch to Master Branch  
   ```bash
   git checkout master
   ```
   - Ensures you start from the latest version of the main branch.

4. Create a New Branch  
   ```bash
   git checkout -b devops
   ```
   - Creates and switches to a new branch named **devops**.

5. Copy and Add Files  
   ```bash
   cp /tmp/index.html .
   git add .
   git commit -m "added file"
   ```
   - Copies `index.html` into the repo, stages it, and commits the change to the **devops** branch.

6. Merge the Branch into Master  
   ```bash
   git checkout master
   git merge devops
   ```
   - Merges the changes from the **devops** branch into the **master** branch.

7. Push Changes to Remote Repository  
   ```bash
   git push origin master
   git push origin devops
   ```
   - Pushes both the master and devops branches to the remote Git repository.

---

### Outcome
- New branch **devops** created and updated with a committed file.  
- Successfully merged **devops** branch into **master** without conflicts.  
- Both branches pushed to the remote repository.  
### Key Learnings
- Creating and merging branches using Git for collaborative workflows.  
- Managing commits and version history across branches.  
- Using `git merge` to integrate development changes into the main codebase.  
- Understanding remote synchronization with `git push` for multiple branches.
