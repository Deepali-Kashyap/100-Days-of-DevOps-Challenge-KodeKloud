## Day 71: Configure Jenkins Job for Package Installation

### Task Summary
Create a **parameterized Jenkins Freestyle job** that installs Linux packages dynamically on the **storage server** using a user-provided package name at build time.

This task demonstrates Jenkins job creation, parameter usage, and remote command execution via SSH.

---

#### Step 1: Login to Jenkins UI
- Open Jenkins from the top bar.

## Step 2: Create a New Jenkins Job
1. From the Jenkins Dashboard, click **New Item**.
2. Enter the job name:
   ```
   install-packages
   ```
3. Select **Freestyle project**.
4. Click **OK**.

---

#### Step 3: Add String Parameter `PACKAGE`
1. In the job configuration page, go to **General**.
2. Check ☑ **This project is parameterized**.
3. Click **Add Parameter → String Parameter**.
4. Fill in the details:
   - **Name:** PACKAGE  
   - **Default Value:** (leave empty)  
   - **Description:** Package name to install
5. Save the parameter.

---

#### Step 4: Configure Job to Install Package on Storage Server

#### Assumption
- Jenkins server has SSH access to the storage server.
- Passwordless or root SSH access is already configured.

#### Add Build Step
1. Scroll to **Build** section.
2. Click **Add build step → Execute shell**.
3. Paste the following script:

```bash
ssh root@storage <<EOF
yum install -y $PACKAGE
EOF
```

✔ Uses the `PACKAGE` parameter dynamically  
❌ No hardcoded package names

---

#### Step 5: Save the Job
- Click **Save** to store the job configuration.

---

#### Step 6: Test the Job (Verification)
1. Open the **install-packages** job.
2. Click **Build with Parameters**.
3. Enter a package name, for example:
   ```
   PACKAGE = httpd
   ```
4. Start the build and monitor the console output.

Expected:
- Jenkins connects to the storage server
- Installs the specified package successfully

---

#### Outcome & Key Learnings
- Created a **Freestyle Jenkins job**
- Used **string parameters** for dynamic input
- Executed remote commands using **SSH**
- Automated package installation through Jenkins
- Learned how Jenkins can be used for basic system automation tasks
