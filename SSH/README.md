# SSH (Secure shell) Protocol

SSH, or Secure Shell, is a network protocol that gives users—particularly system administrators and DevOps engineers a secure way to access and manage a computer over an unsecured network.

When you use SSH, it creates an encrypted "tunnel" between your local machine and a remote server (like an AWS EC2 instance). Even if someone intercepts the data moving through the internet, they cannot read it because it is scrambled with high-level mathematics.

##  How SSH Works (The Basics)

SSH typically uses a Client-Server model:

### The SSH Client: 
The software on your computer (like Terminal, PowerShell, or PuTTY) that you use to initiate the connection.

### The SSH Server:
 The software running on the remote machine (usually a Linux server) that listens for incoming connections on Port 22.

 ### The Connection Process:

 #### Handshake:
  The client and server agree on encryption algorithms.

 #### Authentication:
   The server verifies who you are. This is done via a Password or, more securely, SSH Keys (a Public/Private key pair).
#### Encryption:
   Once verified, all commands you type and the data sent back are encrypted.
   
## Why is SSH Used?
   SSH is the "gold standard" for remote management for several reasons:
   
 ### Remote Command Line Access:
    You can log into a server sitting in a data center in Virginia or Mumbai and run commands as if you were sitting right in front of it.

### Secure File Transfer (SFTP/SCP):
     You can move files between your local machine and a server securely. (You might use this to upload your utilities.py or app.log files to a production server).
     
### Tunneling (Port Forwarding):
 You can "pipe" traffic from a private database in an AWS VPC through an SSH jump box to your local machine so you can inspect data safely.
 
 ### Automation:
  DevOps tools like Ansible or Terraform use SSH to log into hundreds of servers at once to install updates or configure software
  
 ## SSH vs. Telnet
 Before SSH, people used Telnet. However, Telnet is dangerous because it sends everything—including your username and password—in plain text.
 
  Anyone "sniffing" the network could easily steal your credentials. SSH was designed specifically to fix this massive security hole.
  
 ##  Telnet vs SSH Comparison

| Feature   | Telnet            | SSH                                   |
|-----------|------------------|---------------------------------------|
| Security  | None (Plain Text)| Encrypted                             |
| Port      | 23               | 22                                    |
| Integrity | Can be tampered  | Protected via MAC (Message Authentication Code) |
  
  ## How You'll Use It (Example)
  Since you are learning Python for DevOps, you will eventually use the paramiko library to automate SSH tasks.
  #### Manual Command Example:
  Bash#  Connecting to a server using a private key (.pem file)
ssh -i "my-key-pair.pem" ubuntu@3.85.12.44


## SSH Encryption Mechanism

It uses both symmetric and asymmetric cryptography.

### Asymmetric (The Handshake):
 When you connect to a server, SSH uses Asymmetric encryption to verify your identity and securely "agree" on a temporary secret key.

### Symmetric (The Session):
 Once the "handshake" is done and the secret key is safely exchanged, SSH switches to Symmetric encryption (AES) for the rest of the session because it is much faster for sending commands and files.