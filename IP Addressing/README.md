# What is IP Addressing?

IP addressing is a system used to uniquely identify devices on a network. Every device connected to a network—such as a computer, server, mobile phone, or router—is assigned an IP (Internet Protocol) address. This address allows devices to communicate with each other by sending and receiving data packets.

Just like a home address helps the postal system deliver mail to the correct house, an IP address ensures that data reaches the correct device on a network or the internet.

### What is an IP Address?

- A logical address assigned to a device
- Works at Network Layer (Layer 3 of OSI)
- Used for routing packets
- Can be public or private
- Can be static or dynamic

Example:
192.168.1.10

---

## IPv4 (Internet Protocol Version 4)

IPv4 is the fourth version of the Internet Protocol and the most widely used addressing system today. It uses a 32-bit address format, which allows approximately 4.3 billion unique addresses.

IPv4 addresses are written in dotted decimal notation, separated by periods. Due to the rapid growth of the internet, IPv4 addresses have largely been exhausted.

**IPv4 Format**

- 32-bit address
- Divided into 4 octets
- Each octet ranges from 0–255
- Written in dotted decimal format

Example:
192.168.0.1

---

### Problems with IPv4

- Limited address space (4.3 billion)
- Address exhaustion
- Requires NAT
- Less built-in security
- Manual configuration complexity

---

## IPv6 (Internet Protocol Version 6)

IPv6 is the latest version of the Internet Protocol designed to replace IPv4. It uses a 128-bit address format, allowing an extremely large number of unique addresses (approximately 340 undecillion). IPv6 addresses are written in hexadecimal format and separated by colons. It was developed to solve the address exhaustion problem and improve efficiency, security, and scalability of modern internet infrastructure.

### IPv6 Format

- 128-bit address
- Written in hexadecimal
- 8 groups separated by colons
- Each group contains 4 hex digits

Example:-
2001:0db8:85a3:0000:0000:8a2e:0370:7334

Compressed form:-
2001:db8:85a3::8a2e:370:7334

---

### Features of IPv6 (Pointwise)

- Massive address space
- No need for NAT
- Built-in IPSec support
- Better routing efficiency
- Auto-configuration (SLAAC)
- Improved multicast

---

### Why IPv6 is Needed

1. IPv4 addresses are exhausted.
2. Growing number of IoT devices.
3. Need for better scalability.
4. Simplified routing.
5. Improved security.
6. End-to-end connectivity without NAT.
7. Future-proof internet infrastructure.

---

### DevOps Perspective

- Cloud providers support IPv6.
- Kubernetes clusters may use IPv6.
- Load balancers support dual-stack.
- Modern applications must handle IPv6.
- Useful in large-scale distributed systems.

## IPv4 vs IPv6 (Key Differences)

| Feature           | IPv4                          | IPv6                                   |
| ----------------- | ----------------------------- | -------------------------------------- |
| Address Length    | 32-bit                        | 128-bit                                |
| Address Format    | Decimal (e.g., 192.168.1.1)   | Hexadecimal (e.g., 2001:0db8::1)       |
| Total Addresses   | ~4.3 billion                  | ~340 undecillion (huge)                |
| Header Complexity | Simple                        | More efficient but larger              |
| Configuration     | Manual / DHCP                 | Auto-configuration (SLAAC)             |
| Security          | Optional (IPSec)              | Built-in IPSec support                 |
| NAT Requirement   | Required (due to limited IPs) | Not required (enough IPs available)    |
| Broadcast         | Supported                     | Not supported (uses multicast instead) |
| Speed             | Slower (due to NAT)           | Faster (no NAT, optimized routing)     |
| Example Use Case  | Traditional internet          | Modern internet, IoT, future networks  |

---

## Public IP vs Private IP

### Public IP Address

A Public IP address is an IP address that is globally unique and reachable over the internet. It is assigned by an Internet Service Provider (ISP) and allows a device, server, or network to communicate directly with the internet.

Public IP addresses must be unique worldwide because routers on the internet use them to route traffic correctly to the intended destination. It is generally used for Used for web servers, APIs, cloud instances.

For example, when you host a website on a cloud server, that server uses a public IP so users from anywhere in the world can access it.

#### Types of Public IP

- Static Public IP → Fixed (used for servers)
- Dynamic Public IP → Changes periodically (home broadband)

---

### Private IP Address

A Private IP address is used within an internal network (like home, office, or cloud VPC) and is not directly accessible from the internet. These IPs are reusable across different networks because they are not globally unique.

Devices inside a private network communicate using private IPs, and when they need internet access, a NAT (Network Address Translation) device converts the private IP to a public IP.

For example, your laptop inside your home WiFi uses a private IP like 192.168.1.5.

#### Private IP Ranges (Very Important for Interview)

Defined by RFC 1918:

- 10.0.0.0 – 10.255.255.255 (10.0.0.0/8)
- 172.16.0.0 – 172.31.255.255 (172.16.0.0/12)
- 192.168.0.0 – 192.168.255.255 (192.168.0.0/16)

### Key Characteristics of Private IP address

- Not accessible from internet
- Reusable in different networks
- Used inside LAN or VPC
- Requires NAT for internet access
- More secure by default

---

## How Public and Private IP Work Together

![alt text](< Private-Public-IP.png >)

#### Example: Home Network (Step-by-Step Packet Flow)

Let’s say:

- Laptop Private IP → 192.168.1.10
- Router Public IP → 49.36.120.15
- Website Server IP → 142.250.190.78

---

### Step 1: Laptop Sends Request

Your laptop wants to open a website.

It sends:

- Source IP: 192.168.1.10
- Destination IP: 142.250.190.78

But this private IP cannot travel on the internet.

---

### Step 2: Router Performs NAT

Router replaces the source IP with its public IP:

- Source IP: 49.36.120.15
- Destination IP: 142.250.190.78

Router also stores mapping in NAT table:

Private IP-------------Public IP-------------Port

192.168.1.10---------49.36.120.15---------55001

This is called PAT (Port Address Translation).

---

### Step 3: Internet Sees Only Public IP

The website server thinks request came from:
49.36.120.15 (Router's public IP)

It has no idea about internal private IP.

---

### Step 4: Response Comes Back

Server responds to:

- Destination IP: 49.36.120.15

Router checks NAT table, sees port mapping, and forwards response to:

- 192.168.1.10

Your laptop receives the webpage.

---

### Cloud Example (DevOps Important)

In Amazon Web Services (AWS):

- EC2 in Private Subnet → Private IP only
- NAT Gateway → Has Public IP
- Private instance sends traffic via NAT

**Flow:**

Private EC2 → NAT Gateway → Internet → Response → NAT → EC2

Production design:

- Database in private subnet
- App server in private subnet
- Load balancer in public subnet
- NAT for outbound traffic

### Why This Design Is Used

**Security:-**
Private IP systems are not directly accessible from internet.

**IP Conservation:-**
One public IP can serve thousands of private devices.

**Network Organization:-**
Internal systems stay isolated.

---

### Public vs Private IP in Cloud (DevOps Important)

In Amazon Web Services (AWS):

- EC2 in Public Subnet → Has Public IP
- EC2 in Private Subnet → No Public IP
- Private instances access internet via NAT Gateway

Production Best Practice:

- Keep database in private subnet
- Only load balancer in public subnet

---

## Public IP vs Private IP (Key Differences)

| Feature       | Public IP                               | Private IP                             |
| ------------- | --------------------------------------- | -------------------------------------- |
| Definition    | IP address accessible over the internet | IP address used within a local network |
| Assigned By   | Internet Service Provider (ISP)         | Router / DHCP                          |
| Accessibility | Globally reachable                      | Not accessible from internet directly  |
| Uniqueness    | Unique across the internet              | Unique only within local network       |
| Security      | Less secure (exposed to internet)       | More secure (hidden behind NAT)        |
| Cost          | Limited and may cost                    | Free and reusable                      |
| Example       | 52.14.22.10                             | 192.168.1.1                            |
| Usage         | Hosting websites, servers               | Internal communication (LAN devices)   |

---

## How IP Addresses Are Allocated

### Public IP Allocation (Hierarchy)

1. Global authority → Internet Assigned Numbers Authority (IANA)
2. IANA allocates blocks to Regional Internet Registries (RIRs)
3. RIR allocates to ISPs
4. ISP assigns to customers
   RIR Examples:

- APNIC (Asia-Pacific)
- ARIN (North America)

---

### Private IP Allocation

Private IPs are assigned by:

- Router DHCP server (home network)
- Corporate DHCP server
- Cloud VPC CIDR allocation

Example:

When you create a VPC in AWS:
10.0.0.0/16

AWS assigns private IPs automatically inside that range.

### Inbound vs Outbound Traffic

#### Outbound (Easy)

Private → NAT → Internet

#### Inbound (Needs Configuration)

Internet → Public IP → Port forwarding → Private IP

Example:
Hosting web server at home requires port forwarding.

---

## Static IP vs Dynamic IP

### What is a Static IP?

A Static IP address is an IP address that remains permanently assigned to a device and does not change over time. It is manually configured or reserved and is commonly used for servers, networking devices, and infrastructure components that require consistent and reliable access.

Static IPs are important when hosting websites, running mail servers, configuring firewalls, or enabling remote access because the address must remain constant for proper routing and DNS mapping.

### Characteristics of Static IP

- Does not change automatically
- Manually assigned or reserved
- Used for servers and networking devices
- Required for DNS mapping
- More predictable and stable

### Where Static IP is Used

- Web servers
- Load balancers
- VPN servers
- Database endpoints (sometimes internal static)
- Cloud Elastic IP
  Example in Amazon Web Services (AWS):
- Elastic IP = Static public IP
- Used for production server stability

---

### What is a Dynamic IP?

A Dynamic IP address is automatically assigned to a device by a DHCP (Dynamic Host Configuration Protocol) server and can change periodically. Most home internet connections and corporate internal networks use dynamic IP allocation to efficiently manage limited IP address pools.

Dynamic IP addresses reduce administrative overhead because they are assigned automatically when a device connects to the network.

### Characteristics of Dynamic IP (Pointwise)

- Automatically assigned
- Managed by DHCP server
- May change periodically
- Cost-effective
- Common for home users

### How Dynamic IP Works (Step-by-Step)

1. Device connects to network
2. DHCP server receives request
3. DHCP assigns available IP from pool
4. IP is leased for a specific duration
5. Lease expires → IP may change
   DHCP uses DORA process:

- Discover
- Offer
- Request
- Acknowledge

---

## Static IP vs Dynamic IP (Key Differences)

| Feature    | Static IP                                | Dynamic IP                           |
| ---------- | ---------------------------------------- | ------------------------------------ |
| Definition | Fixed IP address that does not change    | IP address that changes periodically |
| Assignment | Manually configured or reserved          | Automatically assigned via DHCP      |
| Stability  | Constant and stable                      | May change over time                 |
| Cost       | Usually paid                             | Usually free or included             |
| Security   | Less secure (easier to track)            | More secure (changes frequently)     |
| Use Case   | Hosting servers, websites, remote access | Home users, general browsing         |
| Example    | 52.14.22.10                              | Changes like 49.36.x.x               |

---

## Public vs Private Static/Dynamic (Important Concept)

Both public and private IPs can be static or dynamic.

### Public Static IP

- Elastic IP in AWS
- Required for production services

### Public Dynamic IP

- Home broadband connection

### Private Static IP

- Internal database server

### Private Dynamic IP

- Office laptop via DHCP

## DevOps Perspective

When to Use Static IP

- Hosting production server
- SSL certificate mapping
- DNS A record mapping
- Firewall whitelisting
- VPN endpoint

When to Use Dynamic IP

- Internal employees’ devices
- Temporary environments
- Auto-scaling cloud instances

---

## DHCP (Dynamic Host Configuration Protocol)

DHCP is a network protocol used to automatically assign IP addresses and other network configuration details (like subnet mask, gateway, and DNS server) to devices when they join a network.

It removes the need for manual IP configuration and ensures devices can communicate on the network immediately.

### How DHCP Works ( DORA Process)

1. Discover – Device broadcasts a request asking for an IP address.
2. Offer – DHCP server offers an available IP address.
3. Request – Device requests the offered IP.
4. Acknowledge – DHCP server confirms and assigns the IP address.

### Key Points

- Automatically assigns IP addresses
- Reduces manual configuration
- Uses a lease system (IP assigned for a specific time)
- Common in home routers, offices, and cloud networks

### Example

When you connect your laptop to WiFi:

Laptop → DHCP Request → Router (DHCP Server) → Assigns IP

Example assigned IP:
192.168.1.25
