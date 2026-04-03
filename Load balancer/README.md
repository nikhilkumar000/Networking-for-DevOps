# Load Balancers


A load balancer is a system that distributes incoming network traffic across multiple servers to ensure no single server becomes overloaded.

 It improves availability, scalability, and reliability of applications by evenly spreading requests. When a user sends a request (like opening a website using HTTP or HTTPS), the load balancer receives it first and then forwards it to one of the backend servers.
 
  If one server fails, the load balancer automatically redirects traffic to healthy servers, ensuring continuous service.

## Types of Load Balancers

### Layer 4 Load Balancer (Transport Layer)

Works at the transport layer using Transmission Control Protocol and User Datagram Protocol.

Routes traffic based on:
- IP address
- Port number

Does not inspect actual request content
Very fast and efficient

#### Example:

TCP load balancing for APIs or databases

### Layer 7 Load Balancer (Application Layer)

Works at the application layer.

Routes traffic based on:
- URL
- Headers
- Cookies

Can make intelligent decisions

 **Example:**

/api → Backend server

/images → CDN

**Common tools:**

- Nginx
- HAProxy

### Hardware Load Balancer

Physical device installed in data centers
- Very powerful but expensive
- Used in large enterprises

#### Example:

- F5 load balancer

### Software Load Balancer

Runs as software on servers or cloud
Flexible and widely used in DevOps

Examples:

- Nginx
- HAProxy
- Cloud load balancers

### Cloud Load Balancer

Provided by cloud platforms:

- Auto scaling
- Managed service
- High availability

**Examples:**

- AWS ELB
- Azure Load Balancer
- GCP Load Balancer

### Reverse Proxy Load Balancer

- Sits between client and backend servers
- Receives requests and forwards them

#### Example flow:

Client → Nginx → Backend Servers

---

## Load Balancing Algorithms

### Round Robin

Round Robin is a simple load balancing algorithm where incoming requests are distributed sequentially across all servers in a circular order. Each server gets one request at a time, ensuring equal distribution of traffic.

**Example flow:**

- Request 1 → Server A  
- Request 2 → Server B  
- Request 3 → Server C  
- Request 4 → Server A  

 It is easy to implement and works well when all servers have similar capacity, but it does not consider server load.

---
### Least Connections

Least Connections sends the incoming request to the server that currently has the fewest active connections.

**Example:**

- Server A → 10 connections  
- Server B → 5 connections  
- Server C → 2 connections  

 Next request goes to Server C (least load)

 This is more efficient than Round Robin because it considers real-time load, making it ideal for applications where requests take different amounts of time.

---
### Sticky Sessions (Session Affinity)

Sticky Sessions ensure that a user’s requests are always sent to the same server.

Example:

User1 → Server A  
User1 (next request) → Server A  

#### Useful when:

Session data is stored on the server
Applications require user-specific state

 Can be implemented using:

- Cookies
- IP-based routing

#### Drawback:

Can lead to uneven load distribution if many users stick to one server

---

### IP Hash

IP Hash is a load balancing algorithm where the client’s IP address is used to decide which backend server will handle the request. 

The load balancer applies a hash function on the client IP and maps it to a specific server. This ensures that the same client is always routed to the same server, as long as the server pool remains unchanged.

**Example:**

- User IP: 192.168.1.10 → Server A  
- User IP: 192.168.1.11 → Server B  
- User IP: 192.168.1.10 → Server A (again)

 This behavior is similar to sticky sessions, but instead of cookies, it uses the client’s IP.

**Key Points**

- Same IP → Same server
- No need for cookies
- Maintains session consistency
- Works at load balancer level

**Advantages**

- Simple session persistence
- No additional storage (like cookies) needed
- Useful for stateful applications

**Disadvantages**

- Uneven load distribution (if many users - share same IP, like NAT)
- If a server goes down, mapping changes
- Not reliable for mobile users (IP may change)

**DevOps Use Case**

- Applications where session is stored on server
- When cookie-based sticky sessions are not preferred
- Internal systems with stable IP users

---

### How load balancer improves availability

---

A load balancer improves availability by distributing traffic across multiple backend servers, so no single server becomes a point of failure. If one server goes down, the load balancer automatically routes requests to healthy servers, ensuring continuous service.

 It performs health checks to detect failures and remove unhealthy instances. This setup prevents downtime and supports horizontal scaling during high traffic. 
 
 It also helps maintain consistent performance by balancing load evenly. As a result, users experience high uptime and reliability even during failures or traffic spikes.