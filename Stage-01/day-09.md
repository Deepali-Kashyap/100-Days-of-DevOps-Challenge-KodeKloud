## Day 09: MariaDB Troubleshooting

**Challenge:** Troubleshoot and fix issues preventing the MariaDB service from running properly by checking its status, setting up the data directory, initializing the system database, and starting the service.

---

### Steps Followed

1. Login to the Database Server
   ```bash
   ssh peter@stdb01
   sudo systemctl status mariadb   # Check service status
   ```

2. Create the Data Directory
   ```bash
   sudo mkdir -p /var/lib/mysql
   sudo chown -R mysql:mysql /var/lib/mysql
   sudo chmod 750 /var/lib/mysql
   ```

3. Initialize the MariaDB System Database
   ```bash
   sudo mariadb-install-db --user=mysql --basedir=/usr --datadir=/var/lib/mysql
   ```

4. Start and Verify MariaDB Service
   ```bash
   sudo systemctl start mariadb
   sudo systemctl status mariadb   # Verify MariaDB is running
   ```

---

### Outcome
- MariaDB data directory created successfully  
- System database initialized properly  
- MariaDB service started and verified  

---

### Key Learnings
- Troubleshooting MariaDB startup issues  
- Understanding MariaDB data directory and permissions  
- Initializing a fresh MariaDB installation  
- Managing database services using `systemctl`
