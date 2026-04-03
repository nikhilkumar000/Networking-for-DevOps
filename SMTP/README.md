

#  What is SMTP Protocol?

 SMTP (Simple Mail Transfer Protocol) is a communication protocol used to send emails over the Internet. It defines how mail servers send and relay email messages between each other.

 In simple words: SMTP is responsible for sending emails from a client (like Gmail, Outlook, or a web app) to a mail server and between mail servers.

- Works on **Application Layer**
- Uses **TCP for reliable communication**

---

##  Common SMTP Ports

| Port | Usage |
|------|------|
| 25   | Default SMTP port (server-to-server communication) |
| 587  | SMTP with authentication (most common today) |
| 465  | SMTP over SSL/TLS |

---

##  How SMTP Works (Step-by-Step)

###  Step 1: User Composes Email
A user writes an email in a mail client such as Gmail, Outlook, Apple Mail, or a web application backend.

**Example:**

From: nikhil@gmail.com

To: friend@yahoo.com

Subject: Hello

Hi, How are you?


---

###  Step 2: Email Client Connects to SMTP Server
The mail client connects to the sender’s SMTP server (e.g., smtp.gmail.com) using TCP.


Client → SMTP Server
TCP connection established


---

###  Step 3: SMTP Handshake
The client and server establish communication using SMTP commands.

**Example:**

Client: HELO mail.example.com
Server: 250 Hello


| Command      | Purpose              |
|-------------|----------------------|
| HELO / EHLO | Identify client      |
| MAIL FROM   | Sender email         |
| RCPT TO     | Receiver email       |
| DATA        | Email body           |
| QUIT        | Close connection     |

---

###  Step 4: Sender and Receiver Identification
The client specifies sender and receiver email addresses.


MAIL FROM: nikhil@gmail.com

RCPT TO: friend@yahoo.com


Server verifies recipient existence.

---

###  Step 5: Email Content Transfer
The actual email content is sent using the DATA command.


DATA
Subject: Hello

Hi, How are you?
.


 `.` (dot) indicates end of message.

---

###  Step 6: SMTP Server Finds Recipient Server
The sender mail server performs a DNS lookup to find the recipient’s mail server using MX records.

**Example:**

yahoo.com → MX record → Yahoo mail server


---

### Step 7: Server-to-Server Email Transfer
The sender SMTP server connects to the receiver SMTP server and transfers the email.


Gmail SMTP Server → Yahoo SMTP Server


---

###  Step 8: Email Stored in Recipient Mailbox
The email is stored in the recipient’s mailbox, and the user retrieves it using:

| Protocol | Purpose |
|----------|--------|
| POP3     | Download emails |
| IMAP     | Sync emails |

 **Important:** SMTP is used to send emails, while IMAP/POP3 are used to receive emails.

---


###  Real-Life Example

You send an email:


From: nikhil@gmail.com

To: hr@company.com


##  SMTP in DevOps / Backend Development

SMTP is commonly used in production systems for sending emails in various scenarios.

---

###  Common Use Cases

#### 1. Sending OTP
Used in authentication systems where a one-time password is sent to the user’s email.

**Example:**

Login → Send OTP email


---

#### 2. Password Reset
Used when a user clicks "Forgot Password" and receives a reset link via email.


Click "Forgot Password" → Email reset link


---

#### 3. Notifications
Used for sending important updates and alerts to users.

**Examples:**
- Order confirmation emails  
- Deployment alerts  
- Monitoring alerts  

---

###  DevOps Tools Using SMTP

Many DevOps and monitoring tools use SMTP to send alerts:

- Jenkins → Build status notifications  
- Prometheus → Alertmanager emails  
- Grafana → Monitoring alerts  

---

##  SMTP Security

Modern email systems use encrypted SMTP for secure communication.

---

###  TLS (STARTTLS)
Connection starts as normal SMTP and then upgrades to an encrypted connection.


SMTP → STARTTLS → Secure


---

###  SMTPS
Uses a direct encrypted connection from the beginning.


SMTP over SSL/TLS


## POP3 Protocol (Post Office Protocol v3)


POP3 is an email protocol used to download emails from the mail server to the user's local device.

After downloading, the emails are usually deleted from the server (depending on settings).

Think of POP3 like collecting letters from a physical post office and taking them home.

## IMAP Protocol (Internet Message Access Protocol)


IMAP is an email protocol used to access and manage emails directly on the mail server without downloading them permanently.

Emails remain stored on the server, and all devices stay synchronized.

Think of IMAP like reading emails stored in the cloud.