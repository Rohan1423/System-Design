HTTP vs HTTPS

🔷 HTTP (HyperText Transfer Protocol)

Used for communication between client and server
Data sent in plain text
Default port: 80
Not secure

Example Problem:
If someone intercepts traffic, they can read passwords.



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