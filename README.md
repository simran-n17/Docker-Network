# Docker Networking

Docker Networking enables seamless communication between Docker containers within a managed network, orchestrated by a master node known as the **Manager**. Containers within a Docker Network can exchange data efficiently, facilitating interconnected services. Below, we explore essential Docker networking concepts and commands to help you get started.

## Types of Network Drivers

Docker provides various network drivers, each catering to specific use cases:

1. **Bridge (Default)**: If no driver is specified when creating a container, it is placed in the default bridge network. This allows containers on the same host to communicate but isolates them from external networks.
2. **Host**: Eliminates container isolation by directly attaching the container to the host machine's network, meaning it won’t have a separate IP.
3. **None**: No networking capabilities are assigned to the container, making it entirely isolated from other containers and external networks.
4. **Overlay**: Enables communication between multiple Docker daemons, facilitating interactions between services in a Docker Swarm.
5. **IPvlan**: Provides complete control over IPv4 and IPv6 addressing, offering flexible networking options.
6. **Macvlan**: Assigns unique MAC addresses to containers, making them appear as physical devices on the network.

---

## 📄 Documentation
- [Docker Official Docs](https://linktodocumentation)
- [Docker Network Guide](https://linktodocumentation)
- [Networking Basics](https://www.geeksforgeeks.org/basics-computer-networking/)

---

## 🚀 Installation & Setup
Before getting started, ensure that Docker is installed on your system, and you are signed in to **Docker Hub** and **Docker Desktop**.

Check existing Docker networks:
```bash
  docker network ls
```

### Launching a Container on the Default Network
1️⃣ **Verify Docker Network Command**
```bash
sudo docker network
```

2️⃣ **Create a Custom Network**
```bash
docker network create --driver bridge --subnet 172.20.0.0/16 --ip-range 172.20.240.0/20 net-bridge
```

3️⃣ **Connect a Container to a Network**
```bash
sudo docker network connect <network-name> <container-name or id>
```

4️⃣ **Inspect Network Details**
```bash
sudo docker network inspect <network-name>
```

5️⃣ **Run a Redis Container in a Bridge Network**
```bash
docker run -itd --net=net-bridge --name=cont_database redis
```

6️⃣ **Retrieve the IP Address of a Specific Container**
```bash
docker inspect --format='{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' cont_database2
```

7️⃣ **Run a BusyBox Container in the Custom Network**
```bash
docker run -itd --net=net-bridge --name=server-A busybox
```

8️⃣ **Inspect Network Details and Format Output in JSON**
```bash
docker inspect --format='{{json .Containers}}' net-bridge | python -m json.tool
```

9️⃣ **Retrieve and Format Network Settings of a Specific Container**
```bash
docker inspect --format='{{json .NetworkSettings}}' server-B | python -m json.tool
```

🔟 **Access a Running Container’s Shell**
```bash
docker container exec -it <CONTAINER ID> bash
```

### Updating and Installing Utilities
🔹 **Update the Package List**
```bash
apt-get update
```

🔹 **Install `ping` Utility for Network Connectivity Testing**
```bash
apt-get install iputils-ping
```

Now, you can test network connectivity using the `ping` command!

Happy Networking! 🚀

