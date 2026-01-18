## Day 73: Jenkins Scheduled Jobs

### Task Summary
Create a Jenkins Freestyle job to **periodically copy Apache logs** from App Server 1 to a directory on the Storage Server using SSH. The job should run every 7 minutes.

---

### Step 1: Verify Servers and Logs

#### App Server 1
```bash
ssh tony@STapp01
ls /var/log/httpd/
```
**Expected Output:**
```
access_log
error_log
```

#### Storage Server
```bash
ssh natasha@STstor01
ls /usr/src/itadmin
```
Initially, this directory should be empty.

---

### Step 2: Install Required Jenkins Plugins
Navigate to:
```
Manage Jenkins → Manage Plugins → Available
```
Install the following:
- SSH plugin ✅
- Credentials plugin ✅
- Publish Over SSH ✅

Restart Jenkins after installation.

---

### Step 3: Add SSH Credentials in Jenkins
Navigate to:
```
Manage Jenkins → Credentials → System → Global credentials → Add Credentials
```

#### App Server Credentials
- **Username:** tony  
- **Password:** `<AppServerPassword>`  
- **ID:** app-server-1

#### Storage Server Credentials
- **Username:** natasha  
- **Password:** `<StorageServerPassword>`  
- **ID:** storage-server

---

### Step 4: Configure SSH Remote Hosts
Navigate to:
```
Manage Jenkins → Configure System
```

#### App Server 1
- **Hostname:** STapp01  
- **Port:** 22  
- **Credentials:** app-server-1  
- ✔ Check connection (should succeed)

#### Storage Server
- **Hostname:** STstor01  
- **Port:** 22  
- **Credentials:** storage-server  
- ✔ Check connection

Save configuration.

---

### Step 5: Create Jenkins Job
1. Go to **New Item**  
2. Job name: `copy-logs`  
3. Select **Freestyle Project**  
4. Click **OK**

---

### Step 6: Configure Periodic Build
Under **Build Triggers**:
- ✔ Check **Build periodically**  
- Cron expression:
```
*/7 * * * *
```
➡ Runs every 7 minutes

---

### Step 7: Configure Log Copy Command
Under **Build → Add build step → Execute shell script on remote host using SSH**, enter:
```bash
sshpass -p '<storage_password>' \
scp -o StrictHostKeyChecking=no \
/var/log/httpd/* \
natasha@STstor01:/usr/src/itadmin
```
⚠️ Note: This uses `sshpass` for quick setup. A more secure approach is **SSH key-based authentication**.

---

### Step 8: Build & Verify
1. Trigger the build: **Build Now**  
2. Check **Console Output**  

**Expected Output:**
```
Finished: SUCCESS
```

---

### Step 9: Validate Logs on Storage Server
```bash
ls /usr/src/itadmin
```
**Expected Output:**
```
access_log
error_log
```

---

### Outcome & Key Learnings
- Successfully created a **scheduled Jenkins job** to automate log copying.  
- Learned to use **SSH credentials** and configure **remote hosts** in Jenkins.  
- Cron-based periodic builds allow **automated repetitive tasks**.  
- Verified logs are correctly transferred from App Server to Storage Server.
