## Day 20: Configure Nginx + PHP-FPM Using Unix Sock

**Challenge:** Set up Nginx to work with PHP-FPM using a Unix socket connection, running on port **8093** for improved performance and security.

---

### Steps Followed

1. **Connect to App Server 2**
   ```bash
   ssh steve@stapp02
   ```
   - Logged into the target application server where Nginx and PHP-FPM will be configured.

2. **Install Nginx**
   ```bash
   sudo yum install -y nginx
   ```
   - Installs the Nginx web server package.

3. **Configure Nginx to Use Port 8093**
   ```bash
   sudo vi /etc/nginx/nginx.conf
   ```
   - Modify the configuration file as follows:
     ```nginx
     server {
         listen       8093;
         root         /var/www/html;
         index        index.php index.html index.htm;

         location ~ \.php$ {
             include fastcgi_params;
             fastcgi_pass unix:/var/run/php-fpm/default.sock;
             fastcgi_index index.php;
             fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
         }
     }
     ```
   - This ensures Nginx listens on **port 8093** and processes PHP files via a Unix socket.

4. **Install(using broswer) and Configure PHP-FPM**
   - Edit the PHP-FPM pool configuration:
     ```bash
     sudo vi /etc/php-fpm.d/www.conf
     ```
     Update or ensure the following values:
     ```
     user = nginx
     group = nginx
     listen = /var/run/php-fpm/default.sock
     ```
   - Create the socket directory and set permissions:
     ```bash
     sudo mkdir -p /var/run/php-fpm
     sudo chown -R nginx:nginx /var/run/php-fpm
     ```

5. **Enable and Restart Services**
   ```bash
   sudo systemctl enable php-fpm
   sudo systemctl restart php-fpm
   sudo systemctl restart nginx
   ```
   - Ensures both services are active and properly linked via the Unix socket.

6. **Verify from Jump Host**
   - From the jump host, test connectivity:
     ```bash
     curl -Ik http://stapp02:8093/
     ```

---

### Outcome
- Nginx successfully configured to serve PHP applications over **port 8093**.  
- PHP-FPM connected through a secure and efficient Unix socket.  
- Verified that Nginx and PHP-FPM services are active and serving requests.

### Key Learnings
- Integration of Nginx with PHP-FPM using Unix sockets.  
- Configuring custom listening ports in Nginx.  
- Managing PHP-FPM pools and socket permissions.  
- Validating web service functionality via command-line tools like `curl`.
