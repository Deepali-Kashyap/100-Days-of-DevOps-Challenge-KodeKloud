# Day 15: Setup SSL for Nginx

**Challenge:** Install and configure Nginx with SSL/TLS certificates to serve secure HTTPS traffic on App Server 3.

---

### Steps Followed

1. Login to App Server 3
   ```bash
   ssh banner@stapp03
   ```

2. Install Nginx and Create Web Root Directory
   ```bash
   sudo yum install -y nginx
   sudo mkdir -p /var/www/html
   ```

3. Create an Index Page
   ```bash
   echo "Welcome!" | sudo tee /var/www/html/index.html
   ```
   - Confirms Nginx will have content to serve once configured.

4. Move SSL Files to Nginx’s SSL Directory
   ```bash
   sudo mkdir -p /etc/nginx/ssl
   sudo mv /tmp/nautilus.crt /etc/nginx/ssl/
   sudo mv /tmp/nautilus.key /etc/nginx/ssl/
   sudo chmod 600 /etc/nginx/ssl/nautilus.key
   ```
   - Moves certificate and private key to the correct directory with proper permissions.

5. Configure Nginx for HTTPS
   ```bash
   sudo vi /etc/nginx/conf.d/default.conf
   ```
   - Update the configuration file with the following content:
   ```
   server {
       listen 80;
       listen 443 ssl;
       server_name _;

       ssl_certificate     /etc/nginx/ssl/nautilus.crt;
       ssl_certificate_key /etc/nginx/ssl/nautilus.key;

       root /var/www/html;
       index index.html;

       location / {
           try_files $uri $uri/ =404;
       }
   }
   ```

6. Test and Start Nginx
   ```bash
   sudo nginx -t
   sudo systemctl enable nginx
   sudo systemctl start nginx
   ```
   - Verifies configuration and starts the Nginx service.

7. Verify SSL from Jump Host
   ```bash
   curl -Ik https://<app-server-ip>/
   ```
   - The `-I` flag fetches only headers to confirm HTTPS connection.  
   - Expected response includes `HTTP/1.1 200 OK`.

---

### Outcome
- Nginx successfully installed and configured for HTTPS.  
- SSL certificates properly placed and secured.  
- Verified secure access using `curl` from the jump host.

---

### Key Learnings
- Installing and configuring Nginx on CentOS/RHEL.  
- Setting up SSL/TLS certificates for secure web communication.  
- Editing Nginx configuration files for HTTPS.  
- Testing and validating SSL setup using `curl`.
