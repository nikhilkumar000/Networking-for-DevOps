# Cryptography Basics

Cryptography is the science and art of securing information by transforming readable data (plaintext) into an unreadable format (ciphertext) using mathematical algorithms and keys. It ensures data privacy, integrity, and authentication, making it essential for secure communication, online transactions, and cybersecurity.

## Types of Cryptography

### 1. Symmetric cryptography (Private Key)

In symmetric encryption, the same key is used for both encryption and decryption. Both the sender and the receiver must have a copy of this secret key.

 #### How it works:
 Think of a physical safe. You put a document inside and lock it with a key. To get the document out, the other person must have a duplicate of that exact same key.

#### Speed:
 It is extremely fast and efficient, making it ideal for encrypting large amounts of data (like a database backup or a streaming video).

#### The Big Problem: 
Key Distribution. How do you send the secret key to the other person over the internet without a hacker stealing it? If the key is intercepted, the security is broken.

#### Common Algorithm Examples: 
AES (Advanced Encryption Standard), used by your Wi-Fi (WPA2) and for encrypting hard drives.

#### Real world example

For example, suppose Alice wants to send the message “HELLO” to Bob. She uses a symmetric algorithm like AES (Advanced Encryption Standard) with a shared key (e.g., K123) to encrypt the message into ciphertext (e.g., XyZ@91). This encrypted message is sent over the network. When Bob receives it, he uses the same key K123 with the AES algorithm to decrypt it back to “HELLO”.

---

### 2. Asymmetric cryptography (Public Key)

Asymmetric encryption uses a pair of keys: a Public Key and a Private Key. They are mathematically linked, but you cannot figure out the private key even if you have the public one.

#### How it works:
 Think of a mailbox. Anyone can walk up and drop a letter through the slot (Public Key), but only the owner has the physical key to open the box and read the mail (Private Key).

#### The Solution:
 You can share your Public Key with the whole world. Anyone can use it to encrypt a message for you, but only you can decrypt it using your secret Private Key.

#### Speed:
 It is mathematically complex and much slower than symmetric encryption.

#### Common Algorithm Examples:
 RSA, ECC (Elliptic Curve Cryptography), and the technology behind SSH Keys and HTTPS certificates.

 #### Real world example

 For example, suppose Alice wants to send the message “HELLO” to Bob. Bob provides his public key (e.g., Pub_B). Alice uses an asymmetric algorithm like RSA to encrypt the message using Pub_B, converting it into ciphertext (e.g., A9#kL2). This encrypted message is sent over the network. When Bob receives it, he uses his private key (Priv_B) to decrypt the ciphertext back into “HELLO”.

