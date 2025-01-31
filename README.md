# Docker Swarm Setup Guide 🚀

This guide provides step-by-step instructions for setting up a **Docker Swarm Cluster** with the required **UFW firewall rules** and **Swarm commands**.

## 🔥 Firewall Configuration (UFW)

To enable the necessary ports for Docker Swarm, run the following commands:

```sh
# Swarm management port (Only for Manager nodes)
sudo ufw allow 2377/tcp  

# Swarm node communication (For all Nodes)
sudo ufw allow 7946/tcp   
sudo ufw allow 7946/udp   

# Overlay network (For all Nodes)
sudo ufw allow 4789/udp   

# Swarm services (Optional but recommended)
sudo ufw allow 30000:32767/tcp  
sudo ufw allow 30000:32767/udp  

# Reload firewall rules
sudo ufw reload
````

## 🐳 Docker Swarm Setup

### Initialize the Swarm
Run the following command on the **Manager Node**:

```
docker swarm init --advertise-addr <MANAGER_IP>
```

Replace `<MANAGER_IP>` with the actual IP of the manager node.

### Retrieve Join Tokens
To get the **Manager Join Token**, run:

```
docker swarm join-token manager
```

To get the **Worker Join Token**, run:


```
docker swarm join-token worker
```

### Add Nodes to the Swarm
On **Worker Nodes**, use the token obtained earlier:

```
docker swarm join --token <WORKER_TOKEN> <MANAGER_IP>:2377
```

On **Additional Manager Nodes**, use:

```
docker swarm join --token <MANAGER_TOKEN> <MANAGER_IP>:2377
```

### List Swarm Nodes
To verify connected nodes:

```
docker node ls
```

## 📜 License
This project is licensed under the **MIT License**. See the [LICENSE](LICENSE) file for details.

---

## 🤝 Contributing
🚀 **Contributions are welcome!**  
Feel free to fork this repository, create a branch, and submit a **pull request**.

