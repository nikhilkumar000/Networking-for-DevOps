# UDP (User Datagram Protocol)

UDP (User Datagram Protocol) is a transport layer protocol used in the TCP/IP Model for sending data between devices over a network in a fast but unreliable way.

 Unlike Transmission Control Protocol, UDP does not establish a connection before sending data and does not guarantee delivery, order, or error correction. It simply sends data packets (called datagrams) from sender to receiver without checking whether they arrive successfully. 
 
 Because of this, UDP is very fast and lightweight, making it suitable for real-time applications like video streaming, online gaming, VoIP calls, and DNS queries where speed is more important than reliability.

 ## Working of UDP

 UDP (User Datagram Protocol) works in a very simple and fast way because it does not establish a connection like Transmission Control Protocol. Below is the step-by-step working:

 ### Step 1: Application Sends Data

An application (like video streaming, gaming, or DNS) wants to send data.

#### Example:

- Video call app sending voice data
- DNS request to find a website IP

The application passes data to UDP.

### Step 2: UDP Adds Header

UDP creates a datagram by adding a small header to the data.

Header contains:

- Source Port
- Destination Port
- Length
- Checksum (basic error check)

UDP header is very small → makes it fast.

### Step 3: No Connection Setup

Unlike TCP, UDP does not perform a handshake.

- No SYN
- No ACK
- No connection establishment

 Data is sent immediately without waiting.

### Step 4: Data Sent to IP Layer

UDP passes the datagram to Internet Protocol.

- IP adds its own header (IP address)
- Packet is sent into the network

### Step 5: Data Travels Through Network

Packets move through:

Sender → Router → Internet → Receiver
- Each packet travels independently
- Packets may take different routes
- Some packets may be lost

### Step 6: No Acknowledgement

UDP does not wait for any response.

- No ACK from receiver
- Sender does not know if data arrived or not

 This makes UDP very fast.

### Step 7: Receiver Gets Data

At the destination:

UDP receives the datagram
- Removes header
- Sends data to the application
- Step 8: No Error Recovery or Reordering

If:

- Packet is lost 
- Packet is corrupted 
- Packet arrives out of order 

UDP does nothing.

 The application must handle it if needed.



##  Features of UDP (User Datagram Protocol)

- Connectionless Protocol: UDP does not establish a connection before sending data, allowing faster communication without handshake overhead.

- Unreliable Communication: UDP does not guarantee delivery, acknowledgment, or retransmission of lost packets, making it less reliable than TCP.

- No Ordering of Data: Packets may arrive out of order since UDP does not use sequence numbers or reordering mechanisms.

- No Error Recovery: UDP only performs basic checksum error detection but does not correct or retransmit corrupted data.

- Faster Transmission: Due to minimal overhead and no connection setup, UDP provides very fast data transmission.

- Lightweight Protocol: UDP has a small header size (8 bytes), making it efficient for applications requiring low latency.

- No Flow Control: UDP does not control data flow between sender and receiver, which can lead to packet loss if receiver is overwhelmed.

- No Congestion Control: UDP does not manage network congestion, so it keeps sending data regardless of network conditions.

- Supports Broadcasting & Multicasting: UDP allows sending data to multiple recipients simultaneously, useful for streaming and real-time applications.

- Used in Real-Time Applications: UDP is preferred for applications like video streaming, gaming, and VoIP where speed is more important than reliability.


## Interview Questions 

##  Networking Concepts (HTTP, DNS, TCP)

###  Why HTTP uses TCP

HTTP uses Transmission Control Protocol because web communication requires reliable and ordered data delivery. When loading a webpage, all files (HTML, CSS, JS) must arrive completely and correctly, otherwise the page may break. TCP ensures this by using acknowledgments, retransmissions, and sequencing, making it suitable for HTTP.

---

###  Why DNS uses UDP

Domain Name System uses User Datagram Protocol because it needs fast and lightweight communication. DNS queries are small and require quick responses, so UDP is preferred as it has no connection setup and low overhead. This allows faster domain resolution, which improves overall website loading speed.

#### Real Example (DNS Request)


When you open a website:

- Browser sends DNS request using UDP
- UDP sends packet instantly (no handshake)
- DNS server replies quickly
- Browser gets IP

 Fast response is more important than reliability here.

---

###  What happens if TCP handshake fails?

If the TCP handshake fails, the connection between client and server is not established, and no data is transferred. The client may retry the connection multiple times, and if it still fails, it results in errors like “connection timeout” or “connection refused.” This usually happens due to server downtime, network issues, firewall blocking, or incorrect ports.




