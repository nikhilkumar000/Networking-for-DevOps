# Ports in DevOps

In networking, a port is a logical communication endpoint used by applications to send and receive data over a network. Every device connected to a network has an IP address, which identifies the device, but multiple applications may run on the same device. 

Ports help the operating system determine which application should receive the incoming data. Ports work together with protocols like Transmission Control Protocol and User Datagram Protocol to enable communication between services.

 In DevOps environments, ports are very important because servers, containers, databases, and web services expose their functionality through specific ports. For example, web servers usually run on port 80 or 443, SSH runs on port 22, and databases like MySQL use port 3306.

In simple terms, if the IP address is the building address, then the port is the room number where a specific service is running.

---

## Types of Ports

### 1. Well-Known Ports (0–1023)

These ports are reserved for common internet services.

**Examples:**

-	22 → SSH
-	80 → HTTP
-	443 → HTTPS
-	25 → SMTP
-	53 → DNS

DevOps engineers frequently interact with these ports while configuring servers.
________________________________________

### 2. Registered Ports (1024–49151)
Used by applications and services.
Examples:
-	3306 → MySQL
-	5432 → PostgreSQL
-	6379 → Redis
-	27017 → MongoDB
________________________________________

### 3. Dynamic / Ephemeral Ports (49152–65535)

Temporary ports used by client applications for communication.

**Example:**

Your browser might open a random port like 50123 when connecting to a server.
________________________________________

## Why Ports Are Important in DevOps

Ports are used for many tasks in DevOps such as:
-	Running web servers
-	Connecting to databases
-	Accessing servers through SSH
-	Exposing containers
-	Configuring load balancers
-	Debugging network issues
-	Monitoring services

For example:

- Frontend server → Port 3000
- Backend API → Port 5000
- Database → Port 3306
________________________________________

##  Common Ports Used in DevOps

| Port  | Service            |
|-------|--------------------|
| 22    | SSH                |
| 80    | HTTP               |
| 443   | HTTPS              |
| 3306  | MySQL              |
| 5432  | PostgreSQL         |
| 6379  | Redis              |
| 27017 | MongoDB            |
| 8080  | Web applications   |
________________________________________

## Linux Commands Related to Ports (Important for DevOps)

### 1. Check Open Ports

**netstat command**

netstat -tuln

#### Meaning:
-	t → TCP ports
-	u → UDP ports
-	l → listening ports
-	n → numeric format

#### Example output:

tcp   0  0 0.0.0.0:22   0.0.0.0:*   LISTEN

This means SSH is running on port 22.
________________________________________

### 2. Using ss command (Modern Replacement for netstat)

ss -tuln

This command shows all listening TCP and UDP ports.

DevOps engineers use this often for debugging services.
________________________________________

### 3. Find Which Process Is Using a Port

lsof -i :3000

#### Example output:

node   2345  user   TCP *:3000 (LISTEN)

This means a Node.js application is running on port 3000.
________________________________________

### 4. Check Port Using netstat with Process ID

netstat -tulpn

#### Example:

tcp   0  0 0.0.0.0:80   0.0.0.0:*   LISTEN   1234/nginx

This shows nginx is using port 80.
________________________________________

### 5. Kill Process Running on a Port

Sometimes a port is already in use.

#### Find process:
- lsof -i :3000

#### Kill it:
 - kill -9 PID

#### Example:
- kill -9 2345
________________________________________

### 6. Test If Port Is Open

Using nc (netcat)

nc -zv localhost 80

#### Output:

Connection to localhost 80 port successful

This means the port is open.
________________________________________

### 7. Check Port with curl

Used for web services.

curl http://localhost:3000

This checks if the server is responding.
________________________________________

### 8. Scan Ports Using nmap

nmap localhost

This scans all open ports on the machine.
________________________________________

### Example in Real DevOps Workflow
Imagine you deploy a MERN application.

- React app → Port 3000
- Node API → Port 5000
- MongoDB → Port 27017
- Nginx → Port 80

Steps DevOps engineer might do:
1.	Check if backend is running
ss -tuln | grep 5000
2.	Check which process is using port
lsof -i :5000
3.	Test API
curl http://localhost:5000


## How Ports Work When You Open a Website

(Browser → Port → Load Balancer → Server → Application)

When you open a website in your browser, ports play a very important role in deciding which service on the server should receive your request. A server can run many services at the same time (web server, database, SSH, etc.), and ports help the operating system route the request to the correct service.

For example, if you type:
https://example.com
your browser automatically connects to port 443, which is the default port for HTTPS. The communication itself happens using Transmission Control Protocol, which ensures reliable delivery of the data packets. The request then travels through several networking components before reaching the application.
________________________________________
## Step-by-Step Flow of a Website Request

### Step 1: User Types Website URL
Example:
https://example.com

The browser understands:
-	Protocol → HTTPS
-	Default Port → 443

So internally the browser prepares a request like:
example.com:443
________________________________________

### Step 2: DNS Resolves Domain to IP

The browser asks Domain Name System to convert the domain name into an IP address.

#### Example:
example.com → 142.250.183.14

Now the browser knows which server to connect to.
________________________________________

### Step 3: TCP Connection to the Server Port

The browser initiates a connection to:
142.250.183.14:443

Here:
-	142.250.183.14 → server IP
-	443 → HTTPS port

TCP then performs a three-way handshake to establish a reliable connection.
________________________________________

### Step 4: Request Reaches Load Balancer

In production systems, traffic usually goes through a load balancer.

**Example architecture:**

User Browser -----------> Internet ----------> Load Balancer (Port 443) ----------> Web Servers


The load balancer:
-	receives traffic on port 443
-	distributes requests across multiple servers.

Example: Nginx or HAProxy.
________________________________________

### Step 5: Reverse Proxy Routes Request

Often the load balancer or reverse proxy forwards the request to an internal application port.

#### Example:
- User Request → Port 443
- Load Balancer → Port 80
- Backend App → Port 3000

Example architecture:
Client ------> Nginx (443) ------> Node.js App (3000)

Here:
-	Nginx listens on 443
-	forwards traffic to the Node.js server running on port 3000
________________________________________

### Step 6: Application Processes Request

The backend application receives the request.

#### Example:

Node.js server running on:

- localhost:3000

The application:
-	processes the request
-	may query a database

#### Example database port:

- MongoDB → 27017
- MySQL → 3306
________________________________________

### Step 7: Response Sent Back

The response follows the reverse path:

Application ---->>> Reverse Proxy ---->>> Load Balancer ---->>> Internet ---->>> User Browser (The browser then displays the webpage )

________________________________________

### Real Production DevOps Architecture Example

User Browser ------->>> Internet ------->>> Cloud Load Balancer (443) ------->>> Nginx Reverse Proxy (80) ------->>> Node.js API Server (3000) ------->>> Database (MongoDB 27017)
 
Each component listens on different ports.
________________________________________

### Example DevOps Commands to Verify Ports

Check running ports:

ss -tuln

Check which service is using port 443:

lsof -i :443

Test web server:

curl https://localhost
________________________________________


#  What is Port Mapping? (DevOps Deep Dive)
 
 


Port mapping (also called port forwarding) is a networking technique that maps a port on a public IP address to a specific private IP address and port inside a local network. It allows external devices on the internet to access services running on private network machines that are otherwise not directly reachable. Port mapping works together with NAT (Network Address Translation) to forward incoming traffic from a public-facing router or server to the correct internal system.

### Interview-Ready One-Liner
Port mapping forwards traffic from a public IP and port to a specific private IP and port, enabling external access to internal services using NAT.
________________________________________

##  Why Port Mapping is Needed

Private IP addresses are not accessible from the internet. If you host a service inside a private network (like a web server or database), outside users cannot reach it unless you configure port mapping.

#### Without port mapping:

Internet → 192.168.1.10 (Blocked)

#### With port mapping:

Internet → PublicIP:80 → Router → 192.168.1.10:80
________________________________________

##  How Port Mapping Works (Step-by-Step)

Example:
-	Public IP: 49.36.120.15
-	Internal Server: 192.168.1.10
-	Web server running on port 80
________________________________________

###  Step 1: External Request

User accesses:

http://49.36.120.15:80
________________________________________

###  Step 2: Router Checks Port Mapping Rule

Router has rule:

Public Port 80 → 192.168.1.10:80
________________________________________

###  Step 3: NAT Translation

Router forwards packet to:

Destination: 192.168.1.10:80
________________________________________

###  Step 4: Response Flow

Internal server responds → Router translates back → Sent to external user.
________________________________________

** Real Example: Hosting Web Server at Home**

If you want to host a website on your local PC:

1.	Install Nginx on local machine
2.	Configure router port forwarding
3.	Map:
Public Port 80 → Local IP 192.168.1.10 Port 80
4.	Now internet users can access your website
_______________________________________
________________________________________

##  Types of Port Mapping

### 1️. Static Port Mapping

Fixed mapping:

Public 80 → Private 80

### 2️. Dynamic Port Mapping

Public port assigned dynamically from pool.

### 3️. PAT (Port Address Translation)

Multiple private devices share one public IP using different ports.

##  Example NAT Table

| Public IP     | Public Port | Private IP     | Private Port |
|---------------|------------|----------------|--------------|
| 49.36.120.15  | 55001      | 192.168.1.10   | 443          |
| 49.36.120.15  | 55002      | 192.168.1.11   | 443          |
________________________________________


###  Security Considerations

-	Opening ports increases attack surface
-	Never expose database ports publicly
-	Use firewall rules
-	Restrict IP ranges
-	Use VPN for sensitive services
________________________________________

##  Port Mapping vs NAT (Key Differences)

| Feature           | NAT (Network Address Translation)              | Port Mapping (Port Forwarding)                |
|-------------------|-----------------------------------------------|----------------------------------------------|
| Definition        | Translates private IPs to public IPs          | Maps a specific public port to a private IP/port |
| Purpose           | Enable outbound internet access               | Allow inbound access to internal services     |
| Direction         | Mostly outbound traffic                       | Mostly inbound traffic                        |
| Mapping Type      | IP-to-IP or many-to-one (PAT)                 | Port-to-IP:Port mapping                       |
| Public Access     | Internal devices are hidden                   | Exposes specific internal service             |
| Example           | 192.168.1.10 → 49.36.120.15                  | 49.36.120.15:8080 → 192.168.1.10:80            |
| Use Case          | Browsing internet from private network        | Hosting web server, SSH, gaming servers       |


# Difference Between Load Balancer and Port Mapping

| Feature | Load Balancer | Port Mapping |
|--------|--------------|-------------|
| Definition | Distributes incoming traffic across multiple servers | Maps a host port to a container port |
| Purpose | Improve scalability, availability, and reliability | Expose container services to outside world |
| Level | Works at network/application level (L4/L7) | Works at container/host level |
| Traffic Handling | Distributes requests among multiple backends | Forwards traffic to a single container |
| Use Case | High traffic systems, microservices, production apps | Local development, simple deployments |
| Example Tool | Nginx, HAProxy, AWS ELB | Docker (`-p` flag) |
| Fault Tolerance | Yes (redirects traffic if one server fails) | No (single container dependency) |
| Complexity | More complex setup | Simple and quick setup |
| Scaling | Supports horizontal scaling | Does not provide scaling |
| Example | User → Load Balancer → Server1/Server2 | User → Host:8080 → Container:3000 |

---






## Why is port 22 dangerous to expose publicly?
 

Port 22 (SSH) is dangerous to expose publicly because it becomes a common target for brute-force and hacking attempts, where attackers try to guess login credentials. If not properly secured (e.g., weak passwords), it can lead to unauthorized server access and full system compromise.
________________________________________

________________________________________

##  Reverse Proxy vs Port Forwarding (Key Differences)

| Feature            | Reverse Proxy                                      | Port Forwarding                                |
|--------------------|----------------------------------------------------|------------------------------------------------|
| Definition         | Server that forwards client requests to backend servers | Maps a public port to a private IP/port         |
| Layer              | Application Layer (Layer 7)                         | Network Layer (Layer 3/4)                       |
| Function           | Handles requests, load balancing, caching, SSL     | Simply forwards traffic to internal device      |
| Security           | Hides backend servers and adds security features   | Exposes internal service directly               |
| Flexibility        | Highly flexible (routing, filtering, auth, etc.)   | Limited (basic port mapping only)               |
| Example            | Nginx, Apache, AWS ALB                             | Router port forwarding                          |
| Use Case           | Web apps, microservices, load balancing            | Access local server from internet               |

## Docker Port Mapping

Docker port mapping is used to connect a container’s internal port to a port on the host machine, so that applications running inside containers can be accessed from outside. By default, containers are isolated and not accessible externally, so we use port mapping to expose them. 

This is done using the -p flag, which binds a host port → container port.

### Syntax

docker run -p <host_port>:<container_port> image_name

**Example**

docker run -p 3000:3000 my-app

#### What this means:

- Container is running app on port 3000

- Host machine exposes it on port 3000

 Access in browser:

http://localhost:3000

#### Another Example

docker run -p 8080:3000 my-app

#### Meaning:
- App runs inside container on 3000

- Accessible outside on 8080

 Access:

http://localhost:8080




## How DevOps Engineers Debug When a Service Is Not Accessible on a Port

In real DevOps work, a common problem is: “My service is running but I cannot access it.”
For example, you deploy a backend API on port 3000, but when you open the browser or send a request, it does not respond.

DevOps engineers follow a step-by-step debugging process to identify where the problem is occurring. The issue could be related to the application, the port, firewall rules, or networking components.
________________________________________

### Step 1: Check if the Application Is Running

First verify that the service is actually running.

**Example command:-**
ps aux | grep node

or if it is a system service:

systemctl status nginx

If the service is not running, start it.

**Example:** 
systemctl start nginx
________________________________________

### Step 2: Check If the Port Is Listening

Next check whether the service is listening on the expected port.

#### Command:

ss -tuln

#### Example output:

tcp   LISTEN   0   128   0.0.0.0:3000

This means the application is listening on port 3000 using Transmission Control Protocol.

If the port is not listed, the application might not be configured correctly.
________________________________________

### Step 3: Check Which Process Is Using the Port

Sometimes another process is already using the port.

#### Command:
lsof -i :3000

#### Example output:
node   2456   user   TCP *:3000 (LISTEN)

This tells you which application is running on that port.
________________________________________

### Step 4: Test the Service Locally

Before testing externally, check if the service works locally.

#### Example:
curl http://localhost:3000

If you get a response, the service is working locally.

If not, the issue is probably inside the application.
________________________________________

### Step 5: Check Firewall Rules

Sometimes the firewall blocks the port.
Check firewall rules:
- sudo ufw status

If the port is blocked, allow it:
- sudo ufw allow 3000

Cloud providers like AWS also have firewall rules.
Example: security groups.
________________________________________

### Step 6: Check If the Service Is Bound to Correct IP

Sometimes applications bind only to localhost (127.0.0.1).

#### Example output:
127.0.0.1:3000

This means the service is only accessible from the same machine.

To allow external access, it should listen on:
0.0.0.0:3000
________________________________________

### Step 7: Check Reverse Proxy Configuration

Many production systems use reverse proxies like Nginx.

#### Example configuration:
server {

    listen 80;

    location / {

        proxy_pass http://localhost:3000;

    }

}

If this configuration is wrong, requests will fail.
________________________________________

### Step 8: Check Network Connectivity

Test whether the port is reachable from another machine.

#### Example:
nc -zv server-ip 3000
or
telnet server-ip 3000

If connection fails, the port might be blocked by firewall or security groups.
________________________________________

### Step 9: Check Container Ports (Docker Case)

If the application runs inside Docker, verify port mapping.

#### Example:
docker ps
#### Output:
0.0.0.0:3000 -> 3000/tcp

If mapping is missing, container ports are not exposed.

#### Correct command:
docker run -p 3000:3000 app
________________________________________

### Step 10: Check Logs

Logs often show the real problem.
#### Example:

journalctl -u nginx
or
docker logs container_id

Logs may reveal errors like:
-	port already in use
-	application crash
-	permission issues
________________________________________

### Real DevOps Debugging Example

Suppose your Node.js API should run on port 5000 but it is not accessible.

DevOps engineer might do:

#### 1️. Check service
- ps aux | grep node

#### 2️. Check port
- ss -tuln | grep 5000

#### 3️. Test locally
- curl localhost:5000

#### 4️. Check firewall
- ufw status

#### 5️. Check reverse proxy
- nginx config

#### 6️. Check cloud firewall / security group
________________________________________

### Quick DevOps Troubleshooting Checklist

When a port is not accessible, check:
1.	Application running or not
2.	Port listening or not
3.	Port already used or not
4.	Local service working or not
5.	Firewall blocking port
6.	Service bound to localhost
7.	Reverse proxy configuration
8.	Container port mapping
9.	Cloud security group
10.	Application logs
