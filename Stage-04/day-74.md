## Day 74:  Jenkins Database Backup Job

### Task Summary
Configure a **Jenkins Freestyle job** to automatically take a MySQL database backup from a **Database Server** and securely copy it to a **Backup Server** every 10 minutes using SSH.

---

#### Step 1: Install Required Jenkins Plugins

Navigate to:
```
Manage Jenkins → Plugins → Available
```

Install the following plugins:
- ✅ SSH Plugin  
- ✅ SSH Credentials Plugin  
- ✅ Publish Over SSH  

After installation:
- Click **Restart Jenkins** (when no jobs are running)
- Refresh the page if the UI freezes

---

#### Step 2: Add SSH Credentials

Navigate to:
```
Manage Jenkins → Credentials → System → Global Credentials → Add Credentials
```

Add credentials for:
- **Database Server**
- **Backup Server**

(Use appropriate usernames and passwords as per server configuration)

---

#### Step 3: Configure SSH Remote Hosts

Navigate to:
```
Manage Jenkins → Configure System
```

Scroll to **SSH remote hosts** and add:

#### Database Server
- Hostname: *(as provided)*
- Port: 22
- Credentials: Database Server credentials
- ✔ Test connection

#### Backup Server
- Hostname: *(as provided)*
- Port: 22
- Credentials: Backup Server credentials
- ✔ Test connection

Save the configuration.

---

#### Step 4: Create Jenkins Job

1. Click **New Item**
2. Job name: `database-backup`
3. Select **Freestyle project**
4. Click **OK**

---

#### Step 5: Configure Job Schedule

Under **Build Triggers**:
- ✔ Enable **Build periodically**
- Use the EXACT cron expression:
```
*/10 * * * *
```
➡ Runs every **10 minutes**

---

#### Step 6: Add Build Step (Core Logic)

Go to:
```
Build → Add build step → Execute shell script on remote host using SSH
```

- Select **SSH Site**: 👉 Database Server  
- Paste the following command **exactly**:

```bash
mysqldump -u kodekloud_roy -pasdfgdsd kodekloud_db01 > /tmp/db_$(date +%F).sql

sshpass -p '<BACKUP_SERVER_PASSWORD>' \
scp -o StrictHostKeyChecking=no \
/tmp/db_$(date +%F).sql \
clint@stbkp01.stratos.xfusioncorp.com:/home/clint/db_backups

rm -f /tmp/db_$(date +%F).sql
```

⚠️ Replace `<BACKUP_SERVER_PASSWORD>` with the actual backup server password.

Click **Save**.

---

#### Step 7: Run Job Manually (Initial Verification)

- Click **Build Now**
- Open **Console Output**

**Expected Result:**
```
Finished: SUCCESS
```

---

#### Step 8: Verify Backup on Backup Server

Login to the backup server:
```bash
ssh clint@stbkp01
ls -la /home/clint/db_backups
```

**Expected Output:**
```
db_YYYY-MM-DD.sql
```

---

#### Final Result ✅

- ✔ Jenkins job **database-backup** created successfully  
- ✔ MySQL database dump generated  
- ✔ Backup copied to backup server  
- ✔ Temporary files cleaned up  
- ✔ Job runs automatically every 10 minutes  
- ✔ Task requirements met exactly  
