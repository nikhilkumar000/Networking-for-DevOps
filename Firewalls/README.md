# Firewall

A firewall is a network security device (or software) that monitors and filters incoming and outgoing network traffic based on an organization's previously established security policies.

At its most basic level, a firewall is essentially the security guard at the entrance of a private network. it examines every "packet" of data trying to enter or leave and decides whether to let it pass or block it.

## Core Functions of a Firewall

### 1. Packet Filtering
This is the most fundamental function. The firewall inspects every packet of data. It looks at the source IP, destination IP, and Port Number (like Port 22 for SSH or Port 80 for Web). If the packet doesn't match the "Allowed" list, it is instantly dropped.

### 2. Connection Tracking (Stateful Inspection)
Modern firewalls don't just look at one packet; they remember the "state" of a connection.

#### Example:
 If you send a request from your computer to Google, the firewall remembers you started that conversation. When Google sends data back, the firewall lets it in because it recognizes it as part of an established "session."

### 3. Network Address Translation (NAT)
As we discussed earlier, many firewalls also perform NAT. They hide the private IP addresses of your internal devices (like your dev machine or your database) and represent them to the internet using a single public IP address.

### 4. Application-Level Inspection
Advanced firewalls (Next-Generation Firewalls or NGFWs) can look "deeper" into the data. Instead of just seeing that traffic is coming through Port 80 (Web), they can detect if that traffic contains a SQL Injection attack or a virus trying to enter your network.

### 5. Virtual Private Network (VPN) Support
Many enterprise firewalls act as the "gateway" for VPNs. They encrypt the connection between a remote employee (working from home) and the office network, ensuring that sensitive company data isn't exposed on the public internet.

## Types of Firewall

### 1. Packet Filtering Firewall (The First Generation)
This is the oldest and simplest type. It operates at the Network Layer (Layer 3) and Transport Layer (Layer 4) of the OSI model.

#### How it works:
 It looks at each packet individually. It checks the Source IP, Destination IP, Protocol (TCP/UDP), and Port Number against a list of rules (Access Control Lists or ACLs).

#### Weakness:
 It is "stateless." It doesn't know if a packet is a response to a request you sent or a random attack from outside.

#### DevOps Context: 
This is exactly how AWS Network ACLs (NACLs) work. They are fast but "dumb."

### 2. Stateful Inspection Firewall (The Standard)
Unlike the packet filter, this firewall keeps track of the "state" of active connections.

#### How it works:
 It maintains a State Table. If you reach out to a website, the firewall records that "outbound" connection. When the website sends data back, the firewall sees the entry in its table and lets the data in automatically.

#### Benefit:
 You don't need to write a rule for every single return packet. It’s much more secure because it blocks any "unsolicited" incoming traffic.

#### DevOps Context:
 AWS Security Groups are stateful. If you allow outbound traffic on Port 80, the return traffic is automatically allowed.

### 3. Proxy Firewall (The Middleman)
A Proxy Firewall (also called an Application-Level Gateway) acts as the only entry point to the network.

#### How it works:
 A client from the internet connects to the Proxy, not your server. The Proxy then makes a new request to your server on the client's behalf. The two never talk directly.

#### Benefit:
 It completely hides your internal network addresses. It can also perform "Deep Packet Inspection" to look for specific forbidden content inside the data (like blocking certain URLs).

#### Downside:
 It is slower because it has to terminate and recreate every single connection.

### 4. Next-Generation Firewall (NGFW)
This is the modern enterprise standard. It combines the features of the first three and adds advanced security layers.

#### How it works: 
It doesn't just look at ports and IPs; it looks at the Application. It can tell the difference between "Facebook Chat" and "Facebook Video" and block one while allowing the other.

#### Key Features:

- IPS (Intrusion Prevention System): Automatically blocks known hacking patterns.

- Sandboxing: Runs suspicious files in a safe "bubble" to see if they are malware before letting them into your network.

- Antivirus/Malware Filtering: Scans traffic in real-time.

#### DevOps Context:
 Services like AWS Network Firewall or third-party tools like Palo Alto/Fortinet are used here to protect complex cloud environments.

 ### 🔥 Firewall Types Comparison (Quick Reference)

| Feature         | Packet Filter      | Stateful              | Proxy                 | NGFW                  |
|-----------------|-------------------|-----------------------|-----------------------|-----------------------|
| OSI Layer       | 3 & 4             | 3, 4, & 5             | 7 (Application)       | 3 through 7           |
| Performance     | Very Fast         | Fast                  | Slow                  | Moderate              |
| Security Level  | Low               | Medium                | High                  | Very High             |
| Example         | Router ACLs       | AWS Security Groups   | Web Proxy             | Next-Gen Firewall     |

## Interview Questions 

### UFW (Uncomplicated Firewall)


UFW (Uncomplicated Firewall) is a user-friendly tool used to manage firewall rules in Linux systems. It acts as a simplified interface over iptables, making it easier for DevOps engineers to control incoming and outgoing traffic without writing complex rules.

 UFW is commonly used to allow or block ports, restrict IP access, and secure servers quickly. It is especially useful in cloud and production environments where basic firewall configurations are required.

**Common Commands**

- sudo ufw enable
- sudo ufw status
- sudo ufw allow 22        # allow SSH
- sudo ufw allow 80        # allow HTTP
- sudo ufw allow 443       # allow HTTPS
- sudo ufw deny 3000       # block port


## iptables


iptables is a powerful and low-level firewall utility in Linux used to define rules for packet filtering, NAT, and port control. It works directly with the Linux kernel and provides fine-grained control over network traffic. 

Unlike UFW, iptables is more complex but highly flexible, making it suitable for advanced security configurations in DevOps and production systems.

**Example Commands**

- sudo iptables -L                  # list rules

- sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT

- sudo iptables -A INPUT -p tcp --dport 3000 -j DROP

## Port Blocking



Port blocking is the process of restricting access to specific network ports to prevent unauthorized communication. In DevOps, only required ports (like 22, 80, 443) are kept open, while all unnecessary ports are blocked. This reduces the attack surface and prevents malicious access to services running on unused or sensitive ports.

**Example**

- sudo ufw deny 3306     # block MySQL port
- sudo iptables -A INPUT -p tcp --dport 5000 -j DROP

## Security Hardening


Security hardening is the process of strengthening a system’s security by reducing vulnerabilities and attack surfaces. In DevOps, it includes configuring firewalls, disabling unused services, securing SSH access, applying updates, and enforcing strict access controls. The goal is to make the system resistant to attacks and unauthorized access while maintaining performance and reliability.

**Common Hardening Practices**

- Disable unused ports and services
- Use firewall (UFW / iptables)
- Change default SSH port & disable root login
- Use SSH keys instead of passwords
- Regularly update system packages
- Enable logging and monitoring
- Limit access using IP whitelisting