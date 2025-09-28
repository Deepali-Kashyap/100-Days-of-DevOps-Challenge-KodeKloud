# Day 02 – Day 2: Temporary User Setup with Expiry
---

### Step 1: Server Access and Privilege Escalation
```bash
ssh steve@stapp02
sudo su -
```
- Connect securely to the server and switch to root for administrative tasks.
- `sudo su -` loads the full root environment.

### Step 2: Verify if User Exists
```bash
id siva
```
- Output if user does not exist:
```
id: siva: no such user
```
- Ensures no conflicts before creation.

### Step 3: Create User Account and Set Expiry
```bash
adduser siva
chage -E 2024-04-15 siva
chage -l siva
```
- Creates the user `siva` with home directory `/home/siva` and default shell `/bin/bash`.
- Sets account expiry to `Apr 15, 2024` and validates it.
- Lowercase username is used following standard protocol.

### Step 4: Importance, Best Practices, and Monitoring
- Temporary users do not linger in the system, reducing security risk.
- Follows compliance and security best practices.
- `chage` tool manages password and account expiration policies effectively.
- Monitor user activity:
```bash
lastlog -u siva
grep siva /var/log/auth.log
```
- Ensures proper lifecycle management of temporary accounts in production.

---

## Real-World Relevance
- Temporary access for contractors, interns, or automation scripts.
- Reduces risk of stale accounts.
- Demonstrates ability to manage secure Linux environments in production.

---
