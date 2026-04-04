


### 1.What is the difference between TCP and UDP? Give use cases for both in a microservices architecture.


TCP is connection-oriented, reliable, and ensures ordered delivery with error checking, while UDP is connectionless, faster, and does not guarantee delivery or order. TCP has higher overhead due to acknowledgments and retransmissions, whereas UDP is lightweight and low-latency.

Use cases in microservices:

- **TCP:** Used for critical services like REST APIs, database communication, payment systems where data reliability and consistency are required.

- **UDP:** Used for real-time features like live streaming, gaming, telemetry, logging, or service discovery where speed matters more than reliability.

### 2. How does a DNS lookup work? Trace the path from a browser to an IP address.

When you enter a URL in the browser, it first checks the local cache (browser/OS) for the IP. If not found, the request goes to a recursive DNS resolver (usually your ISP). The resolver queries root servers → TLD servers (like .com) → authoritative DNS server for that domain. The authoritative server returns the IP address. Finally, the resolver sends the IP back to the browser, which then connects to the server.
Explain the three-way handshake in TCP.

### 3. What is the difference between HTTP/1.1, HTTP/2, and gRPC?


| Feature            | HTTP/1.1                              | HTTP/2                                      | gRPC                                              |
|--------------------|----------------------------------------|----------------------------------------------|--------------------------------------------------|
| Protocol Type      | Text-based                            | Binary (framed)                              | Binary (uses HTTP/2)                             |
| Connection         | One request per connection (no multiplexing) | Multiplexing (multiple requests in one connection) | Multiplexing via HTTP/2                          |
| Performance        | Slower (head-of-line blocking)        | Faster (parallel streams, header compression)| Very fast (efficient binary + streaming)         |
| Data Format        | Plain text (JSON, HTML, etc.)         | Same as HTTP/1.1 (but optimized transport)   | Protocol Buffers (compact binary)                |
| Streaming          | Limited                               | Supports streaming                           | Full bi-directional streaming                    |
| Use Case           | Traditional web apps, REST APIs       | Modern web apps, improved REST APIs          | Microservices communication, low latency systems |
| Latency            | Higher                                | Lower                                       | Very low                                         |
| Browser Support    | Fully supported                       | Fully supported                             | Not directly (needs proxy like gRPC-Web)         |
| Complexity         | Simple                                | Moderate                                    | Higher (requires proto files & code generation)  |
| Example Usage      | Basic websites, legacy systems        | Faster APIs, CDNs                            | Internal service-to-service communication        |


### 4. What are Sticky Sessions (Session Affinity) in load balancing?

Sticky Sessions (Session Affinity) is a load balancing technique where a user’s requests are consistently routed to the same backend server. This is typically done using cookies, IP hashing, or session IDs. It helps maintain user session state (like login or shopping cart data) without needing shared storage. However, it can reduce scalability and fault tolerance because if the server goes down, the session may be lost. Modern architectures often avoid sticky sessions by using centralized session stores like Redis.

### 5. Explain CIDR notation. What does /24 or /16 mean in a subnet?

CIDR (Classless Inter-Domain Routing) is a method to represent IP addresses with a network prefix. The “/” value (like /24 or /16) indicates how many bits are used for the network portion of the IP. For example, /24 means the first 24 bits are network bits and the remaining 8 bits are for hosts (256 total addresses). Similarly, /16 means 16 network bits and 16 host bits (65,536 addresses). A larger prefix (like /24 → /28) means fewer hosts but more subnets. CIDR helps in efficient IP allocation and routing.

### 6. What is ARP (Address Resolution Protocol) and how does it work?

ARP (Address Resolution Protocol) is used to map an IP address to a MAC address within a local network. When a device wants to communicate, it checks its ARP cache for the MAC of the target IP. If not found, it sends a broadcast ARP request asking “Who has this IP?”. The device with that IP replies with its MAC address (ARP reply). The sender stores this mapping in its ARP cache for future use. This allows proper delivery of data frames at the data link layer.

### 7. What is RARP (Reverse Address Resolution Protocol) and how does it work?

RARP (Reverse Address Resolution Protocol) is used to map a MAC address to an IP address, essentially the opposite of ARP. It was mainly used by diskless machines to discover their IP address at boot time. The device broadcasts a RARP request containing its MAC address on the network. A RARP server listens and responds with the corresponding IP address. The client then configures itself using that IP. RARP is now obsolete and has been replaced by protocols like DHCP, which provide more features.

### 8. Describe the purpose of ICMP. Which common tools use it?

ICMP (Internet Control Message Protocol) is used for network diagnostics and error reporting in IP networks. It helps devices communicate issues like unreachable hosts, time exceeded, or routing problems. ICMP does not carry application data but supports network reliability and troubleshooting. It is mainly used by tools like Ping, which checks connectivity between two hosts. Another tool is Traceroute, which tracks the path packets take across networks. Routers and servers use ICMP messages to inform senders about delivery failures. Overall, ICMP is essential for monitoring and debugging network health.

# 9. What is MTU (Maximum Transmission Unit), and why does it matter for VPNs or Tunnels?

MTU (Maximum Transmission Unit) is the maximum size of a data packet that can be transmitted over a network without fragmentation. For example, Ethernet typically has an MTU of 1500 bytes. If a packet exceeds the MTU, it must be fragmented or dropped.

In VPNs or tunnels, extra headers (encryption, encapsulation) increase packet size. This reduces the effective MTU, leading to fragmentation if not adjusted properly. Fragmentation can cause performance issues, packet loss, or latency.

To avoid this, MTU is often lowered in VPN configurations or Path MTU Discovery is used. Proper MTU tuning ensures efficient and reliable communication over tunnels.

## 10. Explain the OSI Model and which layers a DevOps engineer interacts with most.

The OSI (Open Systems Interconnection) Model is a 7-layer framework that standardizes how data flows across a network. The layers are: Physical, Data Link, Network, Transport, Session, Presentation, and Application. Each layer has a specific role, from transmitting raw bits to handling user-level protocols.

A DevOps engineer mainly works with the Application layer (HTTP, APIs, microservices), Transport layer (TCP/UDP, ports), and Network layer (IP, routing, DNS). They also interact with the Data Link layer in cloud networking (VPCs, subnets, MAC-level concepts).

In real-world DevOps, most troubleshooting and system design revolves around Layers 3–7, especially for debugging latency, connectivity, and service communication issues.

## 11. What is load balancer ?

A load balancer is a system that distributes incoming network traffic across multiple servers. It ensures no single server gets overloaded, improving performance and reliability. It can operate at different layers (Layer 4 – TCP/UDP or Layer 7 – HTTP/HTTPS). Load balancers also perform health checks to route traffic only to healthy servers. This helps achieve high availability and scalability in applications.

## 12. How load balancer ensure availability ?

A load balancer ensures availability by distributing traffic across multiple backend servers instead of relying on a single one. It continuously performs health checks and removes unhealthy or failed servers from the pool. If one server goes down, traffic is automatically redirected to healthy instances. It can also scale by adding new servers during high load. This prevents downtime and keeps the application accessible to users.

## 13. What is the difference between L4 (Transport) and L7 (Application) Load Balancing? 


| Feature          | L4 (Transport Layer)                     | L7 (Application Layer)                        |
|------------------|------------------------------------------|----------------------------------------------|
| Layer            | Works at Layer 4 (TCP/UDP)               | Works at Layer 7 (HTTP/HTTPS)                |
| Decision Basis   | IP address, port                         | URL path, headers, cookies, content          |
| Performance      | Faster, low latency (no deep inspection) | Slightly slower (inspects request content)   |
| Routing Type     | Simple routing                           | Advanced routing (path-based, host-based)    |
| Protocol Support | TCP, UDP                                 | HTTP, HTTPS, WebSockets                      |
| Use Case         | High-speed traffic, gaming, streaming    | Web apps, microservices, API gateways        |
| Flexibility      | Limited                                  | Highly flexible                              |
| Example          | TCP Load Balancer (NLB)                  | Reverse Proxy (NGINX, ALB)                   |

## 14. Explain the Round Robin vs. Least Connections algorithms.

Round Robin distributes requests sequentially across all servers in a circular order, regardless of their current load. It is simple, fast, and works well when all servers have similar capacity. However, it does not consider active connections, so some servers may get overloaded.

Least Connections, on the other hand, sends traffic to the server with the fewest active connections. It dynamically balances load based on real-time usage. This makes it more efficient for applications with uneven or long-lived requests.

Round Robin is best for uniform workloads, while Least Connections is better for variable traffic and better resource utilization.

## 15. What is a Reverse Proxy, and how does it differ from a Forward Proxy?

A Reverse Proxy sits in front of backend servers and handles client requests on their behalf. It forwards requests to the appropriate server and returns the response, hiding backend details. It is used for load balancing, SSL termination, caching, and security (e.g., NGINX).

A Forward Proxy sits between clients and the internet, acting on behalf of the client. It hides the client’s identity and is often used for filtering, anonymity, or accessing restricted content.

Key difference: Reverse proxy protects and manages servers, while forward proxy represents and controls clients.

## 16. How does Global Server Load Balancing (GSLB) work for multi-region apps?

Global Server Load Balancing (GSLB) distributes user traffic across multiple geographic regions using DNS. When a user makes a request, GSLB resolves the domain to the best regional server based on factors like latency, location, or health. It performs health checks to ensure traffic is only routed to available regions.

If one region fails, traffic is automatically redirected to another healthy region (failover). It can also use policies like geo-routing or weighted routing. This ensures high availability, low latency, and better user experience for multi-region applications.

## 17. What is a Health Check? Difference between "Liveness" and "Readiness" checks?

A Health Check is a mechanism used by load balancers or orchestrators (like Kubernetes) to determine if a service instance is functioning properly. It periodically sends requests to check the status of an application.

Liveness Check verifies if the application is still running (not stuck or crashed). If it fails, the system restarts the container or service.

Readiness Check determines if the application is ready to handle traffic. If it fails, the instance is temporarily removed from load balancing but not restarted.

In short, liveness = should it be restarted?, readiness = should it receive traffic?.

## 18. Explain SSL Termination vs. SSL Passthrough.

SSL Termination vs SSL Passthrough

- SSL Termination means the load balancer decrypts HTTPS traffic and forwards plain HTTP to backend servers.
- This reduces CPU load on servers and allows features like caching, routing, and header inspection.
- It also simplifies certificate management since SSL is handled at one point (the load balancer).
- SSL Passthrough means encrypted traffic is passed directly to backend servers without decryption.
- The load balancer only routes based on IP/port (Layer 4), not content.
- Backend servers handle SSL decryption and certificate management.

In short: Termination = better performance & control; Passthrough = end-to-end encryption but less flexibility.

## 19. What is Anycast IP and how is it used in CDNs?

Anycast IP is a networking technique where the same IP address is advertised from multiple geographically distributed servers. When a user sends a request, routing protocols (like BGP) direct it to the nearest or best-performing server.

In CDNs, Anycast allows users to connect to the closest edge location automatically, reducing latency. Multiple servers share the same IP, but traffic is routed based on network proximity and health.

If one node fails, traffic is automatically redirected to another available node without changing the IP. This improves fault tolerance and availability.

Anycast is widely used by CDNs, DNS providers, and large-scale distributed systems to deliver fast and reliable content globally.

## 20. Describe the role of Nginx or HAProxy in a DevOps stack.

Nginx and HAProxy act as high-performance reverse proxies and load balancers in modern architectures. They sit in front of applications to distribute traffic across multiple backend services. They improve scalability and availability by preventing any single server from being overloaded.

They handle SSL termination, reducing encryption overhead on application servers. They also provide features like caching, compression, and request routing.

In microservices, they are often used as API gateways or ingress controllers (e.g., in Kubernetes). Overall, they are critical for performance optimization, security, and traffic management in a DevOps stack.

## 21. What is a Virtual IP (VIP)?

A Virtual IP (VIP) is an IP address that does not belong to a single physical machine but is shared by multiple servers. It is commonly used in load balancing and high-availability setups. Clients send requests to the VIP instead of individual server IPs.

The VIP is managed by a load balancer or clustering system, which forwards traffic to available backend servers. If one server fails, another server can take over the VIP without changing the client’s connection point.

This ensures seamless failover, high availability, and easier service access using a single stable IP address.

## 22. How do you prevent a "Single Point of Failure" in a networking setup?

To prevent a Single Point of Failure (SPOF), systems are designed with redundancy at every critical layer. Multiple servers are deployed behind a load balancer so traffic can be distributed and failover handled automatically.

Use redundant load balancers (active-passive or active-active) with a Virtual IP (VIP) to avoid the load balancer itself becoming a SPOF. Data is replicated across databases (primary-replica or multi-region setups) to ensure availability.

Network redundancy is achieved using multiple routers, switches, and internet links. Health checks and automatic failover mechanisms ensure traffic shifts instantly when a component fails.

Additionally, use DNS-based failover, Anycast routing, and cloud multi-AZ/multi-region deployments. This layered redundancy ensures high availability and fault tolerance.

## 23. What is Port Forwarding and when do you use it? 

Port Forwarding is a networking technique that maps an external (public) IP address and port to an internal (private) IP and port. It is commonly configured on routers or firewalls. When a request comes to a specific port, it is forwarded to the designated internal service.

It is used to expose services like web servers, SSH, or game servers running inside a private network to the internet. It helps access internal resources from outside without revealing the entire network.

Port forwarding is also useful in home networks, NAT environments, and for remote access setups.

## 24. What is the difference between TLS and SSL?


| Feature            | SSL (Secure Sockets Layer)                  | TLS (Transport Layer Security)                |
|--------------------|---------------------------------------------|----------------------------------------------|
| Version            | Older protocol (SSL 2.0, 3.0)              | Modern protocol (TLS 1.0 → 1.3)              |
| Security           | Less secure (known vulnerabilities)        | More secure with stronger encryption         |
| Performance        | Slower                                    | Faster and more efficient                    |
| Encryption         | Basic encryption algorithms                | Advanced encryption (AES, ChaCha20, etc.)   |
| Handshake          | Complex and less secure                    | Improved and secure handshake process        |
| Usage              | Deprecated and no longer recommended       | Widely used in modern HTTPS communication    |
| Compatibility      | Supported in legacy systems                | Supported in all modern systems              |
| Example            | Old HTTPS implementations                  | Current HTTPS, secure APIs, web apps         |

## 25. How does a WAF (Web Application Firewall) protect an application?

A WAF (Web Application Firewall) protects applications by filtering and monitoring HTTP/HTTPS traffic between clients and servers. It inspects incoming requests at the application layer (Layer 7) to detect malicious patterns.

It helps prevent common attacks like SQL Injection, Cross-Site Scripting (XSS), and CSRF. WAFs use rules, signatures, and behavior analysis to block suspicious requests.

They can also enforce rate limiting to prevent DDoS or brute-force attacks. Many WAFs provide IP blocking, geo-filtering, and bot protection.

Additionally, WAFs log and monitor traffic for security analysis and compliance. Overall, they act as a protective shield in front of web applications, enhancing security without modifying code.

## 26. Explain DDoS and common mitigation strategies.

A DDoS (Distributed Denial of Service) attack floods a server or network with massive traffic from multiple sources, making it unavailable to legitimate users. Attackers use botnets (compromised devices) to generate this traffic.

There are different types like volumetric attacks (traffic flooding), protocol attacks (SYN flood), and application-layer attacks (HTTP floods). The goal is to exhaust bandwidth, CPU, or server resources.

Mitigation strategies include using CDNs and Anycast to absorb and distribute traffic globally. Rate limiting and throttling help control excessive requests. WAFs and firewalls block malicious patterns and IPs.

Load balancing and auto-scaling handle traffic spikes, while monitoring and anomaly detection identify attacks early. Dedicated DDoS protection services (like AWS Shield, Cloudflare) provide advanced defense mechanisms.

Mitigation strategies:

- Use CDNs and Anycast to absorb and distribute traffic globally.

- Implement rate limiting and throttling to control excessive requests.

- Deploy WAFs and firewalls to filter malicious traffic patterns.

- Use load balancing and auto-scaling to handle traffic spikes.

- Enable DDoS protection services (e.g., AWS Shield, Cloudflare).

- Monitor traffic and use anomaly detection to identify attacks early.

## 27. What is IP Whitelisting and why is it often considered a "weak" security measure? 

IP Whitelisting is a security method where only specific trusted IP addresses are allowed to access a system or service, while all others are blocked. It is commonly used for admin panels, APIs, or internal tools.

However, it is considered a weak security measure because IP addresses can be spoofed or compromised. In many networks (like ISPs or mobile users), IPs are dynamic and can change frequently. If an attacker gains access to a whitelisted network (e.g., via VPN or internal breach), they can bypass restrictions.

It also lacks user-level authentication and does not verify identity—only location. Therefore, it should be used as an additional layer, not as the primary security control.

## 28. How do you troubleshoot a DNS resolution issue on a Linux server?

To troubleshoot a DNS resolution issue on a Linux server, follow a systematic approach:

- Check basic connectivity using `ping 8.8.8.8` to confirm network access (IP works).
- Try `ping google.com` to see if DNS resolution fails (name vs IP issue).
- Verify DNS configuration in /etc/resolv.conf (nameserver entries).
- Use `dig google.com` or `nslookup google.com` to test DNS queries directly.
- Check if the DNS server is reachable (`ping <DNS_IP>`).
- Restart DNS-related services like systemd-resolved or networking.
- Clear DNS cache (`sudo systemd-resolve --flush-caches`).
- Inspect /etc/hosts for incorrect manual mappings.
- Check firewall rules (iptables / ufw) blocking port 53.
- Verify /etc/nsswitch.conf for correct lookup order (hosts: files dns).
- Test with a public DNS (8.8.8.8) temporarily.
- Look at logs (`journalctl -u systemd-resolved`) for errors.
- If in cloud/VPC, check security groups and DNS settings.

## 29. Which tool would you use to trace the hops a packet takes? (Traceroute/MTR). 

To trace the hops a packet takes across a network, you can use Traceroute or MTR (My Traceroute).

Traceroute shows the path packets take by listing each router (hop) between source and destination. It also displays the time taken for each hop, helping identify delays or failures. It is useful for basic, one-time diagnostics.

MTR combines Traceroute and Ping, providing real-time, continuous updates of latency and packet loss for each hop. This makes it more powerful for debugging intermittent network issues.

In short, Traceroute is good for quick checks, while MTR is better for detailed and ongoing network analysis.

## 30. How do you check if a specific port is open on a remote server? (nc, telnet, nmap). 

To check if a specific port is open on a remote server, you can use several tools:

**nc (Netcat):**
- Run `nc -zv <host> <port>` to check connectivity. It shows if the port is open or closed quickly.
**telnet:**
- Use `telnet <host> <port>`. If it connects, the port is open; if it fails, it’s closed or blocked.
**nmap:**
- Run `nmap -p <port> <host>` for a detailed scan. It tells whether the port is open, closed, or filtered.

These tools help diagnose firewall issues, service availability, and network connectivity problems.

## 31. What is packet sniffing, and which tool is best for it? (tcpdump, Wireshark). 

Packet sniffing is the process of capturing and analyzing network packets flowing through a network interface. It helps in debugging network issues, monitoring traffic, and detecting security threats. By inspecting packet headers and payloads, you can understand protocols, latency, and failures.

`tcpdump` is a command-line tool that captures packets in real time and is lightweight, making it ideal for servers and quick diagnostics. It allows filtering by IP, port, or protocol.

`Wireshark` is a GUI-based tool that provides deep packet analysis with detailed visualization and decoding of protocols. It is best for in-depth analysis and troubleshooting.

In short, tcpdump is best for quick, server-side captures, while Wireshark is best for detailed, visual inspection.

## 32. Explain the concept of Zero Trust Networking. 

Zero Trust Networking is a security model based on the principle “never trust, always verify.” It assumes no user, device, or network is trusted by default, even inside the internal network.

Every access request must be authenticated, authorized, and continuously validated before granting access. It uses strong identity verification, multi-factor authentication (MFA), and strict access controls.

Access is granted on a least privilege basis, meaning users only get the minimum permissions required. Network segmentation is used to limit lateral movement within systems.

It also involves continuous monitoring, logging, and threat detection. Overall, Zero Trust improves security by reducing reliance on perimeter-based defenses.

## 33. What happens if two devices on a network have the same IP address? 

If two devices on the same network have the same IP address, it creates an IP address conflict. Both devices will compete to respond to network requests, causing confusion in routing.

This leads to unstable connectivity—packets may go to the wrong device or get dropped. Users may experience intermittent network access or complete disconnection.

ARP tables can become inconsistent, as the same IP maps to different MAC addresses. This results in frequent updates and network instability.

Most operating systems detect the conflict and show warnings. To fix it, one device must be assigned a unique IP (via DHCP or manual configuration).

## 34. 	How do you handle overlapping IP ranges when connecting two different companies' networks? (Advanced Question)

When two networks have overlapping IP ranges (e.g., both use 10.0.0.0/8), direct routing between them causes conflicts. To handle this, NAT (Network Address Translation) is commonly used. One network’s IP range is translated into a different, non-overlapping range before communication.

Another approach is re-IPing, where one network is renumbered to a new IP range, though this can be complex and disruptive.

You can also use VPN with NAT (NAT-T) or policy-based routing to map specific subnets and avoid conflicts. In cloud environments, VPC peering with CIDR translation or Transit Gateway with NAT is often used.

Using proxy servers or application-layer gateways is another workaround when only specific services need access.

The best approach depends on scale, downtime tolerance, and control over network infrastructure.

## 35. How would you implement a Blue-Green deployment using a Load Balancer? 

Blue-Green deployment uses two identical environments: Blue (current live) and Green (new version) behind a load balancer.

First, deploy the new application version to the Green environment while Blue continues serving users. Run tests and health checks on Green to ensure stability.

Once verified, update the load balancer to shift traffic from Blue to Green (either instantly or gradually). This switch makes the new version live with minimal downtime.

If any issues occur, you can quickly roll back by routing traffic back to Blue. This approach ensures safe deployments, easy rollback, and zero/near-zero downtime.

## 36. How do you manage SSL/TLS certificates automatically? (e.g., Cert-manager or AWS ACM). 

To manage SSL/TLS certificates automatically, tools like Cert-Manager and AWS ACM (AWS Certificate Manager) are widely used.

Cert-Manager (Kubernetes):
It automates certificate issuance, renewal, and management داخل Kubernetes clusters. It integrates with certificate authorities like Let’s Encrypt using ACME protocol. You define resources like Certificate and Issuer, and Cert-Manager handles the lifecycle automatically. It also updates secrets and reloads ingress controllers when certificates renew.

AWS ACM:
AWS ACM provisions and manages SSL/TLS certificates for services like ELB, CloudFront, and API Gateway. It automatically renews certificates before expiration with no downtime. Certificates are securely stored and integrated directly with AWS services.

Both tools eliminate manual certificate handling, reducing human error and downtime. They ensure continuous HTTPS security by auto-renewing certificates.

In production, you combine them with monitoring and alerts to track certificate health and expiration.

## 37.	What is a BGP (Border Gateway Protocol), and why is it important for hybrid cloud connectivity? (Advanced Question)

BGP (Border Gateway Protocol) is a path-vector routing protocol used to exchange routing information between different networks (Autonomous Systems) on the internet. It determines the best path for data based on policies, path attributes, and network rules.

In hybrid cloud setups (on-prem + cloud), BGP is used with services like VPN or Direct Connect/ExpressRoute to dynamically share routes between environments. This avoids manual route configuration and enables automatic updates when network changes occur.

BGP provides high availability by rerouting traffic if a link fails and supports load balancing across multiple paths. It also allows fine-grained control over routing policies.

Overall, BGP is crucial for scalable, reliable, and flexible connectivity in hybrid and multi-cloud architectures.

## 38. 	What is Network Latency, and how do you measure it in a distributed system? 7-9 lines

Network latency is the time it takes for a data packet to travel from source to destination and back (round-trip time). It directly affects application performance, especially in distributed systems.

It can be measured using tools like ping, which shows RTT (round-trip time) between nodes. Traceroute/MTR help identify latency at each hop in the network path.

At the application level, monitoring tools (Prometheus, Grafana, APMs) measure request-response times between services. You can also use synthetic tests or health checks across regions.

Metrics like p50, p95, and p99 latency are used to understand performance distribution. Continuous monitoring helps detect bottlenecks and optimize system performance.


## 39. Explain the difference between Throughput and Bandwidth.


| Feature        | Bandwidth                                      | Throughput                                      |
|----------------|-----------------------------------------------|------------------------------------------------|
| Definition     | Maximum data transfer capacity of a network   | Actual data transferred successfully over time |
| Nature         | Theoretical limit                             | Real-world performance                          |
| Unit           | Bits per second (bps)                         | Bits per second (bps)                           |
| Dependency     | Depends on network infrastructure             | Affected by latency, congestion, packet loss    |
| Measurement    | Defined by ISP or network capability          | Measured using tools (iperf, speed tests)       |
| Performance    | Higher bandwidth ≠ always higher throughput   | Reflects actual user experience                 |
| Example        | 100 Mbps link capacity                        | 60 Mbps actual data transfer                    |

## 40. Explain the difference between TCP and UDP. 


| Feature            | TCP (Transmission Control Protocol)           | UDP (User Datagram Protocol)                |
|--------------------|-----------------------------------------------|--------------------------------------------|
| Connection Type    | Connection-oriented                           | Connectionless                             |
| Reliability        | Reliable (guarantees delivery)                | Unreliable (no guarantee of delivery)      |
| Ordering           | Ensures ordered delivery                      | No ordering guarantee                      |
| Error Handling     | Error detection + retransmission              | Error detection only (no retransmission)   |
| Speed              | Slower (due to overhead)                      | Faster (low overhead)                      |
| Overhead           | High (acknowledgments, handshakes)            | Low                                        |
| Flow Control       | Yes                                           | No                                         |
| Use Cases          | Web, APIs, file transfer, databases           | Streaming, gaming, VoIP, DNS               |
| Example Protocols  | HTTP, HTTPS, FTP, SMTP                        | DNS, DHCP, RTP                            |


## 41. What is the CIA Triad in security? 

The CIA Triad is a core security model that stands for Confidentiality, Integrity, and Availability.

- Confidentiality: Ensures that sensitive data is accessible only to authorized users (e.g., encryption, access control).

- Integrity: Ensures data is accurate and not altered or tampered with (e.g., hashing, checksums).

- Availability: Ensures systems and data are accessible when needed (e.g., redundancy, load balancing).

Together, these three principles form the foundation of designing secure systems.

## 42. How does a reverse proxy improve security? 

A reverse proxy improves security by hiding backend server details from clients, reducing direct exposure. It can filter and block malicious requests before they reach the application. It enables SSL/TLS termination, ensuring encrypted communication. Reverse proxies also provide rate limiting and DDoS protection. They can integrate with WAFs to prevent attacks like SQL injection and XSS. Overall, it acts as a protective layer between users and servers.

## 43. How does multi-factor authentication (MFA) enhance security? 

Multi-factor authentication (MFA) enhances security by requiring users to verify their identity using two or more factors instead of just a password. These factors typically include something you know (password), something you have (OTP, mobile device, security token ), and something you are (biometrics).

Even if an attacker steals a password, they cannot access the system without the second factor. This significantly reduces the risk of account compromise from phishing, brute-force, or credential leaks.

MFA also adds protection for sensitive operations like payments or admin access. Modern systems use app-based OTPs, push notifications, or hardware tokens.

Overall, MFA provides an extra layer of defense, making unauthorized access much harder.

## 44. What is a honeypot in cybersecurity?

A honeypot is a security mechanism that acts as a decoy system to attract and detect attackers. It mimics real services or vulnerabilities to lure malicious users away from actual systems.

When attackers interact with the honeypot, their actions are monitored and logged for analysis. This helps security teams understand attack patterns, tools, and techniques.

Honeypots can be low-interaction (basic simulation) or high-interaction (realistic systems). They are isolated to prevent attackers from using them to access real infrastructure.

Overall, honeypots are used for threat detection, research, and improving security defenses.

## 45. What is SSO (Single Sign-On)? 

SSO (Single Sign-On) is an authentication mechanism that allows a user to log in once and gain access to multiple applications or services without re-entering credentials.

It works by authenticating the user with a central identity provider (IdP), which then issues a token or session used across different systems.

Common protocols used in SSO include SAML, OAuth, and OpenID Connect.

SSO improves user experience (fewer logins) and enhances security by centralizing authentication and enabling features like MFA.

## 46.  What is a security token?

A security token is a digital credential used to authenticate and authorize a user or system. It represents identity and permissions, allowing access to resources without repeatedly sending credentials.

Tokens are typically issued after successful login by an authentication server (e.g., in OAuth or JWT-based systems). They contain information like user ID, roles, and expiration time.

There are different types, such as access tokens, refresh tokens, and ID tokens. Tokens can be stored in cookies or headers and are validated by servers on each request.

Overall, security tokens enable secure, stateless authentication in modern applications.

## 47. What is a bastion host?

A bastion host (also called a jump server) is a special-purpose server used to securely access systems inside a private network. It acts as a single, controlled entry point from the public internet to internal resources.

The bastion host is typically placed in a public subnet and hardened with strict security measures. It allows administrators to connect (usually via SSH) and then access private servers that are not directly exposed to the internet.

Only specific IPs, users, and ports are allowed to connect to the bastion host, reducing the attack surface. It often uses strong authentication methods like SSH keys and multi-factor authentication (MFA).

Once connected to the bastion, users can “jump” into internal servers using private IPs. This avoids exposing sensitive systems directly to the public internet.

**Example:**
In AWS, you launch an EC2 instance as a bastion host in a public subnet. Your private EC2 instances (in private subnets) do not have public IPs. You SSH into the bastion host first, and from there SSH into private instances.

This setup improves security, centralizes access control, and enables monitoring/logging of all administrative access.

## 48. What is a DMZ in networking? 

A DMZ (Demilitarized Zone) is a network segment that sits between a trusted internal network and an untrusted external network (like the internet). It is used to host public-facing services while protecting the internal network.

Systems in the DMZ are isolated so that even if they are compromised, attackers cannot easily access internal resources. Firewalls control traffic between Internet ↔ DMZ ↔ Internal Network with strict rules.

Example:
A company hosts its web server in the DMZ. Users from the internet can access the web server, but the web server cannot directly access the internal database server. If needed, only limited and controlled communication is allowed (e.g., specific ports).

This setup improves security by creating a buffer zone and reducing the risk of internal network exposure.

## 49. What is Intrusion Detection System (IDS) ?

An Intrusion Detection System (IDS) is a security tool that monitors network or system traffic for suspicious or malicious activity. It analyzes packets and logs to detect known attack patterns or anomalies. IDS operates in a passive mode and does not block traffic, only generates alerts. It helps security teams identify threats and investigate incidents. Common types include network-based IDS (NIDS) and host-based IDS (HIDS).

## 50. What is Intrusion Prevention System (IPS) ?

An Intrusion Prevention System (IPS) is a security tool that monitors network traffic in real time and actively blocks malicious activity. It is placed inline in the network, allowing it to inspect and control traffic flow. IPS detects threats using signatures, anomaly detection, and behavior analysis. When a threat is identified, it can drop packets, block IPs, or terminate connections. It helps prevent attacks like SQL injection, DDoS, and exploits. Overall, IPS provides proactive protection by stopping threats before they reach systems.

## 51. What is network segmentation?

Network segmentation is the practice of dividing a network into smaller, isolated segments or subnets to improve security and performance. It limits access between segments using firewalls, VLANs, or access control policies.

If one segment is compromised, attackers cannot easily move laterally to other parts of the network. It also helps reduce congestion and improve traffic management.

Network segmentation is commonly used in enterprises, cloud environments, and Zero Trust architectures to enhance security and control.

## 52. What is an access control list (ACL)? 

An Access Control List (ACL) is a set of rules used to control incoming and outgoing network traffic. It defines which users, IP addresses, or protocols are allowed or denied access to a network resource.

ACLs are commonly configured on routers, switches, and firewalls. They work by evaluating traffic against rules in order (top to bottom) and applying the first matching rule.

They can filter traffic based on IP address, port number, or protocol (TCP/UDP). Overall, ACLs help enforce security policies and restrict unauthorized access.

## 53. What is a container network security concern?

Container network security concerns arise because containers share the same host network and kernel, increasing the risk of lateral movement if one container is compromised. Misconfigured network policies can allow unauthorized communication between services. Exposed container ports or insecure APIs can be targeted by attackers.

Another concern is lack of proper isolation between containers, especially in flat networks where all services can talk to each other. Attackers can exploit this to move across microservices.

Example: If a compromised container in a Kubernetes cluster can freely access a database service due to missing network policies, sensitive data may be exposed.

To mitigate this, use network segmentation, Kubernetes NetworkPolicies, service meshes, and enforce least-privilege communication between containers.

## 54. What is reconnaissance and why we use it ?

Reconnaissance is the process of gathering information about a target system, network, or organization before performing any attack or security testing. It is the first phase in cybersecurity (also called footprinting).

It is used to identify details like IP addresses, domains, network structure, technologies used, and potential vulnerabilities. This helps attackers plan effective attacks or helps security professionals find weaknesses during penetration testing.

In short, reconnaissance provides the intelligence needed to understand a target and prepare the next steps.

## 55. What is the difference between active and passive reconnaissance? 

- **Active Reconnaissance:** Directly interacts with the target system (e.g., scanning ports with Nmap, sending requests). It provides detailed and accurate data but is detectable by security systems (logs, IDS/IPS alerts).

- **Passive Reconnaissance:** Gathers information without directly interacting with the target (e.g., WHOIS lookup, public DNS records, social media). It is stealthy and hard to detect, but the information may be limited or outdated.

In short: Active = direct + detectable, Passive = indirect + stealthy.

## 56. 









3. Cloud Networking (AWS/Azure/GCP Focus)
What is a VPC (Virtual Private Cloud)?

Difference between a Public Subnet and a Private Subnet.

What is a NAT Gateway, and why is it used in private subnets?

Explain VPC Peering and its limitations (e.g., transitive routing).

What is a Security Group vs. a Network ACL (NACL)? Which one is stateful?

How do you connect an on-premise data center to the cloud? (VPN vs. Direct Connect).

What is an Internet Gateway (IGW)?

Explain the concept of an Egress-only Internet Gateway.

What is an Endpoint (Interface vs. Gateway) in the context of cloud services?

How would you debug a "Connection Timeout" between two instances in different subnets?

4. Container & Kubernetes Networking
What is the CNI (Container Network Interface)?

How do Pods communicate with each other in Kubernetes?

Explain the difference between ClusterIP, NodePort, and LoadBalancer services.

What is a Kubernetes Ingress Controller?

What is a Service Mesh (e.g., Istio, Linkerd), and why is it needed?

Describe Sidecar Proxy pattern in networking.

What is CoreDNS in a Kubernetes cluster?

Explain Network Policies in Kubernetes.

What is Port Forwarding and when do you use it?

How does Docker Bridge Networking work?

