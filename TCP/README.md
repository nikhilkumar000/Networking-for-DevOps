# Transmission Control Protocol (TCP)

The Transmission Control Protocol (TCP) is a connection-oriented protocol that ensures reliable communication between devices. It allows applications and devices to exchange messages over a network with confidence that the data will arrive intact and in the correct order, without error and packet lost.

TCP is designed to break information into packets, send them across the internet, and then reassemble them at the destination, making sure nothing is lost along the way.

It is a connection-oriented protocol, meaning it must establish a formal "handshake" between two devices before any data is exchanged.

## TCP Lifecycle

![alt text](<TCP lifecycle.png>)

## How TCP Works: The Lifecycle

TCP communication follows a strict three-phase process: Establishment, Data Transfer, and Termination.

### Phase 1: The Three-Way Handshake (Connection)

Before your browser (the client) can talk to a server, they must "sync up" their sequence numbers to track the data.

 - **SYN (Synchronize):** The client sends a packet to the server saying, "I want to connect. Here is my starting sequence number (e.g., 100)."

- **SYN-ACK (Sync-Acknowledge):** The server replies, "I received your request (ACK 101). I also want to connect. Here is my starting sequence number (e.g., 500)."

- **ACK (Acknowledge):** The client sends a final confirmation, "I received your number (ACK 501). Let's start!"

![alt text](<3-way Handshake.png>)

### Phase 2: Reliable Data Transfer

Once connected, data is broken into "segments." TCP uses several mechanisms to guarantee delivery:

- **Sequencing:** Every byte is numbered. If packets arrive out of order, TCP uses these numbers to reassemble them correctly.

- **Acknowledgments (ACKs):** For every group of packets received, the receiver sends an "ACK" back. If the sender doesn't get an ACK within a certain timeframe, it assumes the data was lost and retransmits it automatically.

- **Flow Control (Windowing):** The receiver tells the sender how much data it can handle at once. This prevents a fast sender from overwhelming a slow receiver.

### Phase 3: The Four-Way Handshake (Termination)

When the conversation is over, TCP closes the connection gracefully so no data is cut off.

- **Client sends FIN:** "I'm done sending data."

- **Server sends ACK:** "I heard you, let me finish my last tasks."

- **Server sends FIN:** "I'm done too."

- **Client sends ACK:** "Confirmed. Goodbye."

## TCP Header Format

![alt text](<TCP Header.png>)


The TCP header is the first 20 bytes of a TCP segment and contains important details about the connection. 

It holds the parameters and state information needed for communication between two endpoints. 

Inside the header are several key fields such as the source and destination port numbers that help identify where the data is coming from and where it should go.


- **Source Port (16 bits):** Identifies the sender’s TCP port number.

- **Destination Port (16 bits):** Identifies the receiver’s TCP port number.

- **Sequence Number (32 bits):** Indicates the position of the first byte of data in the current TCP segment. When a new TCP connection is created, this number starts with a randomly chosen value to improve security and reliability.

- **Acknowledgment Number (32 bits):** Used by the receiver to confirm data has been received. If the ACK flag is set, this field specifies the next sequence number the receiver expects from the sender. Once the connection is established, this field is always included.

- **Data Offset (4 bits):** Also called the header length, it specifies the size of the TCP header in 32-bit words.

- **Reserved (6 bits):** Reserved for future use and always set to zero.

- **Control Flags (9 bits):** A set of flags that manage the state of the connection and control how data flows. The most commonly used flags include:

URG — Urgent: Marks data as high priority.

ACK — Acknowledgment: Confirms that data has been received.

PSH — Push: Instructs TCP to deliver data immediately without waiting for the buffer to fill.

RST — Reset: Abruptly terminates a faulty or invalid connection.

SYN — Synchronize: Used to start a new connection and synchronize sequence numbers.

FIN — Finish: Gracefully closes a connection (both sides must send FIN to fully close).

- **Window Size (16 bits):** Indicates how much data (in bytes) the receiver is ready to accept at once. This is key for TCP’s flow control.

- **Checksum (16 bits):** Used for error-checking the TCP header and data to ensure integrity.

- **Urgent Pointer (16 bits):** Works with the URG flag to mark the last byte of urgent data.

- **Options (0–320 bits):** Optional field for extra features like maximum segment size (MSS) or window scaling.




## Features of TCP (Transmission Control Protocol)

### 1. Connection-Oriented

TCP establishes a connection between sender and receiver before data transfer using a 3-way handshake process.

### 2. Reliable Communication

TCP ensures reliable delivery of data by using acknowledgments (ACK) and retransmitting lost packets.

### 3. Ordered Data Delivery

TCP delivers data in the correct sequence using sequence numbers to maintain order.

### 4. Error Detection & Correction

TCP uses checksums to detect errors in data and retransmits corrupted packets for accuracy.

### 5. Flow Control

TCP controls the data flow between sender and receiver using a sliding window to prevent overload.

### 6. Congestion Control

TCP manages network congestion using algorithms like slow start and congestion avoidance.

### 7. Full-Duplex Communication

TCP allows simultaneous two-way data transmission between sender and receiver.

### 8. Byte Stream Protocol

TCP treats data as a continuous stream of bytes rather than separate messages.

### 9. Port-Based Communication

TCP uses port numbers to identify and manage communication between different applications.

### 10. Segmentation & Reassembly

TCP divides data into smaller segments for transmission and reassembles them at the receiver side.