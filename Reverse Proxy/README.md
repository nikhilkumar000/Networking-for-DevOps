# Reverse Proxy


A reverse proxy is a server that sits between clients (users) and backend servers, receiving client requests and forwarding them to the appropriate backend service.

 The client does not directly communicate with the backend server; instead, it interacts only with the reverse proxy. 
 
 After processing, the reverse proxy sends the response back to the client. Tools like Nginx and HAProxy are commonly used as reverse proxies in DevOps architectures.

## Why We Use Reverse Proxy

Reverse proxies are used to improve performance, security, scalability, and manageability of applications.

 They can handle tasks like load balancing, SSL termination, caching, request routing, and hiding backend servers from direct exposure. 
 
 This adds an extra layer of protection and flexibility. For example, instead of exposing multiple backend services directly to the internet, you expose only the reverse proxy, which then intelligently routes traffic to the correct service. This is essential in modern cloud and microservices architectures.

## Common Use Cases of Reverse Proxy

**1. Load Balancing**

A reverse proxy distributes incoming traffic across multiple backend servers.

#### Example:

Client → Nginx → Server1 / Server2 / Server3

 Prevents overload and improves availability.

**2. SSL Termination**

The reverse proxy handles HTTPS encryption using Transport Layer Security.

Client (HTTPS) → Reverse Proxy (decrypts) → Backend (HTTP)

 Reduces load on backend servers.

**3. API Gateway / Routing**

Routes requests based on URL or path.

Example:

/api → Backend API server  
/images → Static server  

 Useful in microservices.

**4. Security (Hide Backend Servers)**
Backend servers are not directly exposed
Prevents direct attacks

 Only reverse proxy IP is visible.

**5. Caching**

Reverse proxy can store frequently requested data.

 Faster response and reduced backend load.

**6. Compression**

Compresses responses before sending to client.

 Improves performance and reduces bandwidth.

**Real DevOps Example**

User → Nginx (Reverse Proxy)

          │
          ├── /api → Node.js (Port 3000)
          ├── /auth → Auth Service (Port 4000)
          └── /images → Static Server

## Why Use Nginx


Nginx is widely used in DevOps because it is a high-performance web server, reverse proxy, and load balancer that can handle a large number of concurrent connections efficiently.

 It uses an event-driven architecture, which makes it faster and more scalable compared to traditional servers. Nginx is commonly used in production systems to serve websites, route traffic, secure applications, and improve performance. 
 
 It plays a critical role in modern architectures like microservices, cloud deployments, and containerized environments.

### Key Reasons to Use Nginx

---

**1. High Performance & Scalability :-**

- Handles thousands of concurrent connections
- Uses low memory and CPU
- Ideal for high-traffic applications

**2. Reverse Proxy :-**
Acts as a middle layer between client and backend
Hides backend servers

Example:
User → Nginx → Backend (Node.js / Java / Python)

**3. Load Balancing :-**
Distributes traffic across multiple servers
Supports:
- Round Robin
- Least Connections
- IP Hash

**4. SSL/TLS Termination :-**

- Handles HTTPS using Transport Layer Security
- Offloads encryption work from backend

**5. Static File Serving :-**

Very fast at serving:
- HTML
- CSS
- Images

Faster than backend servers for static content

**6. API Gateway / Routing :-**
Routes requests based on URL

Example:

/api → Backend  
/images → Static server 

**7. Security :-**

- Hides backend servers
- Supports rate limiting
- Helps prevent attacks

**8. Caching & Compression :-**

- Caches responses → faster performance
- Compresses data → reduces bandwidth

#### Real DevOps Architecture Example
User → Nginx (443 HTTPS)
          
          │
          ├── React App (Static Files)
          ├── Node.js API (Port 3000)
          └── Database (Internal)

### Why backend should not have public IP

Backend servers should not have a public IP because it exposes them directly to the internet, increasing the risk of attacks like DDoS, brute force, and unauthorized access. 

Instead, they are placed in private networks (VPCs) and accessed only through controlled layers like load balancers or reverse proxies. This improves security by hiding internal architecture and reduces the attack surface.

 It also allows better control using firewalls, security groups, and internal routing. In DevOps, this design follows the principle of least exposure, ensuring only necessary components are public. Overall, it keeps backend services safe and manageable.