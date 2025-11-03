## Day 32: Git Rebase

**Challenge:** Rebase a feature branch onto the latest `master` so the feature branch sits on top of current master commits, then push the rebased branch to remote.

---
### Steps Followed

1. Go to the repository
   ```bash
   cd /usr/src/kodekloudrepos/apps   # or /usr/src/kodekloudrepos/<your_project>
   ```

2. Make sure you’re on the feature branch
   ```bash
   git checkout feature
   ```

3. Fetch the latest commits from remote (ensure both branches are up to date)
   ```bash
   git fetch origin
   ```

4. Start the rebase onto master
   ```bash
   git rebase master
   ```
   - This takes commits on `feature` that are not in `master` and re-applies them on top of the latest `master`.
   
5. Push the rebased branch to remote (history rewritten — force push required)
   ```bash
   git push origin feature --force
   ```
   - Use `--force-with-lease` for a safer force-push that prevents overwriting others' updates:
     ```bash
     git push origin feature --force-with-lease
     ```

---

### Outcome
- `feature` branch successfully rebased on top of the latest `master`.  
- Local commit history rewritten so the feature branch reflects the newest base.  
- Rebasing completed and pushed to remote (force push), updating the remote branch to match local.
### Key Learnings
- `git rebase master` replays feature commits on top of `master` to create a linear history.  
- Handle merge conflicts during rebase with `git add` and `git rebase --continue`.  
- Use `git rebase --abort` to cancel a problematic rebase.  
- Prefer `--force-with-lease` over `--force` when pushing rewritten history to avoid accidentally overwriting others' work.
