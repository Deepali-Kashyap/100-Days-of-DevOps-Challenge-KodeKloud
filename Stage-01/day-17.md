## Day 17: Install and Configure PostgreSQL

**Challenge:** Install and configure PostgreSQL, create a new database and user, assign privileges, and verify successful access.

---

### Steps Followed

1. Login to the Database Server
   ```bash
   ssh peter@stdb01
   ```

2. Access PostgreSQL Shell as the `postgres` Superuser
   ```bash
   sudo -i -u postgres psql
   ```
   - Opens the PostgreSQL interactive shell (`psql`) as the administrative user.

3. Create a User with Password
   ```sql
   CREATE USER kodekloud_top WITH PASSWORD 'B4zNgHA7Ya';
   ```

4. Create a New Database
   ```sql
   CREATE DATABASE kodekloud_db2;
   ```

5. Grant Privileges on the Database to the User
   ```sql
   GRANT ALL PRIVILEGES ON DATABASE kodekloud_db2 TO kodekloud_top;
   ```

6. Exit the PostgreSQL Shell
   ```sql
   \q
   ```

7. Verify Database Access (Optional)
   ```bash
   psql -U kodekloud_top -d kodekloud_db2 -h localhost
   ```
   - Confirms that the user can successfully connect to the database.

---

### Outcome
- PostgreSQL configured successfully.  
- User `kodekloud_top` created with appropriate privileges.  
- Database `kodekloud_db2` created and linked to the new user.  
- Verified access using the created credentials.

### Key Learnings
- Managing PostgreSQL users and databases via `psql`.  
- Understanding privilege assignments in PostgreSQL.  
- Securely connecting to a database using a specific user.  
- Basic SQL commands for database administration.
