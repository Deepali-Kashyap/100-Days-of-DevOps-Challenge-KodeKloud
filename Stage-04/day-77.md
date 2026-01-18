## Day 77: Jenkins Deploy Pipeline

### Task Summary
Create a **Jenkins Pipeline job** that deploys a web application by pulling the latest code from Git on a **storage server acting as a Jenkins agent (slave node)**. The deployment is performed using a Jenkins Pipeline running on the storage server via SSH.

---

#### Step 1: Install Required Jenkins Plugins

Navigate to:
```
Manage Jenkins → Manage Plugins → Available
```

Install the following plugins:
- ✅ Git Plugin
- ✅ SSH Plugin
- ✅ SSH Build Agents Plugin (or equivalent SSH agent support)
- ✅ Pipeline Plugin

🔄 Restart Jenkins after plugin installation.

---

#### Step 2: Prepare Storage Server (Agent Node)

##### Install Java (Required for Jenkins Agent)
```bash
sudo yum install -y java-17-openjdk
```

##### Fix Permissions for Web Directory
Ensure Jenkins user can deploy files:
```bash
sudo chown -R natasha:natasha /var/www/html
```

---

#### Step 3: Configure Jenkins Credentials

Navigate to:
```
Manage Jenkins → Credentials → System → Global credentials → Add Credentials
```

Add credentials for **Storage Server**:

---

#### Step 4: Add Jenkins Node (Storage Server as Agent)

Navigate to:
```
Manage Jenkins → New Node
```

Configure:
- Node name: `ststor01`
- Type: Permanent Agent

Node settings:
- Remote root directory: `/home/natasha`
- Labels: `ststor01`
- Usage: Use this node as much as possible
- Launch method: Launch agents via SSH
- Host: STstor01
- Credentials: storage-server

Save and **Launch Agent**.

✅ Ensure agent status is **Connected**.

---

#### Step 5: Create Jenkins Pipeline Job

Click:
```
New Item
```

Job name:
```
devops-webapp-job
```

Select:
- ✅ Pipeline  
❌ Do NOT select Multibranch Pipeline

Click **OK**.

---

## Step 6: Configure Pipeline Script (MOST IMPORTANT)

Scroll to:
```
Pipeline → Definition
```

Choose:
```
Pipeline script
```

Paste **EXACT** pipeline code:
```groovy
pipeline {
    agent {
        label 'ststor01'
    }

    stages {
        stage('Deploy') {
            steps {
                sh '''
                cd /var/www/html
                git pull origin main || git pull origin master
                '''
            }
        }
    }
}
```

##### Notes
- Stage name must be exactly **Deploy** (case-sensitive)
- Pipeline runs on **storage server**
- Repository must already be cloned in `/var/www/html`
- `git pull` updates website content automatically

Click **Save**.

---

#### Step 7: Run the Pipeline

Click:
```
Build Now
```

#### Final Result ✅
- ✔ Jenkins Pipeline job created
- ✔ Storage server configured as Jenkins agent
- ✔ Git-based deployment automated
- ✔ Web content updated using `git pull`
- ✔ Pipeline executed successfully on agent node

---
```
