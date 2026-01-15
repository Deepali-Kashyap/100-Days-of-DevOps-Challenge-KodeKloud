## Day 69: Install Jenkins Plugins

### Task Summary
Install required Jenkins plugins using the **Jenkins UI** to enable Git and GitLab integration, followed by a Jenkins restart to apply changes.

---

#### Step 1: Open Jenkins Dashboard
- Access Jenkins via the browser.
- Log in using the admin credentials.

---

#### Step 2: Install Required Plugins
1. Navigate to:
   ```
   Manage Jenkins → Manage Plugins
   ```
2. Open the **Available** tab.
3. Search and install the following plugins:
   - **Git Plugin**
   - **GitLab Plugin**
4. Select **Install without restart** (or install and restart if prompted).

---

#### Step 3: Restart Jenkins
To ensure all plugins load correctly, restart Jenkins:

- From UI (if prompted), or
- Using the restart option:
  ```
  Manage Jenkins → Reload Configuration from Disk
  ```
  or full service restart if required.

---

### Outcome & Key Learnings
- Successfully installed **Git** and **GitLab** plugins  
- Enabled Jenkins integration with Git-based repositories  
- Restarted Jenkins to apply plugin changes  
- Jenkins is now ready for SCM-based CI/CD jobs
