## Day 78: Jenkins Conditional Pipeline

### Task Summary
Configure a **parameterized Jenkins Pipeline** that deploys a web application from different Git branches (`master` or `feature`) based on user input. The pipeline runs on a **storage server configured as a Jenkins agent** and conditionally executes Git commands.

---

#### Step 1: Prepare Storage Server (Agent Node)

Login to the storage server and run:

```bash
sudo yum install -y java-17-openjdk
sudo chown -R natasha:natasha /var/www/html
```

> Java is required for the Jenkins agent, and permissions ensure Jenkins can deploy files.

---

#### Step 2: Login to Jenkins

Click the **Jenkins** button from the top bar and log in.

---

#### Step 3: Install Required Plugins (If Missing)

Navigate to:
```
Manage Jenkins → Manage Plugins → Available
```

Ensure the following plugins are installed:
- ✅ Pipeline
- ✅ Git
- ✅ SSH Agent

Restart Jenkins if any plugin is newly installed.

---

#### Step 4: Add Jenkins Slave Node (Storage Server)

Go to:
```
Manage Jenkins → Manage Nodes and Clouds → New Node
```

##### Node Configuration

| Field                  | Value                          |
|------------------------|--------------------------------|
| Node name              | Storage Server                 |
| Type                   | Permanent Agent                |
| Remote root directory  | /var/www/html                  |
| Labels                 | ststor01                       |
| Usage                  | Use this node as much as possible |
| Launch method          | Launch agent via SSH           |

Provide **Storage Server SSH credentials**, then **Save**.

✅ Node status must show **Connected / Online**.

---

#### Step 5: Create Jenkins Pipeline Job

Click:
```
New Item
```

Job name:
```
nautilus-webapp-job
```

Select:
- ✅ Pipeline

Click **OK**.

---

#### Step 6: Add Job Parameter

In job configuration:

- ✔ Check **This project is parameterized**
- Click **Add Parameter → String Parameter**

Fill in:
- **Name:** BRANCH
- **Default Value:** master
- **Description:** Branch to deploy (master or feature)

---

#### Step 7: Configure Pipeline Script (MOST IMPORTANT)

Scroll to:
```
Pipeline → Definition
```

Select:
```
Pipeline script
```

Paste **EXACTLY** this script:

```groovy
pipeline {
    agent {
        label 'ststor01'
    }

    parameters {
        string(name: 'BRANCH', defaultValue: 'master', description: 'Branch to deploy')
    }

    stages {
        stage('Deploy') {
            steps {
                sh '''
                cd /var/www/html

                if [ "$BRANCH" = "master" ]; then
                    git checkout master
                    git pull origin master
                elif [ "$BRANCH" = "feature" ]; then
                    git checkout feature
                    git pull origin feature
                else
                    echo "Invalid branch name: $BRANCH"
                    exit 1
                fi
                '''
            }
        }
    }
}
```

📌 Notes:
- Stage name must be exactly **Deploy**
- Pipeline runs on **storage server (ststor01)**
- Repository must already exist in `/var/www/html`

Click **Save**.

---

#### Step 8: Run Pipeline (Testing)

Click:
```
Build with Parameters
```

##### Test Case 1
- **BRANCH:** master  
- Click **Build**

##### Test Case 2
- **BRANCH:** feature  
- Click **Build**

### Expected Result
Both builds should show:
```
Stage: Deploy → SUCCESS
```

---

#### Final Result ✅
- ✔ Conditional Jenkins Pipeline created
- ✔ Parameter-based branch deployment implemented
- ✔ Storage server used as Jenkins agent
- ✔ Git branches deployed successfully
- ✔ Task completed as per requirements
