## Day 68: Set Up Jenkins Server

### Task Summary
Set up a **Jenkins CI server** by installing required dependencies, configuring the Jenkins repository, installing Jenkins, starting the service, and completing the initial UI-based setup with an admin user.

---

#### Step 1: Install Java (Jenkins Prerequisite)

```bash
yum install -y java-17-openjdk
```

Jenkins requires Java to run. Java 17 is supported and recommended.

---

#### Step 2: Add Jenkins Repository

Add the official Jenkins repository:

```bash
wget -O /etc/yum.repos.d/jenkins.repo \
https://pkg.jenkins.io/redhat-stable/jenkins.repo
```

Import the Jenkins GPG key:

```bash
rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io.key
```

---

#### Step 3: Install and Start Jenkins

Install Jenkins:

```bash
yum install -y jenkins
```

Start and enable the Jenkins service:

```bash
systemctl start jenkins
systemctl enable jenkins
```

Verify service status:

```bash
systemctl status jenkins
```

---

#### Step 4: Complete Jenkins Initial Setup (UI)

1. Open Jenkins from the browser (via the Jenkins link or App button).
2. Unlock Jenkins using the initial admin password:

```bash
cat /var/lib/jenkins/secrets/initialAdminPassword
```

3. Create the admin user with the following details:

- **Username:** theadmin  
- **Password:** Adm!n321  
- **Full Name:** Ammar  
- **Email:** ammar@jenkins.stratos.xfusioncorp.com  

Complete the setup wizard and finalize Jenkins configuration.

---

#### Outcome & Key Learnings
- Installed Java and Jenkins successfully  
- Configured Jenkins repository securely  
- Started and enabled Jenkins as a system service  
- Completed Jenkins initial setup and admin user creation  
- Jenkins server is now ready for CI/CD pipelines
