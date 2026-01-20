# Day 80: Jenkins Chained Builds

## Concept Overview

**Chained Builds** in Jenkins mean connecting multiple jobs so they run **in sequence**.  
When one job completes **successfully (stable)**, it automatically triggers the next job.

```
Job A  →  Job B  →  Job C
```

In this task:

- **Upstream Job**: `nautilus-app-deployment`
- **Downstream Job**: `manage-services`

➡️ The downstream job runs **only if** the upstream job finishes successfully.

---

## Definitions

### Upstream Job
- Runs first
- Pulls latest code from Git
- Deploys code to the shared storage server
- Triggers downstream jobs on success

### Downstream Job
- Runs after upstream job
- Triggered automatically
- Restarts Apache service on **all App Servers**
- Executes **only if upstream job is stable**

---

## Task Objective

Set up a **Continuous Deployment (CD) pipeline** using Jenkins chained builds where:

1. Code is updated on a shared storage server
2. Apache service is restarted on all App Servers
3. Restart happens **only after successful code deployment**

---

## Step 1: Access Jenkins UI

- Open Jenkins from the top bar
- Login with admin credentials

---

## Step 2: Install Required Plugin

Navigate to:

```
Manage Jenkins → Manage Plugins → Available
```

Install:
- ✅ Publish Over SSH Plugin

Restart Jenkins after installation and verify the plugin is active.

---

## Step 3: Configure SSH Servers (Publish Over SSH)

Go to:

```
Manage Jenkins → Configure System
```

Scroll down to **Publish over SSH** section.

Click **Add** and configure the following servers:

### 1️⃣ Storage Server
- Hostname: `ststor01`
- Username: `<storage-user>`
- Remote directory: `/var/www/html`

### 2️⃣ App Server 1
- Hostname: `stapp01`
- Username: `<app-user>`

### 3️⃣ App Server 2
- Hostname: `stapp02`
- Username: `<app-user>`

### 4️⃣ App Server 3
- Hostname: `stapp03`
- Username: `<app-user>`

✔ Test connections for all servers  
✔ Save configuration

---

## Jenkins Job Flow (Chained Build)

```
nautilus-app-deployment (Upstream)
        |
        |  (Trigger only if SUCCESS)
        ↓
manage-services (Downstream)
```

- **Upstream Job**
  - Pulls code from Git
  - Deploys to shared storage

- **Downstream Job**
  - Restarts Apache on all App Servers
  - Triggered only when upstream job is stable

### Step 4: Create the Upstream Job  
**Job Name:** `nautilus-app-deployment`

1. Open **Jenkins Dashboard → New Item**
2. Enter job name:
   ```
   nautilus-app-deployment
   ```
3. Select **Freestyle project** → Click **OK**

#### Configure Build Step
- Go to **Build**
- Click **Add build step**
- Select **Send files or execute commands over SSH**
- Choose SSH server:
  ```
  ststor01
  ```

#### Execute Command
Pull the latest code from the master branch:
```bash
cd /var/www/html
git pull origin master
```

#### Configure Post-build Action
- Scroll to **Post-build Actions**
- Select **Build other projects**
- Project to build:
  ```
  manage-services
  ```
- Trigger condition:
  - ✅ **Trigger only if build is stable** (first option)

Save the job.

---

### Step 5: Create the Downstream Job  
**Job Name:** `manage-services`

1. Go to **New Item**
2. Enter job name:
   ```
   manage-services
   ```
3. Select **Freestyle project** → Click **OK**

---

### Step 6: Parameterize the Downstream Job (IMPORTANT)

Enable:
- ☑ **This project is parameterized**

Add **Password Parameters** for each App Server:

| Parameter Name | Description |
|---------------|------------|
| STAPP01_PASS  | Password for App Server 1 |
| STAPP02_PASS  | Password for App Server 2 |
| STAPP03_PASS  | Password for App Server 3 |

➡️ Enter the respective server passwords as default values.

---

### Step 7: Configure Build Steps (Restart Apache)

Go to **Build → Add build step → Send files or execute commands over SSH**

#### App Server 1 (stapp01)
```bash
echo $STAPP01_PASS | sudo -S systemctl restart httpd
```

#### App Server 2 (stapp02)
```bash
echo $STAPP02_PASS | sudo -S systemctl restart httpd
```

#### App Server 3 (stapp03)
```bash
echo $STAPP03_PASS | sudo -S systemctl restart httpd
```

📌 **Note:**  
The `-S` flag tells `sudo` to read the password from standard input (via the pipe) instead of prompting interactively.  
Passwords are passed securely using Jenkins password parameters, not hardcoded.

Save the job.

---

### Step 8: Run the Chained Build

1. Go to **nautilus-app-deployment**
2. Click **Build Now**

### Expected Flow
```
nautilus-app-deployment  (SUCCESS)
          ↓
manage-services          (Apache restarted on all App Servers)
```

---

### Final Result ✅
- Code is updated on the storage server
- Apache restarts automatically on all app servers
- Downstream job triggers **only if** upstream job is stable
- Jenkins chained build configured successfully

     

   
 
