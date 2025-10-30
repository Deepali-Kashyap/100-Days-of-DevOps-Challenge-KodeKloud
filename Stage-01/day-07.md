## Day 07 – Linux SSH Authentication

---

### Step 1: Generate SSH Key Pair on Jump Host
```bash
ssh-keygen 
```
- Generates a RSA key pair.
- `id_rsa` is the private key, `id_rsa.pub` is the public key.
- Press Enter to accept defaults and optionally add a passphrase.

### Step 2: Copy Public Key to App Servers
```bash
ssh-copy-id user@app-server-ip
```
- Transfers public key to remote server's `~/.ssh/authorized_keys`.
- Enables password-less authentication.
- ssh-copy-id always copies the public key to the server. Your private key never leaves your machine. This is what enables password-less SSH in a secure way.

### Step 3: Verify SSH Login
```bash
ssh user@app-server-ip
```
- Ensure you can log in without entering a password.
- Confirms the public/private key pair is working correctly.

### Step 4: Best Practices and Monitoring
- Use strong passphrase for private keys.
- Limit access with proper file permissions:
```bash
chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys
```
- Monitor SSH logs for unauthorized access:
```bash
grep sshd /var/log/auth.log
```
### Step 5: Real-World Relevance
- Password-less SSH authentication is essential for automation and scripting in DevOps.
- Reduces the risk of password compromise.
- Supports secure deployment pipelines, configuration management, and remote server administration.
