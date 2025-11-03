## Day 34: Git Hook

**Challenge:** Implement a Git hook to automatically tag a new release after merging branches in the repository.

---

## Steps Followed

1. Navigate to the Repository Directory  
   ```bash
   cd /usr/src
   ```

2. Verify and Switch Branches  
   ```bash
   git branch
   git checkout master
   git merge feature
   ```
   - Ensures that the `feature` branch changes are merged into the `master` branch.

3. Create and Configure the Git Hook  
   ```bash
   sudo vi /opt/blog.git/hooks/post-update
   ```
   Add the following script inside:
   ```bash
   #!/bin/bash
   tag=release-$(date '+%Y-%m-%d')
   git tag $tag
   ```

4. Make the Hook Executable  
   ```bash
   chmod +x /opt/blog.git/hooks/post-update
   ```
   - This ensures the post-update hook runs automatically after updates to the repository.

5. Push Changes and Verify  
   ```bash
   git push
   git log
   ```
   - The hook automatically creates a tag (e.g., `release-2025-11-03`) after a successful push.  
   - Use `git log` to confirm that the tag has been applied.

---

### Outcome
- Successfully merged `feature` branch into `master`.  
- Configured a post-update Git hook to automatically tag each new release.  
- Verified that the release tag was created and logged correctly.
### Key Learnings
- Understanding Git hooks and their automation capabilities.  
- Using `post-update` hooks to trigger automated actions post push.  
- Automating version tagging for consistent release management.  
- Enhancing CI/CD processes through custom Git workflows.
