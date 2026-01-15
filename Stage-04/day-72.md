## Day 72: Jenkins Parameterized Builds

### Task Summary
Create a **parameterized Jenkins Freestyle job** that accepts user input through **String** and **Choice** parameters and displays their values during build execution.

This task focuses on understanding how Jenkins parameters work and how they are accessed inside build steps.

---

#### Step 1: Login to Jenkins
- Click the **Jenkins** button on the top bar.
- Login using valid Jenkins credentials.

---

#### Step 2: Create the Parameterized Job
1. From the Jenkins Dashboard, click **New Item**.
2. Enter the job name:
   ```
   parameterized-job
   ```
3. Select **Freestyle project**.
4. Click **OK**.

---

#### Step 3: Add Parameters

#### Enable Parameterization
1. In the job configuration page, go to **General**.
2. Check ☑ **This project is parameterized**.

---

#### Add String Parameter: `Stage`
1. Click **Add Parameter → String Parameter**.
2. Fill in:
   - **Name:** Stage  
   - **Default Value:** Build  
   - **Description:** Stage name
3. Click **Add Parameter** to save.

---

#### Add Choice Parameter: `env`
1. Click **Add Parameter → Choice Parameter**.
2. Fill in:
   - **Name:** env  
   - **Choices** (one per line):
     ```
     Development
     Staging
     Production
     ```
   - **Description:** Environment selection

---

#### Step 4: Configure Shell Command
1. Scroll to the **Build** section.
2. Click **Add build step → Execute shell**.
3. Enter the following commands exactly:

```bash
echo "Stage: $Stage"
echo "Environment: $env"
```

These commands print the parameter values during the build.

---

#### Step 5: Save the Job
- Click **Save** to store the job configuration.

---

#### Step 6: Build the Job (Verification)
1. Open the **parameterized-job**.
2. Click **Build with Parameters**.
3. Set:
   - **Stage:** Build (leave default)
   - **env:** Staging
4. Click **Build**.

---

#### Step 7: Verify Build Output
1. Click the build number (e.g., **#1**).
2. Open **Console Output**.

#### Expected Output:
```
Stage: Build
Environment: Staging
```

---

#### Outcome & Key Learnings
- Created a **parameterized Jenkins job**
- Used **String** and **Choice** parameters
- Accessed parameters inside shell scripts
- Understood how user input affects build behavior
- Learned a core Jenkins concept used in real CI/CD pipelines
