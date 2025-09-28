# Day 03 – Secure Root SSH Access
---

## Step 1: Server Access and Privilege Escalation
```bash
ssh steve@stapp01
sudo su -
```
- Connect securely to the server and switch to root for administrative tasks.
- `sudo su -` loads the full root environment.

## Step 2: Verify Current SSH Root Login Setting
```bash
grep PermitRootLogin /etc/ssh/sshd_config /etc/ssh/sshd_config.d/*.conf
```
- Check if root login is enabled or disabled.
- Helps identify current SSH security posture.

## Step 3: Update SSH Configuration to Disable Root Login
```bash
sudo vim /etc/ssh/sshd_config
```
- Locate the line `#PermitRootLogin prohibit-password` and change it to:
```
PermitRootLogin no
```
- Save and exit.
- This prevents root from logging in directly via SSH.

## Step 4: Restart SSH Service
```bash
sudo systemctl restart sshd
```
- Apply configuration changes without rebooting.
- Ensures new SSH rules are in effect immediately.

## Step 5: Verification
```bash
grep PermitRootLogin /etc/ssh/sshd_config /etc/ssh/sshd_config.d/*.conf
```
- Confirm that `PermitRootLogin no` is set.
- SSH attempts as root should now fail.

## Step 6: Importance, Best Practices, and Monitoring
- Disabling root SSH login reduces the attack surface.
- Follows security best practices for enterprise servers.
- Use sudo with normal users for administrative tasks instead.
- Monitor `/var/log/auth.log` for failed login attempts:
```bash
grep sshd /var/log/auth.log
```
- Ensures SSH access is properly secured and audited.

---

## Real-World Relevance
- Prevents unauthorized root access to production servers.
- Encourages principle of least privilege for user accounts.
- Essential step in securing Linux servers for DevOps pipelines and enterprise environments.
