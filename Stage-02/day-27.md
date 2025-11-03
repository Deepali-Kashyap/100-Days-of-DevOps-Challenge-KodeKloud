## Day 27: Git Revert Some Changes

**Challenge:** Revert recent changes in a Git repository on the storage server using `git revert` to maintain stable project history without losing previous commits.

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
   - Access the Git repository where changes need to be reverted.

3. Check Commit History  
   ```bash
   git log
   ```
   - Displays recent commits and their respective commit IDs for reference.

4. Revert the Most Recent Commit  
   ```bash
   git revert HEAD
   ```
   - Creates a new commit that undoes the changes made in the latest commit.

5. Check Repository Status  
   ```bash
   git status
   ```
   - Verifies if any files remain staged, untracked, or modified.

6. Stage and Commit the Revert (if needed)  
   ```bash
   git add .
   git commit -m "Revert apps"
   ```
   - Ensures all reverted changes are committed properly to maintain clean repository state.

---
### Outcome
- The most recent commit successfully reverted using `git revert`.  
- Repository returned to a stable version without modifying existing commit history.  
- Verified repository status after the revert operation.  
### Key Learnings
- Using `git revert` to safely undo changes without rewriting commit history.  
- Understanding the difference between `git revert` and `git reset`.  
- Maintaining repository integrity by using proper revert workflows.  
- Practicing good Git hygiene with verification steps (`git log`, `git status`).
