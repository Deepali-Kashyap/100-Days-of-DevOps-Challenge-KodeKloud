## Day 11: Install and Configure Tomcat Server

**Challenge:** Install and configure an Apache Tomcat server, deploy a sample ROOT.war file, and verify the application is running.

---

### Steps Followed

1. Navigate to /tmp directory and verify the WAR file
   ```bash
   cd /tmp
   ls
   # Check for ROOT.war file
   ```

2. Copy the WAR file to the target server
   ```bash
   scp /tmp/ROOT.war steve@stapp02:/tmp
   ```

3. SSH into the target server
   ```bash
   ssh steve@stapp02
   ls /tmp
   # Confirm ROOT.war file exists
   ```

4. Check Tomcat service status
   ```bash
   sudo systemctl status tomcat
   # Output: service not found
   ```

5. Install Tomcat
   ```bash
   sudo yum install tomcat -y
   ```

6. Check Tomcat configuration
   ```bash
   cd /etc/tomcat/
   cat server.xml
   ```

7. Modify Tomcat port number (default: 8080 → change to 6000)
   ```bash
   sudo vim server.xml
   # Update the Connector port to 6000
   # <Connector port="6000" protocol="HTTP/1.1" ... />
   ```

8. Deploy the WAR file
   ```bash
   sudo cp /tmp/ROOT.war /usr/share/tomcat/webapps/
   ```

9. Restart Tomcat service
   ```bash
   sudo systemctl restart tomcat
   ```

10. Verify application deployment
    ```bash
    curl http://stapp02:6000
    ```

---
### Key Learnings
- Installing and configuring Apache Tomcat  
- Understanding the Tomcat directory structure  
- Modifying server.xml for custom port configurations  
- Deploying WAR files manually
