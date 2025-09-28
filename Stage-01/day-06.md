# Day 06 – Create a Cron Job

---

## Step 1: Install Cron Package
```bash
sudo yum install -y cronie
```
- Installs the cronie package which provides cron service on Linux.
- `-y` automatically confirms installation.

## Step 2: Start and Enable Cron Service
```bash
sudo systemctl start crond
sudo systemctl enable crond
```
- Starts the cron daemon immediately.
- Enables the service to start automatically on boot.

## Step 3: Add Cron Job for Root User
```bash
sudo crontab -e
```
- Add the following line to schedule the job every 5 minutes:
```
*/5 * * * * echo hello > /tmp/cron_text
```
- Saves output "hello" into `/tmp/cron_text` every 5 minutes.

## Step 4: Verification
```bash
sudo crontab -l
cat /tmp/cron_text
```
- Verify that the cron job is listed and that the file `/tmp/cron_text` is being updated.

## Step 5: Importance and Best Practices
- Cron allows scheduling repetitive tasks automatically.
- Ensures jobs run consistently without manual intervention.
- Verify cron jobs regularly and log outputs for auditing.

## Real-World Relevance
- Automates repetitive system maintenance tasks.
- Commonly used in DevOps pipelines for scheduled scripts.
- Supports monitoring, backups, and other automated system operations.
