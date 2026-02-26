HTTP vs HTTPS

🔷 HTTP (HyperText Transfer Protocol)

Used for communication between client and server
Data sent in plain text
Default port: 80
Not secure

Example Problem:
If someone intercepts traffic, they can read passwords.



==> What Does “Intercepting Traffic” Mean?

When data travels from:
-> Your Device → Router → ISP → Internet → Server
-> It passes through multiple network points.
-> If communication is not encrypted (HTTP), anyone who can observe that network path can read the data.

That is called:
-> Traffic interception or packet sniffing

==> How Data Travels (Without HTTPS)

User->>Router: HTTP Request (plain text)
Router->>ISP: Forward data
ISP->>Server: Forward data
Server->>User: HTTP Response (plain text)

-> If the data is plain text, anyone in the middle can read it.

==> This is called a:
Man-in-the-Middle (MITM) scenario

-> Intercept = Capturing network packets while they are traveling between client and server.

==> Think of it like:
Sending a postcard instead of a sealed envelope.
Anyone handling the postcard can read it.


==> Real-World Example:

Imagine you're using public WiFi at:
Airport
Café
Hotel

If website uses HTTP (not HTTPS):
When you send:
username=rohan
password=123456

-> That data is sent in readable form.
-> Someone connected to same network could capture the packets and read it.

==> What Is Packet Sniffing? (Concept Only)

-> Network devices break communication into small pieces called packets.
-> If someone has access to the same network:
-> They can monitor packets flowing through it.

==> If those packets are:
Unencrypted → readable
Encrypted → unreadable


==> Example: HTTPS (Safe)

User->>Server: Encrypted Random Data
Note over User,Server: Encrypted using TLS

==> Even if intercepted:
It looks like random characters.

==> Example of encrypted data:

-> a8sj29sjdk29dj29skd02jdksl29sd
-> Without the decryption key, it's useless.


🔷 HTTPS (HTTP Secure)

HTTP + SSL/TLS encryption
Data encrypted before sending
Default port: 443
Secure communication


HTTP:
User->>Server: HTTP Request (Plain Text)
Server->>User: HTTP Response (Plain Text)

HTTPS:
User->>Server: HTTPS Request (Encrypted)
Server->>User: HTTPS Response (Encrypted)

==> HTTPS is HTTP secured using SSL/TLS encryption, ensuring confidentiality and data integrity.


SSL (Secure Sockets Layer) and TLS (Transport Layer Security) are cryptographic protocols used to secure communication between a client and a server.

👉 Today, we use TLS.
SSL is older and deprecated.

When you see:

https://

That means:

HTTP + TLS encryption

🔷 Why Do We Need TLS?

Without TLS: Anyone intercepting the network can read this.(Data sent in plain text)
With TLS: Now even if someone intercepts traffic, they cannot understand it.(Encrypted Data)

What TLS Provides (Very Important)

TLS ensures:
1️⃣ Confidentiality → Data is encrypted
2️⃣ Integrity → Data cannot be modified
3️⃣ Authentication → Server identity verified

These are core security principles.


SSL vs TLS

SSL	                    TLS
Older	                Newer
Less secure	            More secure
Deprecated	            Currently used
SSL 3.0 last version	TLS 1.2 / 1.3 used today


==> How TLS Works (Handshake Process):

This is the most important part.

-> Step 1: Client Hello
Client sends:
Supported TLS versions
Cipher suites
Random number

-> Step 2: Server Hello
Server replies:
Chosen TLS version
Chosen cipher suite
Sends certificate (contains public key)

-> Step 3: Certificate Verification
Client verifies:
Is certificate signed by trusted CA?
Is domain valid?

-. Step 4: Key Exchange
Client generates:
A symmetric session key
Encrypts it using:
Server’s public key
Sends to server.

-> Step 5: Secure Communication Starts
Both now use
Symmetric encryption (fast)
Same session key

TLS Handshake Diagram:

Client->>Server: Client Hello
Server->>Client: Server Hello + Certificate
Client->>Server: Verify Certificate
Client->>Server: Encrypted Session Key
Server->>Client: Handshake Complete
Note over Client,Server: Secure Communication Begins

🔷 Why Use Public + Symmetric Encryption?

Because:

Asymmetric encryption (public/private key) is secure but slow

Symmetric encryption is fast

So TLS uses:

Asymmetric → to exchange key

Symmetric → for actual data

Smart design.

🔷 What is a Certificate?

A digital certificate contains:

Server public key

Domain name

Issuing Certificate Authority (CA)

Expiry date

Example CAs:

DigiCert

GlobalSign

Let’s Encrypt

If certificate is invalid:
Browser shows:
⚠️ “Your connection is not private”

🔷 Real Interview Example

If designing a payment system:

Non-functional requirement:

All communication must use HTTPS (TLS 1.2+)

Why?

Protect card details

Prevent man-in-the-middle attacks

Ensure data integrity

🔷 TLS in System Design

TLS affects:

Latency (handshake cost)

CPU usage (encryption cost)

Load balancer configuration

Certificate renewal management

In high-scale systems:
TLS termination often happens at Load Balancer.


TLS Termination Example:

User -->|HTTPS| LoadBalancer
LoadBalancer -->|HTTP| AppServer1
LoadBalancer -->|HTTP| AppServer2

Load balancer decrypts traffic, internal communication may remain inside secure VPC.