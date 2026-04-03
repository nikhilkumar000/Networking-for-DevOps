# TLS (Transport Layer Security)


TLS (Transport Layer Security) is a modern security protocol that provides encryption, data integrity, and authentication for communication over a network.

 It is the updated and more secure version of SSL. TLS is mainly used with HTTPS to secure web traffic and runs on top of Transmission Control Protocol. 
 
 It ensures that data exchanged between a client (browser) and a server remains private and protected from attackers, preventing issues like data theft or man-in-the-middle attacks. Today, almost all secure internet communication uses TLS instead of SSL.

## Working of TLS (Step-by-Step)

### Step 1: Client Hello

The client (browser) sends a Client Hello message to the server.

It includes:

- Supported TLS versions
- Supported cipher suites (encryption methods)
- Random number

### Step 2: Server Hello

The server responds with a Server Hello message.

It includes:

- Selected TLS version
- Selected cipher suite
- Server random number

### Step 3: Server Sends Certificate

The server sends its TLS certificate.

- Contains public key
- Issued by a trusted Certificate Authority (CA)

The client verifies this certificate.

### Step 4: Key Exchange

The client generates a session key.

- Encrypts it using server’s public key
- Sends it to the server

The server decrypts it using its private key.

Now both have the same session key.

### Step 5: Secure Connection Established

Both client and server confirm the handshake.

Now:

- Encryption is enabled
- Secure channel is established 

### Step 6: Encrypted Data Transfer

All communication now uses symmetric encryption (session key):

- Data is encrypted before sending
- Decrypted at receiver

Fast and secure communication happens.



### Why TLS Is Important (DevOps View)

- Secures APIs and web apps
- Protects sensitive data
- Required for HTTPS (port 443)
- Used in microservices communication
- Important for compliance (security standards)