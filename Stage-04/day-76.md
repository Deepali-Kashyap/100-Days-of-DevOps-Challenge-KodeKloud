## Day 76: Jenkins Project Security

### Task Summary
Configure **project-level security in Jenkins** by installing required plugins, enabling matrix-based authorization, setting user permissions as per task requirements, and applying job-level access controls.

---

#### Step 1: Install Required Jenkins Plugins

Navigate to:
```
Manage Jenkins → Manage Plugins → Available
```

Search and install:
- ✅ Project Inheritance Plugin  
- ✅ Matrix Authorization Strategy Plugin  

After installation:
- 🔄 Restart Jenkins (when no jobs are running)

---

#### Step 2: Enable Matrix-Based Security

Navigate to:
```
Manage Jenkins → Configure Global Security
```

Configure:
- Authorization: **Matrix-based security**

Add users and assign permissions **as per task**:
- **Admin user**
  - Overall → Administer
- **Other users**
  - Overall → Read

Save configuration.

---

#### Step 3: Configure Project-Level Security

Open the required Jenkins job.

Navigate to:
```
Job → Configure
```

Enable:
- ☑ Enable project-based security

Under **Project-based Matrix Authorization Strategy**, assign permissions **as per task**:

Example:
- **Admin user**
  - Job → Configure
  - Job → Build
  - Job → Read
- **Non-admin user**
  - Job → Read

Save the job configuration.

---

### Final Result ✅

- ✔ Required plugins installed  
- ✔ Matrix-based security enabled  
- ✔ Global permissions configured correctly  
- ✔ Project-level security applied  
- ✔ Job access restricted as per task  
- ✔ Jenkins project security successfully enforced  
