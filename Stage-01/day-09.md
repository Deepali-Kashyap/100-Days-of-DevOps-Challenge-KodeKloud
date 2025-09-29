# Day 09: MariaDB Troubleshooting  

## 📌 Description  
On this day, I worked on troubleshooting **MariaDB** when the database service was not running properly.  
The goal was to check the service status, create the required data directory, initialize the system database, and finally start MariaDB.  

---
### 1️⃣Login to the Database Server
```bash
ssh peter@stdb01
sudo systemctl status mariadb # Check service status
```

**2️⃣ Create the Data Directory**
```
sudo mkdir -p /var/lib/mysql
sudo chown -R mysql:mysql /var/lib/mysql
sudo chmod 750 /var/lib/mysql
```

**3️⃣ Initialize the MariaDB System Database**
```

sudo mariadb-install-db --user=mysql --basedir=/usr --datadir=/var/lib/mysql
```

**4️⃣ Start MariaDB Service**
```
sudo systemctl start mariadb
sudo systemctl status mariadb   # Verify MariaDB is running
```
