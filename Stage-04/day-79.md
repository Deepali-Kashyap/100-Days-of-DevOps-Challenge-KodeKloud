## Day 79: Jenkins Deployment Job

### Task Summary
Create a Jenkins **Freestyle deployment job** that automatically deploys website files from a Git repository to a storage server whenever changes are pushed. The job uses **Poll SCM**, **Git credentials**, and **secret text credentials** for secure deployment.

---

#### Step 1: Prepare App Servers

Login to **all App Servers** and install Apache:

```bash
sudo yum install -y httpd
```

Edit Apache configuration and change the listen port from **80 to 8080**:

```bash
sudo vi /etc/httpd/conf/httpd.conf
```

Update:
```conf
Listen 8080
```

Start and enable Apache:

```bash
sudo systemctl start httpd
sudo systemctl enable httpd
```

---

#### Step 2: Prepare Storage Server

SSH into the storage server:

```bash
ssh natasha@ststor01
```

Change ownership of the web directory:

```bash
sudo chown -R sarah:sarah /var/www/html
```

---

#### Step 3: Access Jenkins UI & Install Plugins

Navigate to:
```
Manage Jenkins → Manage Plugins → Available
```

Install:
- ✅ Credentials Plugin
- ✅ SSH Plugin
- ✅ Git Plugin

Restart Jenkins after installation.

---

#### Step 4: Configure Jenkins Credentials

Go to:
```
Manage Jenkins → Credentials → System → Global credentials
```

###### 4.1 Add Username/Password Credentials (Git User)

- Kind: Username with password  
- Username: sarah  
- Password: `<Git_User_Password>`  
- ID: sarah-git-creds  

Save.

##### 4.2 Add Secret Text Credential

- Kind: Secret Text  
- Secret: `<Git_User_Password>`  
- ID: sarah-pass-secret  

Save.

---

#### Step 5: Create Jenkins Deployment Job

Go to:
```
New Item
```

- Job name: **deployment-job**
- Type: **Freestyle project**
- Click **OK**

---

#### Step 6: Configure Source Code Management

Under **Source Code Management**:
- Select **Git**
- Repository URL: `<Git_Repository_URL>`
- Credentials: **sarah-git-creds**

Enable **Poll SCM**:
```cron
* * * * *
```
➡️ Checks repository every minute for changes.

---

#### Step 7: Configure Environment Variable (Secret Text)

Under **Build Environment**:
- ✔ Check **Use secret text(s) or file(s)**
- Add **Secret Text**
- Credentials: `sarah-pass-secret`
- Variable: `SARAH_PASS`

---

#### Step 8: Configure Build Step (Deployment)

Add build step:
```
Execute shell
```

Paste:
```bash
sshpass -p "$SARAH_PASS" \
scp -o StrictHostKeyChecking=no -r * \
sarah@ststor01:/var/www/html
```

Click **Save**.

---

#### Step 9: Trigger Deployment via Git Push

SSH into storage server and update repo files:

```bash
ssh sarah@ststor01
cd /home/sarah/web
vi index.html
git add .
git commit -m "Updated website content"
git push origin master
```

---

#### Step 10: Verify Deployment

- Jenkins job should trigger automatically via **Poll SCM**
- Check job **Build History**
- Console Output should show **SUCCESS**


#### Final Result ✅
- ✔ Jenkins deployment job created
- ✔ Git repository monitored using Poll SCM
- ✔ Secure credentials used (username/password + secret text)
- ✔ Automatic deployment to storage server
- ✔ Website updates deployed successfully
