## Day 14: Linux Process Troubleshooting

**Challenge:** Troubleshoot Apache (HTTPD) service issues when the configured port is already in use, identify and terminate the conflicting process, and ensure Apache runs on the correct port (3001).

---

### Steps Followed

1. SSH into Each App Host
   ```bash
   ssh tony@stapp01
   ssh steve@stapp02
   ssh banner@stapp03
   ```
   - Connected to each application server from the jump host for troubleshooting.

2. Check if Apache Is Installed and Running
   ```bash
   sudo systemctl status httpd
   ```
   - Error observed: `Address already in use`

3. Confirm Which Port Apache Is Configured to Use
   ```bash
   sudo grep -R "Listen" /etc/httpd/conf/httpd.conf /etc/httpd/conf.d/
   ```
   - Expected output:  
     ```
     Listen 3001
     ```
   - ✅ If it says `3001` → configuration is correct.  
   - ❌ If it says `80` → update the configuration in `/etc/httpd/conf/httpd.conf` to:
     ```
     Listen 3001
     ```

4. Check What Process Is Using Port 3001
   ```bash
   sudo netstat -tulnp | grep 3001
   ```
   - Identify the process ID (PID) occupying port 3001, then terminate it:
   ```bash
   sudo kill -9 <PID>
   ```

5. Restart Apache Service
   ```bash
   sudo systemctl restart httpd
   sudo systemctl status httpd
   ```
   - Verifies Apache restarts successfully without conflicts.

6. Verify Apache Is Listening on Port 3001
   ```bash
   sudo netstat -tulnp | grep httpd
   ```

7. Test Locally
   ```bash
   curl http://localhost:3001
   ```
   - Confirms the web service is reachable on the configured port.

---

### Outcome
- Conflicting process identified and terminated.  
- Apache configured to use port `3001`.  
- HTTPD service restarted successfully and confirmed running on the correct port.  
- Verified accessibility using `curl` locally.

### Key Learnings
- Troubleshooting “Address already in use” errors in Linux.  
- Identifying and killing processes occupying specific ports.  
- Modifying Apache port configuration in `httpd.conf`.  
- Validating web service accessibility using `netstat` and `curl`.
