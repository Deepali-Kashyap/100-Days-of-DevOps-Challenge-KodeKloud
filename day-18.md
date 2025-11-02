## Day 18: Configure LAMP Server

**Challenge:** Set up a LAMP (Linux, Apache, MariaDB, PHP) stack by configuring a database on the DB server and integrating it with Apache and PHP on the app servers.

---

### Steps Followed

1. Login to the Database Server
   ```bash
   ssh peter@stdb01
   ```

2. Install and Start MariaDB
   ```bash
   sudo yum install mariadb-server mariadb -y
   sudo systemctl start mariadb
   sudo systemctl enable mariadb
   ```

3. Login to MariaDB Shell
   ```bash
   sudo -u root mysql
   ```

4. Create Database and User
   ```sql
   -- Create the database
   CREATE DATABASE kodekloud_db5;

   -- Create the user with password
   CREATE USER 'kodekloud_rin'@'%' IDENTIFIED BY 'BruCStnMT5';

   -- Grant full privileges on the database to the user
   GRANT ALL PRIVILEGES ON kodekloud_db5.* TO 'kodekloud_rin'@'%';
   ```

5. Login to Each Application Server
   ```bash
   ssh tony@stapp01
   ssh steve@stapp02
   ssh banner@stapp03
   ```

6. Install Apache (HTTPD) and PHP
   ```bash
   sudo yum install -y httpd php php-mysqlnd
   ```

7. Enable and Start Services
   ```bash
   sudo systemctl enable httpd php
   sudo systemctl start httpd php
   sudo systemctl status httpd php
   ```

8. Configure Apache Port
   ```bash
   sudo vi /etc/httpd/conf/httpd.conf
   ```
   - Change the `Listen` directive to use port **3004**:
     ```
     Listen 3004
     ```

9. Restart Apache Service
   ```bash
   sudo systemctl restart httpd
   ```

---

### Outcome
- MariaDB installed and configured with a new database and user.  
- Apache and PHP installed and running on all application servers.  
- HTTPD configured to listen on port **3004**.  
- Verified successful startup and service operation.

### Key Learnings
- Setting up and configuring a LAMP stack on multiple servers.  
- Creating and managing databases and users in MariaDB.  
- Configuring Apache for custom ports.  
- Integrating PHP and database connectivity for web applications.
