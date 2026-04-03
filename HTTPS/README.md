# HTTPS

HTTPS is simply HTTP with an added layer of security: TLS (Transport Layer Security) or its predecessor, SSL.

 It provides Encryption (hides data), Data Integrity (prevents tampering), and Authentication (proves the website is who they say they are).

It uses Port 443 by default.

## Working of HTTPS

When you type a URL into your browser, a specific "Handshake" occurs: 

### Step 1:- TCP Handshake
Before the browser can send an HTTP request, it must establish a connection using the TCP 3-Way Handshake (SYN, SYN-ACK, ACK) that we discussed earlier.

### Step 2:- TLS Handshake (HTTPS only)

If the website uses HTTPS, an extra "Security Handshake" happens:- 

- Client Hello: The browser sends supported encryption versions.

- Server Hello & Certificate: The server sends its SSL Certificate (which contains its Public Key).

- Authentication: The browser checks with a Certificate Authority (CA) to make sure the certificate is valid.

- Key Exchange: The browser and server use Asymmetric Cryptography to agree on a "Session Key" (a shared secret).

- Encrypted Session: From this point on, they switch to Symmetric Cryptography for speed.

### Step 3: The Request/Response Cycle

Now that the "tunnel" is secure, the actual data transfer happens:

- HTTP Request: The browser sends a message like: GET /index.html HTTP/1.1.

- Server Processing: The server looks for the file or runs code (like your FastAPI or Node.js backend).

- HTTP Response: The server sends back a status code (e.g., 200 OK) and the content of the page.

###  HTTP vs HTTPS Comparison

| Feature     | HTTP                          | HTTPS                              |
|-------------|-------------------------------|------------------------------------|
| Encryption  | None (Plain Text)             | Encrypted (SSL/TLS)                |
| Security    | Vulnerable to "Man-in-the-Middle" attacks | Secure and Private                |
| SEO         | No advantage                  | Search engines (Google) rank HTTPS higher |
| Port        | 80                            | 443                                |
| Certificate | Not Required                  | Requires an SSL Certificate        |


### Why this matters for your DevOps Career

In your AWS VPC, you will often manage Load Balancers. A common task is "SSL Termination," where the Load Balancer handles the heavy HTTPS decryption (Port 443) and then talks to your internal EC2 instances or containers via simple HTTP (Port 80) to save CPU power.

## Certificates in HTTPS

Certificates in HTTPS are called SSL/TLS certificates, and they are used to verify the identity of a website and enable secure (encrypted) communication between a client (browser) and a server.

 A certificate is a digital file issued by a trusted organization called a Certificate Authority (CA), which confirms that the website is genuine. It contains important information such as the domain name, the server’s public key, issuer details, and validity period.
 
  These certificates are a core part of Transport Layer Security, ensuring that data sent between the browser and server is encrypted and protected from attackers.

#### What a Certificate Contains

An HTTPS certificate includes:

- Domain name (e.g., example.com)
- Public key (used for encryption)
- Issuer (Certificate Authority like Let’s Encrypt)
- Validity period (start and expiry date)
- Digital signature of the CA

#### Note:-  Working of certificates is same as ssl handshake or we will know more in ssl protocol

### Types of Certificates

#### 1. Domain Validated (DV)

- Basic verification
- Used for personal or small sites

#### 2. Organization Validated (OV)

- Verifies business identity
- More trusted

#### 3. Extended Validation (EV)

- Highest level of trust
- Shows company name in browser

### Why Certificates Are Important (DevOps View)
- Enable HTTPS (port 443)
- Protect sensitive data (passwords, APIs)
- Prevent man-in-the-middle attacks
- Required for production apps
- Improve SEO ranking