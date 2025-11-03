## Day 28: Git Cherry Pick

**Challenge:** Apply a specific commit from one branch (feature) to another (master) using `git cherry-pick`, allowing selective integration of changes.

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

3. View Commit History from the Feature Branch  
   ```bash
   git log feature --oneline
   ```
   - Displays recent commits from the **feature** branch in a short format.
   - Identify the commit you want to cherry-pick, e.g.:
     ```
     a1b2c3d Update info.txt
     ```

4. Switch to the Master Branch  
   ```bash
   git checkout master
   ```

5. Cherry-Pick the Specific Commit  
   ```bash
   git cherry-pick a1b2c3d
   ```
   - Applies the changes from the commit `a1b2c3d` onto the **master** branch.  
   - If conflicts appear, resolve them and continue with:
     ```bash
     git add .
     git cherry-pick --continue
     ```

6. Push Changes to the Remote Repository  
   ```bash
   git push origin master
   ```
   - Updates the remote **master** branch with the cherry-picked commit.

---

### Outcome
- Specific commit successfully cherry-picked from the **feature** branch to **master**.  
- Repository updated and changes pushed to the remote.  
- Maintained clean commit history with precise control over applied changes.  
### Key Learnings
- Understanding how `git cherry-pick` selectively applies individual commits.  
- Managing targeted updates without merging entire branches.  
- Safely handling conflicts during cherry-pick operations.  
- Strengthening Git branching workflows for controlled deployments.
