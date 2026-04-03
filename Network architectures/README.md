# Client Server Architecture

Client–Server architecture is a network model where multiple clients request services and a centralized server processes and responds to those requests.
-	Client → Sends request
-	Server → Processes request
-	Server → Sends response

**Example:**

Browser → Web Server → Database → Response

________________________________________

##  How It Works (Step-by-Step)

1.	Client sends HTTP request
2.	Load balancer distributes request
3.	Application server processes logic
4.	Database returns data
5.	Response sent back to client

**Example:**

User → Nginx → Node.js → MongoDB → Response
________________________________________

###  Real-World Examples
-	Web apps (React frontend + Node backend)
-	Banking systems
-	SaaS platforms
-	REST APIs
-	Kubernetes control plane
________________________________________

###  Types of Client-Server Architecture

 1-Tier
Application and database in same system (local app)

 2-Tier
Client ↔ Server ↔ Database

 3-Tier (Very Important for DevOps)
-	Presentation Layer (Frontend)
-	Application Layer (Backend)
-	Data Layer (Database)

Most cloud systems use 3-tier architecture.
________________________________________

###  Advantages
-	Centralized control
-	Easy maintenance
-	Better security
-	Easier monitoring
-	Scalable (horizontal scaling)
________________________________________

### Disadvantages
-	Server failure affects all clients
-	Higher infrastructure cost
-	Requires load balancing

--- 

#  Peer-to-Peer (P2P) architecture

Peer-to-Peer (P2P) architecture is a decentralized network model in which each participating device, called a peer or node, functions both as a client and a server.

 Unlike client-server architecture where a centralized server handles requests, in P2P systems every node can request services and also provide services to other nodes directly.
 
  There is no single central authority controlling the network, which makes the system distributed, scalable, and fault tolerant.

 
 
 

________________________________________

##  Working of P2P

1.	A peer joins the network.

2.	It registers or connects to other available peers.

3.	When it needs data, it searches the network for peers that have it.

4.	Data is transferred directly between peers.

5.	In many systems, data is split into chunks and downloaded from multiple peers.

6.	If one peer leaves, others continue serving the data.

7.	Peer discovery may use Distributed Hash Tables (DHT).
________________________________________

##  Types of P2P 

### 1️. Pure P2P

-	No central server at all
-	All nodes are equal
-	Example: Early file-sharing networks

### 2️. Hybrid P2P

-	Central server for peer discovery
-	Data exchange is still peer-to-peer
-	More controlled system

### 3️. Structured P2P

-	Uses structured lookup (DHT)
-	Faster data searching
-	Efficient large-scale systems
________________________________________

###  Real Examples 
-	BitTorrent – File sharing
-	Bitcoin – Blockchain network
-	Blockchain systems
-	Distributed storage systems
________________________________________

 ### Advantages 

-	No single point of failure
-	Highly scalable
-	Lower infrastructure cost
-	Better resource utilization
-	Fault tolerant
________________________________________

 ### Disadvantages 

-	Harder to secure
-	Difficult monitoring & logging
-	Data consistency issues
-	Trust and malicious node risk
-	Network performance unpredictable



---


![alt text](<Network architecture.png>)

---