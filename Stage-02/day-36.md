# Day 35: Install Docker Packages and Start Docker Service

**Challenge:** Install Docker CE and Docker Compose on a CentOS-based system, then start and verify the Docker service.

📘 **Reference:**  
Official Docker Installation Guide for CentOS:  
👉 [https://docs.docker.com/engine/install/centos/](https://docs.docker.com/engine/install/centos/)

 **Verify Installation**  
   ```bash
   docker --version
   docker compose version
   docker ps
   ```
   - Confirms both Docker and Docker Compose are properly installed and operational.

---
### Outcome
- Docker CE and Docker Compose installed successfully.  
- Docker service started and enabled on system boot.  
- Verified Docker is running and ready for container operations.
### Key Learnings
- Installing Docker from official repositories using `yum`.  
- Managing Docker service lifecycle with `systemctl`.  
- Confirming Docker installation and Compose plugin setup.  
- Understanding the foundational step for containerized application deployment.
