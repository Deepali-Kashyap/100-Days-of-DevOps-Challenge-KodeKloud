## Day 31: Git Stash

**Challenge:** Restore previously stashed changes in a Git repository, commit them, and push the updates to the remote master branch.

---

### Steps Followed

1. Navigate to the Repository Directory  
   ```bash
   cd /usr/src/kodekloudrepos/ecommerce
   ```
   - Move to the Git repository where the stash was previously created.

2. Check Available Stashes  
   ```bash
   git stash list
   ```
   - Lists all stashed changes.  
   - Identify the stash you want to restore, for example:  
     ```
     stash@{1}: WIP on master: updated ecommerce configuration
     ```

3. Apply the Specific Stash  
   ```bash
   git stash apply stash@{1}
   ```
   - Restores the changes saved in the specified stash.  
   - The stash remains in the list until explicitly dropped.

4. Stage and Commit the Restored Changes  
   ```bash
   git add .
   git commit -m "Restored stash changes"
   ```
   - Stages and commits the restored modifications to the local repository.

5. Push the Changes to Remote Repository  
   ```bash
   git push origin master
   ```
   - Updates the remote **master** branch with the committed stash changes.

---
### Outcome
- Successfully restored and applied previously stashed changes.  
- Committed and pushed updates to the remote master branch.  
- Verified that all intended modifications were preserved and versioned.  
### Key Learnings
- Using `git stash` to temporarily save and restore uncommitted changes.  
- Applying specific stashes using the stash index (e.g., `stash@{1}`).  
- Committing and pushing restored work to maintain version control consistency.  
- Understanding how stashing helps in context switching during development.
