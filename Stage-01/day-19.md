## Day 19: Install and Configure Web Application

**Challenge:** Deploy and configure a web application by transferring files from the jump host to the app server, setting up Apache (HTTPD), and running it on a custom port (8085).

---

### Steps Followed

1. Copy Website Files from Jump Host to App Server
   ```bash
   scp -r /home/thor/apps banner@stapp03:/tmp/
   scp -r /home/thor/news banner@stapp03:/tmp/
   ```
   - Transfers the website files (`apps` and `news`) from the jump host to the target application server.

2. Move Files to Apache Web Root Directory
   ```bash
   sudo mv /tmp/apps /var/www/html
   sudo mv /tmp/news /var/www/html
   ```
   - Moves the website files into the Nginx/Apache serving directory.

3. Install Apache (HTTPD)
   ```bash
   sudo yum install httpd -y
   ```
   - Installs the Apache web server on the application host.

4. Enable Apache Service
   ```bash
   sudo systemctl enable httpd
   ```
   - Ensures Apache starts automatically on system boot.

5. Configure Apache Port
   ```bash
   sudo vi /etc/httpd/conf/httpd.conf
   ```
   - Modify the `Listen` directive to use port **8085**:
     ```
     Listen 8085
     ```

6. Restart and Verify Apache Service
   ```bash
   sudo systemctl restart httpd
   sudo ss -tulnp | grep httpd
   ```
   - Confirms that Apache is running and listening on port **8085**.
--

### Outcome
- Website files successfully deployed under `/var/www/html`.  
- Apache installed and configured to serve web content on port **8085**.  
- HTTPD service enabled and verified as active.  

### Key Learnings
- Transferring and deploying web files between servers using `scp`.  
- Configuring Apache for custom port usage.  
- Verifying running services and listening ports using `ss`.  
- Managing web content under `/var/www/html` for hosted applications.
