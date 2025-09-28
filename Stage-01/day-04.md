# Day 04 – Script Execution Permissions

---

## Step 1: Server Access and Privilege Escalation
```bash
ssh steve@stapp02
sudo su -
```
- Connect securely to the server and switch to root.
- `sudo su -` ensures full root environment for administrative tasks.

## Step 2: Locate the Script
```bash
ls -l /tmp/xfusioncorp.sh
```
- Verify that the script exists and check its current permissions.

## Step 3: Grant Execute Permissions to All Users
```bash
chmod +x /tmp/xfusioncorp.sh
```
- `+x` adds execute permission.
- Makes the script executable for owner, group, and others.

## Step 4: Verification
```bash
ls -l /tmp/xfusioncorp.sh
```
- Ensure the permission column shows `-rwxr-xr-x` or similar, indicating executable access for all users.

## Step 5: Importance and Best Practices
- Ensures scripts required for automated tasks can run without permission errors.
- Using `chmod +x` is a standard way to provide execution rights safely.
- Always verify the script path and permissions before execution.

## Real-World Relevance
- Common in DevOps pipelines to allow deployment or monitoring scripts to run.
- Prevents runtime failures due to permission issues.
- Supports automation and ensures smooth operations in production environments.
