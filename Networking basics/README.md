# What is a Network?

![alt text](< Network.png >)

A network is a collection of two or more computers or devices connected together so they can share data, resources, and services. These devices communicate using transmission media like cables (Ethernet, fiber optic) or wireless signals (Wi-Fi, radio waves). Networks allow users to share files, printers, internet connections, and applications efficiently.

In simple terms, a network enables communication between devices using defined rules called protocols (like TCP/IP). Every device in a network has an IP address that helps identify it uniquely. Networks can exist within a single room, across cities, or even worldwide.

---

## LAN (Local Area Network)

A LAN is a network that covers a small geographical area like a home, office, school, or building. It is privately owned and usually managed by one organization. LAN provides high-speed connectivity (100 Mbps to 10 Gbps or more) because devices are located close to each other.

In a LAN, devices are connected using Ethernet cables or Wi-Fi. It is cost-effective and easy to maintain. Since it operates in a limited area, it provides better security control and low latency communication. Most modern offices use LAN for internal communication and file sharing.

---

## MAN (Metropolitan Area Network)

A MAN connects multiple LANs within a city or metropolitan region. It is larger than LAN but smaller than WAN. Telecom companies or large organizations typically manage MAN networks.

For example, a university with multiple campuses across a city may use a MAN to connect all campuses. It provides high-speed connectivity across city distances and often uses fiber-optic cables.

### Key Points

- Covers a city
- Connects multiple LANs
- Managed by telecom or large organization
- Medium cost and speed

---

## WAN (Wide Area Network)

A WAN spans large geographical areas like countries or continents. It connects multiple LANs and MANs together. WAN uses leased telecom lines, satellite links, and fiber networks.

The biggest example of WAN is the Internet. WAN is more expensive and has higher latency compared to LAN. Companies use WAN to connect branch offices across different cities or countries.

### Key Points

- Covers countries/continents
- Connects LANs & MANs
- Higher latency
- Expensive infrastructure

---

## LAN vs MAN vs WAN (Quick Difference Table)

| Feature  | LAN            | MAN                 | WAN      |
| -------- | -------------- | ------------------- | -------- |
| Coverage | Small          | City                | Global   |
| Speed    | Very High      | High                | Medium   |
| Cost     | Low            | Medium              | High     |
| Example  | Office Network | City Campus Network | Internet |

## Internet

The Internet is a global public network that connects millions of private, public, academic, business, and government networks worldwide. It is not owned by a single person or organization.

Instead, it is a network of networks using TCP/IP protocol.
Anyone can access the internet using an ISP (Internet Service Provider). Websites, emails, cloud services, streaming platforms — all operate over the internet.

### Key Points

- Global public network
- Accessible to everyone

---

## Intranet

An Intranet is a private network used within an organization. It works like the internet but access is restricted to authorized users only.

For example, a company may have an internal HR portal accessible only to employees. It improves internal communication and data sharing while maintaining privacy. It is more secure than internet.

---

## Internet vs Intranet vs VPN

| Feature   | Internet        | Intranet           | VPN                        |
| --------- | --------------- | ------------------ | -------------------------- |
| Access    | Public          | Private            | Secure private over public |
| Ownership | No single owner | Organization owned | Service-based              |
| Security  | Moderate        | High               | Very High (encrypted)      |

## Basic Networking Devices

### 1. Router

A router is a networking device that connects multiple networks and enables communication between them. It uses IP addresses to determine the best path for forwarding data packets. Routers are essential for connecting local networks to the internet. They perform Network Address Translation (NAT) to allow multiple devices to share a single public IP. Routers often include features like DHCP to assign IP addresses automatically. They also provide basic firewall and security functionalities.

---

### 2. Switch

A switch is used to connect devices within the same local area network (LAN). It forwards data based on MAC addresses to the correct destination device. Switches improve network efficiency by reducing unnecessary traffic. They create separate collision domains for each connected device. Modern switches support VLANs for network segmentation. They are widely used in offices, data centers, and enterprise networks.

---

### 3. Hub

A hub is a simple networking device that connects multiple devices in a LAN. It broadcasts incoming data to all connected devices without filtering. This leads to unnecessary traffic and network collisions. Hubs operate at the physical layer of the OSI model. They do not have intelligence to manage or direct traffic efficiently. Due to inefficiency, hubs are now largely replaced by switches.

---

### 4. Modem

A modem is a device that connects a network to an internet service provider. It converts digital signals from computers into analog signals for transmission. It also converts incoming analog signals back into digital form. Modems are essential for establishing internet connectivity. They are commonly used in DSL, cable, and fiber connections. Modern modems are often integrated with routers in a single device.

---

### 5. Access Point (AP)

An access point enables wireless devices to connect to a wired network. It acts as a bridge between Wi-Fi devices and the LAN. Access points extend the coverage area of a wireless network. They support multiple devices simultaneously with stable connectivity. APs are commonly deployed in offices, campuses, and public spaces. They can be standalone or integrated into routers.

---

### 6. Firewall

A firewall is a security device that monitors and controls network traffic. It filters incoming and outgoing data based on predefined rules. Firewalls help protect systems from unauthorized access and cyber threats. They can block malicious traffic and allow legitimate communication. Firewalls can be hardware-based, software-based, or cloud-based. They are critical for securing enterprise and cloud environments.

---

### 7. Gateway

A gateway is a networking device that connects different networks with different protocols. It acts as a translator between incompatible systems. Gateways allow communication between networks that use different architectures. They serve as an entry and exit point for network traffic. Gateways are commonly used in enterprise and cloud setups. They often perform protocol conversion and data processing.

---

### 8. Repeater

A repeater is used to extend the range of a network by regenerating signals. It receives weak or degraded signals and amplifies them. Repeaters help maintain signal quality over long distances. They operate at the physical layer of the OSI model. They do not filter or manage traffic, only boost signals. Repeaters are commonly used in large wired and wireless networks.

## Network Topology

Network Topology refers to the arrangement and organization of devices in a computer network. It defines how components are structured and how communication is established between them.

- Describes the overall structure of a network
- Helps in network design and planning
- Influences performance and reliability
- Includes Physical Topology, which shows the actual layout of devices and cables
- Includes Logical Topology, which defines how data moves between devices

## Types of Network Topology

The arrangement of a network that comprises nodes and connecting lines via sender and receiver is referred to as Network Topology. Below are various network topologies that include:

### 1. Mesh Topology

Mesh Topology is a network structure in which each device is connected to multiple other devices, creating several communication paths within the network. It provides high redundancy and reliability.

- Devices are interconnected with dedicated links
- Supports multiple paths for data transmission
- Can be full mesh or partial mesh
  ![alt text](< Mesh.png >)

There are two types of Mesh topologies:

- **1. Full Mesh Topology:**
  In a full mesh network, every node is directly connected to all other nodes. If there are N nodes, each node has (N − 1) connections. This provides maximum redundancy and reliability.
- **2. Partial Mesh Topology:**
  In a partial mesh network, only selected nodes are interconnected. Not every node is directly connected to all others. This approach reduces cost and complexity while still maintaining reasonable reliability.

#### **Advantages**

- High fault tolerance
- Reliable data delivery
- Enhanced security due to dedicated links
- Suitable for critical network systems

#### **Disadvantages**

- Expensive to implement
- Requires large amount of cabling
- Complex installation process
- Difficult to manage in large networks

### 2. Star Topology

Star Topology is a network layout in which all devices are connected to a central device such as a switch or hub. All communication between devices passes through this central point.

- Each device has a dedicated connection to the central node
- Central device controls data transmission
- Commonly used in Local Area Networks (LANs)

![alt text](< Star.png >)

#### **Advantages**

- Easy to install and manage
- Simple fault detection and troubleshooting
- Failure of one device does not affect others
- Easy to add or remove devices

#### **Disadvantages**

- Failure of central device stops the entire network
- Requires more cabling than bus topology
- Higher installation cost
- Performance depends on central device capacity

### 3. Bus Topology

Bus Topology is a network structure in which all devices are connected to a single main communication cable called the backbone. Data sent by any device travels along this common cable and is received by the intended device.

- Uses a single backbone cable
- All devices share the same communication channel
- Terminators are placed at both ends of the cable

![alt text](< Bus.png >)

#### **Advantages**

- Simple and easy to implement
- Requires less cable compared to star topology
- Cost-effective for small networks
- Suitable for temporary network setups

#### **Disadvantages**

- Failure of backbone cable stops the entire network
- Difficult to troubleshoot issues
- Performance decreases with high traffic
- Limited scalability for large networks

### 4. Ring Topology

Ring Topology is a network configuration in which each device is connected to two other devices, forming a closed circular path. Data travels around the ring in a fixed direction until it reaches its destination.

- Forms a continuous circular structure
- Each device acts as a repeater
- Data passes through intermediate devices

![alt text](< Ring.png >)

#### **Advantages**

- Reduces chances of data collision
- Provides equal access to all devices
- Performs well under consistent traffic load
- Suitable for orderly data transmission

#### **Disadvantages**

- Failure of one device can disrupt communication
- Troubleshooting can be difficult
- Adding or removing devices affects the network
- Slower compared to some modern topologies

### 5. Tree Topology

Tree Topology is a hierarchical network structure in which multiple star networks are connected to a central backbone cable. It combines features of both bus and star topologies and organizes devices in a parent–child arrangement.

- Follows a hierarchical structure
- Consists of root node and branch nodes
- Uses a backbone cable for connection
- Suitable for large networks

![alt text](< Tree.png >)

#### **Advantages**

- Easy to expand by adding new branches
- Supports structured network management
- Fault isolation is simpler
- Scalable for growing organizations

#### **Disadvantages**

- Backbone failure affects entire network
- Requires more cabling
- Configuration is complex
- Maintenance can be challenging

### 6. Hybrid Topology

Hybrid Topology is a network structure that combines two or more different types of topologies into a single system. It is designed to meet specific organizational requirements by integrating the strengths of multiple network layouts.

- Formed by combining different topologies
- Customized according to network needs
- Common in large enterprise environments
- Supports complex network structures
  Hybrid

![alt text](< Hybrid.png >)

#### **Advantages**

- Flexible network design
- Scalable for future expansion
- Can improve reliability
- Allows optimization based on requirements

#### **Disadvantages**

- Expensive to implement
- Complex to design and manage
- Requires advanced hardware
- Maintenance can be difficult

### 7. Point to Point Topology

Point-to-Point Topology is a network configuration in which two devices are directly connected through a dedicated communication link. The connection is exclusive, meaning the entire bandwidth is used only between these two devices.

- Involves only two connected devices
- Uses a single dedicated link
- Data travels directly without intermediaries
- Simple network structure

![alt text](< P2P.png >)

#### **Advantages**

- High data transfer speed
- Secure communication channel
- Easy to configure
- Low chances of data collision

#### **Disadvantages**

- Not suitable for large networks
- Limited scalability
- Link failure stops communication
- Inefficient for multiple device connections

### 8. Daisy Chain Topology

Daisy Chain Topology is a network arrangement in which devices are connected sequentially, one after another, forming a linear chain. Each device is linked to the next device in the sequence.

- Devices are connected in series
- Data passes through intermediate devices
- Simple linear structure
- Often used in small or temporary networks

![alt text](< Daisy.png >)

#### **Advantages**

- Easy to set up
- Requires less cabling than complex topologies
- Cost-effective for limited devices
- Simple expansion by adding devices at the end

#### **Disadvantages**

- Failure of one device can disrupt the chain
- Performance decreases as more devices are added
- Difficult to troubleshoot faults
- Not suitable for large-scale networks
