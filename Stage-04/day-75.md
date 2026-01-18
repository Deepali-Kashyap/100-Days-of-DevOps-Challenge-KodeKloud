## Day 75: Jenkins Slave Nodes 

### Task Summary
Set up **Jenkins slave (agent) nodes** using SSH by installing required plugins, configuring credentials, installing Java on all application servers, and registering nodes in Jenkins as per instructions.

---

#### Step 1: Install Required Jenkins Plugins

Navigate to:
```
Manage Jenkins → Manage Plugins → Available
```

Install:
- ✅ SSH Plugin

After installation:
- Restart Jenkins (when no jobs are running)

---

#### Step 2: Add SSH Credentials for All Servers

Navigate to:
```
Manage Jenkins → Credentials → System → Global Credentials → Add Credentials
```

Add credentials for **all three servers** (e.g. App Server 1, App Server 2, App Server 3):

For each server:
- Kind: Username with password
- Username: (as provided)
- Password: (as provided)
- ID: meaningful ID (e.g. `app-server-1`, `app-server-2`, `app-server-3`)

Save credentials.

---

#### Step 3: Configure SSH Remote Hosts

Navigate to:
```
Manage Jenkins → Configure System
```

Scroll to **SSH remote hosts** and add entries for **all three servers**:

For each server:
- Hostname: Server hostname
- Port: 22
- Credentials: Corresponding server credentials
- ✔ Test connection (must succeed)

Save the configuration.

---

#### Step 4: Install Java on All Application Servers

Jenkins agents require Java to run.

Login to each application server and install Java:

```bash
sudo yum install -y java-17-openjdk
```

Verify installation:
```bash
java -version
```

Ensure Java is installed successfully on **all app servers**.

---

#### Step 5: Add Jenkins Slave Nodes

Navigate to:
```
Manage Jenkins → Manage Nodes and Clouds → New Node
```

Create nodes **as per instructions**.

For each node:

- Node name: (as instructed)
- Type: Permanent Agent
- Number of executors: 1
- Remote root directory: `/home/jenkins`
- Labels: (as required)
- Usage: Use this node as much as possible
- Launch method: Launch agents via SSH
- Host: Corresponding app server hostname
- Credentials: Matching SSH credentials
- Host Key Verification Strategy: Non verifying Verification Strategy

Save the node.

---

#### Step 6: Verify Node Status

Navigate to:
```
Manage Jenkins → Manage Nodes and Clouds
```

Expected:
- All nodes show **Connected**
- No red or offline indicators

Click a node → **Log** to confirm successful agent launch.

---

#### Final Result ✅

- ✔ SSH plugin installed  
- ✔ Credentials added for all three servers  
- ✔ SSH remote hosts configured  
- ✔ Java installed on all app servers  
- ✔ Jenkins slave nodes added successfully  
- ✔ All nodes connected and ready for builds  

---

<img width="1920" height="626" alt="image" src="https://github.com/user-attachments/assets/01efce1c-8b95-40a2-be30-fb45aec730f3" />
