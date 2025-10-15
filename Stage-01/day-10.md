## 🧠 Day 10: Linux Bash Scripting — Website Backup Automation

### 📘 Project Overview

The production support team at **xFusionCorp Industries** required a Bash script to **automate website backups** from **App Server 2**.  
This task focuses on creating a script that compresses website files, stores the backup locally, and securely transfers it to the **Nautilus Backup Server** — all without requiring manual password entry during the transfer.


### 🖥️ Step-by-Step Implementation

**1. Login to App Server**
```
ssh steve@stapp02
sudo su -
```

**2. Navigate to the Scripts Directory**
```
cd /scripts
```

**3. Create the Backup Script**

```
vim blog_backup.sh
```

**Script Content**
```
#!/bin/bash

echo "Starting website backup..."

# Step 1: Create zip archive
zip -r /backup/xfusioncorp_blog.zip /var/www/html/blog
echo "Backup archive created successfully."

# Step 2: Copy the backup to Nautilus Backup Server
scp /backup/xfusioncorp_blog.zip clint@stbkp01:/backup/
echo "Backup archive copied successfully to Nautilus Backup Server."
```

**4. Setup SSH Key Authentication**

To ensure the script runs without password prompts:
```
ssh-keygen -t rsa
ssh-copy-id clint@stbkp01
```

**Now verify SSH access:**
```
ssh clint@stbkp01
```
⚡ **Make the Script Executable**
```
chmod +x /scripts/blog_backup.sh
```

**Run the Script**
```
bash /scripts/blog_backup.sh
```

**To confirm that the backup was successfully copied:**
```
ssh clint@stbkp01
cd /backup
ls -l
```
You should see:

xfusioncorp_blog.zip

<img width="600" height="629" alt="Screenshot from 2025-10-14 22-27-42" src="https://github.com/user-attachments/assets/438b4562-5425-4db7-b9eb-92677138392c" />

