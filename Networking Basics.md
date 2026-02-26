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





==> What is TLS Termination?

-> TLS Termination means decrypting HTTPS traffic at the Load Balancer instead of at the application server.

==> In simple words:
User → HTTPS → Load Balancer
Load Balancer decrypts it
Then sends normal HTTP to internal servers

==> Why Do We Need TLS Termination?

Because:
-> TLS encryption/decryption is CPU intensive
-> Managing certificates on every server is complex
-> Scaling becomes harder
-> So we centralize TLS handling at the load balancer.

==> Without TLS Termination:

Every app server handles HTTPS.
User -->|HTTPS| Server1
User -->|HTTPS| Server2
User -->|HTTPS| Server3
Server1 --> Database
Server2 --> Database
Server3 --> Database

Problems:
-> Each server must:
-> Store SSL certificates
-> Perform TLS handshake
-> Do encryption/decryption
-> More CPU usage
-> Harder certificate management


==> With TLS Termination (Recommended):

User -->|HTTPS| LoadBalancer
LoadBalancer -->|HTTP| Server1
LoadBalancer -->|HTTP| Server2
LoadBalancer -->|HTTP| Server3
Server1 --> Database
Server2 --> Database
Server3 --> Database

Flow:
1️⃣ User connects via HTTPS
2️⃣ Load balancer performs TLS handshake
3️⃣ Load balancer decrypts traffic
4️⃣ Sends plain HTTP inside private network



What Exactly Is “Termination”?

-> Termination = The point where encrypted communication ends.

At Load Balancer:
-> TLS handshake happens
-> Certificates validated
-> Session keys created
-> Traffic decrypted

==> After that:
Internal communication may not use TLS (inside secure VPC).

==> Real-World Example

-> Companies like:
Amazon
Netflix
Google

==> Use:
AWS ELB / ALB
NGINX
HAProxy
To terminate TLS.

==> Is It Safe?

Yes, if:
-> Internal network is private (VPC)
-> Firewalls restrict access
-> Servers are not publicly exposed


==> What If We Want End-to-End Encryption?

Then we use:
🔐 TLS Passthrough
Load balancer does NOT decrypt.

User -->|HTTPS| LoadBalancer
LoadBalancer -->|HTTPS| Server1
LoadBalancer -->|HTTPS| Server2

Servers handle TLS themselves.

==> Used when:
-> Regulatory compliance required
-> Zero-trust architectures
-> Internal network not fully trusted

==> TLS Termination vs TLS Passthrough

Feature	                TLS Termination	            TLS Passthrough
Decryption happens at	Load Balancer	            pp Server
CPU usage	            Less on app servers	        More on app servers
Certificate management	Centralized	                Distributed
Security	            Good (if private network)	Stronger end-to-end


==> Why System Designers Prefer Termination

1️⃣ Better performance
2️⃣ Easier certificate renewal
3️⃣ Simpler scaling
4️⃣ Centralized security control





🔷 TLS re-encryption

==> Normal TLS Termination (Basic Case):

Flow:
1️⃣ User connects via HTTPS.
2️⃣ Load balancer decrypts traffic.
3️⃣ Sends plain HTTP to app server.
4️⃣ App server sends plain response back.
5️⃣ Load balancer encrypts again before sending to user.

So client communication is always encrypted.
But inside the private network → traffic is plain HTTP.


==> TLS Re-Encryption (More Secure Setup):

Flow:
Now we add extra security.
1️⃣ User → LB: Encrypted
2️⃣ LB decrypts
3️⃣ LB processes request (routing, WAF, etc.)
4️⃣ LB re-encrypts request
5️⃣ Sends encrypted traffic to App Server

So encryption exists:
-> Client → Load Balancer
-> Load Balancer → App Server
-> That’s TLS re-encryption.

==> Why Do We Re-Encrypt?

Because sometimes:
-> Internal network is not fully trusted
-> Zero-trust architecture is required
-> Compliance rules (banking, healthcare)
-> Prevent internal lateral movement attacks

The difference is:
Setup	            Internal traffic
TLS Termination	    HTTP (plain)
TLS Re-encryption	HTTPS (encrypted)

Client communication remains encrypted in both.