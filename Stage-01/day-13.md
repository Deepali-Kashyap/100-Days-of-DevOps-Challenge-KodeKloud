## Day 13 : IPtables Installation and Configuration

**Challenge:** Install and configure IPtables on the app host to control network traffic, allowing access from a specific Load Balancer IP and blocking all other traffic on a given port.

---

### Steps Followed

1. SSH into the App Host
   ```bash
   ssh tony@stapp01
   ```

2. Install IPtables and dependencies
   ```bash
   sudo yum install -y iptables iptables-services
   ```

3. Add Firewall Rules

   **Assumptions:**
   - Apache port: 5002  
   - Load Balancer (LBR) IP: 172.16.238.14  
     *(Replace this with your actual LBR host IP — you can find it using `ping LBR_host` or from `/etc/hosts`.)*

   ```bash
   # 1. Allow traffic from the Load Balancer host
   sudo iptables -A INPUT -p tcp -s 172.16.238.14 --dport 5002 -j ACCEPT

   # 2. Block all other incoming traffic on port 5002
   sudo iptables -A INPUT -p tcp --dport 5002 -j DROP
   ```

4. Save and Enable IPtables for Persistence After Reboot
   ```bash
   sudo service iptables save
   sudo systemctl enable iptables
   sudo systemctl restart iptables
   ```

---

### Outcome
- IPtables installed and configured successfully  
- Traffic allowed only from the Load Balancer on port 5002  
- All other connections to port 5002 blocked  
- Configuration persists across reboots

---

### Key Learnings
- Installing and managing IPtables firewall in Linux  
- Controlling access using IP and port-based rules  
- Understanding ACCEPT and DROP policies in IPtables  
- Making firewall configurations persistent after system reboot
