## Day 16: Install and Configure Nginx as a Load Balancer (LBR)

**Challenge:** Set up and configure Nginx as a load balancer to distribute incoming web traffic across multiple backend application servers running Apache on port 8084.

---

### Steps Followed

1. Login to the Load Balancer Server
   ```bash
   ssh loki@stlb01
   sudo yum install nginx -y
   ```
   - Installed Nginx package on the load balancer host.

2. Login to All App Servers and Verify Apache Status
   ```bash
   ssh tony@stapp01
   ssh steve@stapp02
   ssh banner@stapp03
   ```

3. Check Apache Listening Port and Service Status
   ```bash
   sudo ss -tulnp | grep httpd
   ```
   - Verified Apache is running on port **8084** on each app server.
   ```bash
   sudo systemctl status httpd
   ```
   - Confirmed HTTPD service is active and running.

4. Configure Nginx Load Balancer
   ```bash
   sudo vi /etc/nginx/nginx.conf
   ```
   - Added the following configuration inside the `http` block:
   ```
   http {
       upstream myappservers {
           server stapp01:8084;
           server stapp02:8084;
           server stapp03:8084;
       }

       server {
           listen 80;

           location / {
               proxy_pass http://myappservers;
           }
       }
   }
   ```

5. Test Nginx Configuration Syntax
   ```bash
   sudo nginx -t
   ```
   - Ensures there are no syntax errors.

6. Reload Nginx to Apply Configuration
   ```bash
   sudo systemctl reload nginx
   ```
   - Applies changes without downtime.

---

### Outcome
- Nginx installed and configured as a load balancer.  
- Successfully distributing requests among app servers on port 8084.  
- Verified configuration syntax and applied changes seamlessly.

### Key Learnings
- Installing and configuring Nginx as a reverse proxy/load balancer.  
- Using the `upstream` directive to define backend servers.  
- Managing Nginx configuration testing and reload commands.  
- Understanding basic load balancing flow across multiple app servers.
