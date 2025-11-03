## Day 30: Git Hard Reset

**Challenge:** Perform a Git hard reset to revert the repository to a specific commit, discarding unwanted changes and force-pushing the updated state to the remote repository.

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
   - Access the Git repository that needs to be reset.

3. View the Commit History  
   ```bash
   git log --oneline
   ```
   - Displays a concise list of recent commits.  
   - Identify the **commit ID** you want to reset the repository to.

4. Perform a Hard Reset  
   ```bash
   git reset --hard <commit-id>
   ```
   - Resets the working directory, staging area, and current branch to the specified commit.  
   - All changes after that commit are permanently discarded.

5. Force Push the Changes to Remote  
   ```bash
   git push --force
   ```
   - Updates the remote repository to match the local reset state.  
   - Required because the reset rewrites commit history.

---
### Outcome
- Repository successfully reset to a specific commit.  
- Unwanted commits and changes removed from both local and remote history.  
- Verified that the remote branch now reflects the corrected state.  
### Key Learnings
- Understanding how `git reset --hard` reverts the repository to a previous commit.  
- Difference between `soft`, `mixed`, and `hard` resets.  
- Safely using `git push --force` to sync rewritten commit history.  
- Importance of caution when performing destructive Git operations.  
