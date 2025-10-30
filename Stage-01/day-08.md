## Day 08 – Install Ansible with pip

**Challenge:** Install a specific version of Ansible (4.9.0) using Python’s package manager `pip`, verify the installation, and understand why pip is preferred for certain environments.

---

### Step 1: Install Python pip
```bash
sudo yum install python3-pip -y
```
- Installs `pip3`, the Python package manager, required to install Ansible via pip.

---

### Step 2: Install Ansible 4.9.0 using pip
```bash
sudo pip3 install ansible==4.9.0
```
- Installs a specific version of Ansible (4.9.0) globally.  
- Using `sudo` ensures the installation is available system-wide, not just for a single user.

---

### Step 3: Verify Installation
```bash
which ansible
```
- Displays the binary path of Ansible.  
- Example output:
```bash
/usr/local/bin/ansible
```
This confirms Ansible is installed globally and available for all users.

---

### Step 4: Why Install via pip?
- Provides flexibility to install specific versions (e.g., `4.9.0`).  
- Easier and faster updates compared to OS package managers.  
- Commonly used in Python-based automation and CI/CD environments.

---

### Real-World Relevance
- Ansible is a powerful automation and configuration management tool.  
- Installing via pip ensures teams can match exact versions across environments.  
- This consistency is critical in DevOps pipelines and for debugging version-specific issues.

---

### Screenshot
<img width="700" height="760" alt="Screenshot from 2025-09-28 22-29-55" src="https://github.com/user-attachments/assets/1bdfa04f-3b58-466f-97f6-854cf8067051" />
