# Day 05 – SELinux Installation and Configuration

---

## What is SELinux?
SELinux (Security-Enhanced Linux) is a security module that enforces access control policies on Linux systems to restrict programs and users to only the resources they are allowed to access. It helps strengthen system security by controlling permissions beyond traditional Linux user/group ownership.

---

## Step 1: Install Required SELinux Packages
```bash
sudo yum install -y selinux-policy selinux-policy-targeted policycoreutils
```
- Installs SELinux policy packages and management tools.
- `-y` automatically confirms installation.

## Step 2: Temporarily Disable SELinux
```bash
setenforce 0
```
- Disables SELinux enforcement without reboot.
- Useful during configuration or maintenance.

## Step 3: Permanently Disable SELinux
```bash
vim /etc/selinux/config
```
- Change the line:
```
SELINUX=enforcing
```
  to:
```
SELINUX=disabled
```
- Ensures SELinux remains disabled after the next reboot.
- No immediate reboot is required; a scheduled maintenance reboot is planned.

## Step 4: Verification
```bash
sestatus
```
- Check SELinux status.
- Expected output: `disabled` after reboot.

## Step 5: Importance and Best Practices
- SELinux enforces security policies on Linux systems, controlling access to files, processes, and resources.
- Disabling temporarily allows configuration changes without security restrictions.
- Permanent disablement is sometimes needed before implementing custom policies.

## Real-World Relevance
- Understanding SELinux is crucial for enterprise Linux environments.
- Proper management avoids unexpected permission denials in applications.
- Balances security enforcement with operational flexibility for system administrators and DevOps engineers.
