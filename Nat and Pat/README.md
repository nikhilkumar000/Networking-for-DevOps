# NAT (Network Address Translation)

NAT (Network Address Translation) is a method used to map multiple private IP addresses within a local network to a single public IP address before transferring the information to the internet.

Think of it like a corporate mailroom: Everyone in the building has an internal extension (Private IP), but when they send a letter outside, the return address is always the main building's street address (Public IP). When a reply comes back, the mailroom (NAT) knows exactly which desk it belongs to.

##  Why do we need NAT?

- #### IP Address Conservation:

 There are only about 4.3 billion IPv4 addresses. Without NAT, we would have run out of addresses decades ago. NAT allows thousands of devices to share one public IP.

- #### Security:
 NAT acts as a natural firewall. Since internal devices are "hidden" behind a public IP, outside hackers cannot see or directly initiate a connection to a specific computer inside your network.

- #### Flexibility:
 You can change your internal IP scheme without needing to change your public IP provided by your ISP.

## How NAT Works (Step-by-Step)

 #### Step 1  (Request) :
 Your laptop (192.168.1.5) sends a request to visit a website.

 #### Step 2 (Translation) : 
The packet reaches your router (the NAT device). The router strips away your private IP and replaces it with its Public IP (e.g., 203.0.113.1).

 #### Step 3 (The NAT Table) :
 The router makes a note in a "Translation Table" that Port 5001 on the Public IP belongs to 192.168.1.5.

 #### Step 4 (Response) :
 The website sends data back to the router's Public IP.

 #### Step 5 (Forwarding) :
 The router checks its table, sees Port 5001, and passes the data back to your laptop.

## Common Types of NAT

### Static NAT (One-to-One):
 Maps one private IP to one specific public IP. Used mainly for web servers hosted inside a network.

### Dynamic NAT:
 Uses a pool of public IPs. When a device needs the internet, the router grabs any available public IP from the "pool."

### PAT (Port Address Translation):
 This is what you use at home. It uses a single public IP but assigns a unique Port Number to every device to keep the traffic separated.

## NAT in your AWS VPC
Since you are working on AWS architecture, you'll encounter the NAT Gateway. This is a managed service that sits in your Public Subnet.

### The Use Case: 
Your Database is in a Private Subnet (no internet access). It needs to download a security patch.

### The Flow:
 The Database sends the request to the NAT Gateway. The NAT Gateway uses its Elastic IP (Public) to get the patch and sends it back to the Database.

### The Benefit: 
The Database gets its update, but no one on the internet can "see" or attack the Database directly because it doesn't have a public IP.

---
---
---

# PAT (Port Address Translation)

PAT (Port Address Translation) is a type of NAT where multiple devices share a single public IP address using different port numbers. It is also known as NAT overload. Instead of assigning one public IP per device, PAT uses one public IP and multiple ports to uniquely identify each connection. This is widely used in home networks and cloud environments because it efficiently allows many devices to access the internet using just one public IP.

## PAT (Port Address Translation) – Working Step by Step





##  Real Example Setup

### Private Network Devices:

- PC1 → `192.168.1.2`
- PC2 → `192.168.1.3`
- Router Public IP → `203.0.113.1`

---

##  Step-by-Step Working of PAT

### Step 1: Device Sends Request

PC1 wants to access a website:


Source IP: 192.168.1.2

Destination IP: 8.8.8.8 (Google DNS)

Port: Random (e.g., 1234)


---

### Step 2: Router Applies PAT

Router replaces:

- Private IP → Public IP  
- Assigns a unique port  


192.168.1.2:1234 → 203.0.113.1:5001


---

### Step 3: Multiple Devices Use Same Public IP

PC2 also sends a request:


192.168.1.3:2345 → 203.0.113.1:5002


**Notice:**
- Same public IP (`203.0.113.1`)
- Different ports (`5001`, `5002`)

---

### Step 4: Request Goes to Internet

Now both requests go to the internet:


203.0.113.1:5001 → 8.8.8.8

203.0.113.1:5002 → 8.8.8.8


---

### Step 5: Response Comes Back

Server responds:


8.8.8.8 → 203.0.113.1:5001

8.8.8.8 → 203.0.113.1:5002


---

### Step 6: Router Maps Back to Devices

Router checks its PAT table:

| Public IP:Port       | Private IP:Port     |
|---------------------|---------------------|
| 203.0.113.1:5001    | 192.168.1.2:1234    |
| 203.0.113.1:5002    | 192.168.1.3:2345    |

 Then forwards:


203.0.113.1:5001 → 192.168.1.2

203.0.113.1:5002 → 192.168.1.3


---

##  Full Flow Diagram


PC1 (192.168.1.2) ─┐

                   ├──> Router (PAT) ───> Internet
PC2 (192.168.1.3) ─┘

**Router Mapping:**

203.0.113.1:5001 → PC1

203.0.113.1:5002 → PC2


---

##  Key Points

- Multiple devices share **one public IP**
- Each connection is identified using **unique port numbers**
- Router maintains a **PAT table**
- Efficient use of IP addresses
- Widely used in home networks & cloud environments

---








##  NAT vs PAT (Key Differences)

| Feature            | NAT (Network Address Translation)         | PAT (Port Address Translation)            |
|--------------------|--------------------------------------------|-------------------------------------------|
| Mapping Type       | One-to-One                                 | Many-to-One                               |
| IP Usage           | One private IP → One public IP             | Multiple private IPs → One public IP       |
| Port Usage         | Does not use port numbers                  | Uses port numbers to differentiate traffic|
| Efficiency         | Less efficient (needs more public IPs)     | Highly efficient (saves public IPs)        |
| Also Known As      | Static/Dynamic NAT                         | NAT Overload                              |
| Example            | 10.0.1.5 → 52.x.x.x                        | 10.0.1.5:5000 → 52.x.x.x:3001              |