## Day 12: Linux Network Services

**Challenge:** Troubleshoot and configure HTTP service and firewall rules to ensure a web application is accessible on port 8086.

---

### Steps Followed

1. Login to App Server 1
   ```bash
   ssh tony@stapp01
   sudo su -
   ```

2. Check the status of the HTTPD (Apache) service
   ```bash
   systemctl status httpd
   ```

3. Check which process is using port 8086
   ```bash
   netstat -lntp | grep 8086
   ```

4. Kill the conflicting process (example PID: 448)
   ```bash
   kill 448
   ```

5. Verify that port 8086 is now free
   ```bash
   netstat -lntp | grep 8086
   ```

6. Restart the HTTPD service
   ```bash
   systemctl restart httpd
   ```

7. Check firewall rules for port 8086
   ```bash
   iptables -L -n | grep 8086
   sudo iptables -L INPUT --line-numbers -n
   ```

8. Remove any incorrect rule for port 8086 (if necessary)
   ```bash
   sudo iptables -D INPUT -p tcp --dport 8086 -j ACCEPT
   ```

9. Add a new rule to allow incoming traffic on port 8086
   ```bash
   sudo iptables -I INPUT 5 -p tcp --dport 8086 -j ACCEPT
   ```

10. Test application accessibility
    ```bash
    curl http://stapp01:8086
    ```

---

### Outcome
- HTTPD service restarted successfully  
- Conflicting process on port 8086 resolved  
- Firewall rule correctly configured to allow port 8086  
- Web application accessible at http://stapp01:8086

---

### Key Learnings
- Managing and troubleshooting Linux network services  
- Using `netstat` to identify port conflicts  
- Understanding and modifying `iptables` firewall rules  
- Ensuring HTTP service accessibility on a custom port
