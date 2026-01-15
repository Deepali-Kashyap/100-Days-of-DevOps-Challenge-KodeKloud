## Day 70: Configure Jenkins User Access

### Task Summary
Configure **role-based access control** in Jenkins by creating a new user, installing the required authorization plugin, and assigning appropriate permissions to both admin and non-admin users.

---

### Steps Performed (UI-Based)

#### Step 1: Create a New Jenkins User
1. Log in to the Jenkins dashboard as **admin**.
2. Navigate to:
   ```
   Manage Jenkins → Manage Users → Create User
   ```
3. Create a new user with the required details.
4. Save the user.

---

#### Step 2: Install Matrix Authorization Plugin
1. Navigate to:
   ```
   Manage Jenkins → Manage Plugins
   ```
2. Search for and install:
   - **Matrix Authorization Strategy Plugin**
3. Restart Jenkins after plugin installation.

---

#### Step 3: Enable Matrix-Based Security
1. Go to:
   ```
   Manage Jenkins → Configure Global Security
   ```
2. Under **Authorization**, select:
   ```
   Matrix-based security
   ```

---

#### Step 4: Assign Global Permissions

##### Admin User Permissions
- Granted **Overall → Administer** permission to the admin user.

##### New User Permissions
- Granted **Overall → Read** permission to the newly created user.

This ensures the new user can access Jenkins in read-only mode.

---

#### Step 5: Configure Job-Level Permissions
1. Scroll to **Job / Project Permissions** in Matrix settings.
2. Grant the new user:
   - **Job → Read**
3. Save the configuration.

This allows the new user to view existing Jenkins jobs without modifying them.

---

### Verification
- Admin user has full administrative access.
- New user can:
  - Log in successfully
  - View Jenkins dashboard
  - Read existing jobs
- New user cannot:
  - Create, modify, or delete jobs
  - Change Jenkins configuration

---

### Outcome & Key Learnings
- Created and managed Jenkins users via UI  
- Installed and configured **Matrix Authorization Strategy**  
- Implemented least-privilege access control  
- Learned how to manage global and job-level permissions in Jenkins  
- Improved Jenkins security and user access management
