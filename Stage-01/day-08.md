## Day 08 – Install Ansible with pip

**Challenge:** Install a specific version of Ansible (4.9.0) using Python’s package manager `pip`, verify the installation, and ensure Ansible is available system-wide.

---

### Steps Followed

1. Install Python pip
   ```bash
   sudo yum install python3-pip -y
   ```
   - Installs `pip3`, the Python package manager, required to install Ansible via pip.

2. Install Ansible 4.9.0 using pip
   ```bash
   sudo pip3 install ansible==4.9.0
   ```
   - Installs Ansible version `4.9.0` globally.

3. Verify Installation
   ```bash
   which ansible
   ```
   - Example output:
   ```bash
   /usr/local/bin/ansible
   ```
   - Confirms Ansible is installed globally and available for all users.

---

### Outcome
- Ansible 4.9.0 installed successfully via `pip3`.  
- `ansible` binary available at `/usr/local/bin/ansible` (system-wide).

---

### Key Learnings
- Installing specific versions of Python packages using `pip`.  
- Ensuring system-wide availability of command-line tools when installed with `sudo`.  
- Quick verification of installation using `which`.

---

### Screenshot
<img width="700" height="760" alt="Screenshot from 2025-09-28 22-29-55" src="https://github.com/user-attachments/assets/1bdfa04f-3b58-466f-97f6-854cf8067051" />
