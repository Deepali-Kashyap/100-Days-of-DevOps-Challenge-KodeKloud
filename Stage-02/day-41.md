## Day 41: Write a Docker File

**Challenge:** Create a custom Docker macvlan network for isolated container communication on Application Server 3.

---

### Steps Followed

1. **Login to App Server 3**  
   ```bash
   ssh tony@stapp03
   ```

2. **Verify Docker is Running**  
   ```bash
   docker ps
   sudo systemctl start docker
   ```

3. **Find the Parent Network Interface**  
   ```bash
   ip link
   ```
   Example Output:
   ```
   1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN mode DEFAULT group default 
   2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP mode DEFAULT group default qlen 1000
   ```
   - Note the parent interface (commonly `eth0` or `docker0`).

4. **Create a Macvlan Network**  
   ```bash
   docker network create -d macvlan \
     --subnet=172.168.0.0/24 \
     --ip-range=172.168.0.0/24 \
     --gateway=172.168.0.1 \
     -o parent=docker0 \
     ecommerce
   ```
   - `-d macvlan` → specifies macvlan driver  
   - `--subnet`, `--ip-range`, `--gateway` → define the network configuration  
   - `-o parent` → attaches macvlan to the host’s network interface  

5. **Verify the Network**  
   ```bash
   docker network ls
   docker network inspect ecommerce
   ```
   - Lists all Docker networks and inspects the new `ecommerce` network for detailed configuration.

---

### Result & Insights
✅ Successfully created a **macvlan** network named **ecommerce**.  
✅ Verified its configuration and attachment to the parent interface.  
💡 Learned how to use Docker networking options for isolated communication, useful in complex multi-container or production-like setups.
