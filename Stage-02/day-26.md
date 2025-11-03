## Day 26: Git Manage Remotes

**Challenge:** Configure and manage a new Git remote repository, commit new changes, and push updates to the newly added remote.

---
### Steps Followed

1. Login to the Storage Server  
   ```bash
   ssh natasha@ststor01
   ```

2. Navigate to the Repository Directory  
   ```bash
   cd /usr/src/kodekloudrepos/blog
   ```
   - Move into the existing Git repository.

3. Add a New Remote Repository  
   ```bash
   git remote add dev_blog /opt/xfusioncorp_blog.git
   ```
   - Adds a new remote named **dev_blog** pointing to `/opt/xfusioncorp_blog.git`.

4. Verify the Remote (Optional)  
   ```bash
   git remote -v
   ```
   - Confirms that the new remote **dev_blog** has been added successfully.

5. Copy the Required File into the Repository  
   ```bash
   cp /tmp/index.html .
   ```
   - Copies the `index.html` file from the temporary directory into the repository.

6. Stage and Commit the Change  
   ```bash
   git add index.html
   git commit -m "Add index.html file to master branch"
   ```
   - Stages and commits the new file to the **master** branch.

7. Push the Master Branch to the New Remote  
   ```bash
   git push dev_blog master
   ```
   - Pushes the committed changes from the local **master** branch to the **dev_blog** remote repository.

---
### Outcome
- New remote **dev_blog** successfully added to the Git repository.  
- File `index.html` added, committed, and pushed to the new remote repository.  
- Repository synchronization between local and remote verified.  
### Key Learnings
- Managing multiple Git remotes for collaboration and backup.  
- Adding, verifying, and pushing changes to custom remote repositories.  
- Using `git remote` commands effectively for repository configuration.  
- Understanding Git workflows across local and remote environments.
