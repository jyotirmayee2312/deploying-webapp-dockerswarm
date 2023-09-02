---

# Project Documentation: Deploying a Web App Using Docker Swarm on AWS

## Overview

This project documents the steps to deploy a web application using Docker Swarm on AWS. Docker Swarm is a container orchestration tool that allows you to manage and scale containerized applications efficiently. AWS (Amazon Web Services) provides the cloud infrastructure for hosting our Docker Swarm cluster.

### Project Steps

1. **AWS Instance Setup**
   - Create three AWS instances: Swarm-manager, Swarm-worker1, and Swarm-worker2.
   - Name these instances appropriately in the AWS portal.

2. **Inbound Rule Configuration**
   - For each instance, configure inbound rules in the AWS Security Group as follows:
     - Allow Custom TCP Port 2377 from Anywhere IPv4 (for Docker Swarm management).
     - Allow Custom TCP Port 8001 (or your chosen application port) from Anywhere IPv4 (for web application access).

3. **Docker Installation**
   - Install Docker with Docker Engine on all three AWS instances. Use your preferred method for Docker installation.

4. **Docker Swarm Initialization**
   - On the Swarm-manager instance, initialize the Docker Swarm cluster with the following command:
     ```bash
     sudo docker swarm init
     ```

5. **Adding Worker Nodes**
   - After initializing the Swarm on the manager node, you will receive a command with a token to add other nodes as workers. Run this command on the worker nodes to join them to the Swarm.
   
6. **Checking Swarm Nodes**
   - Confirm that all nodes have successfully joined the Swarm cluster by running the following command on the manager node:
     ```bash
     docker swarm node ls
     ```

7. **Creating a Docker Service**
   - On the Swarm-manager node, create a Docker service for your web application. Modify the image name and port as needed:
     ```bash
     sudo docker service create --name my-web-app --replicas 3 --publish 8001:8001 my-web-app-image:latest
     ```

8. **Checking Service Status**
   - Verify the status of the Docker service by running:
     ```bash
     sudo docker service ls
     ```

9. **Container Verification**
   - Ensure that the service containers are running on the Swarm-manager node:
     ```bash
     sudo docker ps
     ```

10. **Accessing the Web Application**
    - Access your web application by using the public IP address or DNS of any of the AWS instances followed by the port you specified (e.g., `<Public_IP_of_AWS>:8001`).

11. **Node Removal (Optional)**
    - If needed, you can remove a node from the Swarm cluster using the following command on the specific worker node:
      ```bash
      sudo docker swarm leave
      ```

---

