HTTP HTTPS SSL TLS Notes

---

1. What is HTTP

Definition  
HTTP HyperText Transfer Protocol is a communication protocol used for data transfer between client and server

It follows request response model

---

2. How HTTP Works Internally

Step 1 Client Request  
Browser sends request to server  
Example

GET /home HTTP/1.1  
Host: example.com

Step 2 DNS Resolution  
Domain name is converted into IP address

Step 3 TCP Connection  
Connection established using 3 way handshake  
SYN  
SYN ACK  
ACK

Step 4 Request Sent  
Headers and optional body sent

Step 5 Server Processing  
Server processes request

Step 6 Response Sent

HTTP/1.1 200 OK  
Content-Type: text/html

Step 7 Connection Close or Keep Alive

---

3. Problems with HTTP

Data is sent in plain text  
No encryption  
No identity verification  
Vulnerable to man in the middle attacks

---

4. What is HTTPS

Definition  
HTTPS HyperText Transfer Protocol Secure is HTTP with security layer

It uses SSL or TLS for encryption

---

5. What is SSL and TLS

SSL stands for Secure Sockets Layer  
TLS stands for Transport Layer Security

SSL is older protocol now deprecated  
TLS is modern and secure version

In real world HTTPS uses TLS not SSL but people still say SSL

---

6. Why SSL TLS is Required

To secure communication between client and server

Provides  
Encryption  
Integrity  
Authentication

---

7. How TLS Works Internally with Example

Real world example

User opens https website like a banking site

---

Step 1 Client Hello

Browser sends  
Supported TLS versions  
Cipher suites  
Random number

---

Step 2 Server Hello

Server responds with  
Selected TLS version  
Selected cipher suite  
SSL TLS certificate  
Server random number

---

Step 3 Certificate Verification

Browser checks certificate  
Issued by trusted Certificate Authority  
Checks domain validity  
Checks expiry

If invalid connection stops

---

Step 4 Key Exchange

Browser generates a pre master secret  
Encrypts it using server public key  
Sends to server

Server decrypts using private key

Now both have same secret

---

Step 5 Session Key Generation

Client and server use  
Client random  
Server random  
Pre master secret

To generate session key

---

Step 6 Secure Connection Established

Now communication switches to symmetric encryption

---

Step 7 Encrypted Data Transfer

All HTTP data is encrypted using session key

Example

Encrypted GET request  
Encrypted response

---

8. Encryption Types Used

Asymmetric Encryption  
Used during handshake  
Uses public key and private key  
Slower but secure

Symmetric Encryption  
Used after handshake  
Uses same key for encryption and decryption  
Faster

---

9. HTTP vs HTTPS Difference

HTTP  
No encryption  
Plain text communication  
Port 80  
No security  
Faster but unsafe

HTTPS  
Encrypted communication  
Uses TLS  
Port 443  
Secure and trusted  
Slightly slower but safe

---

10. Key Security Features of HTTPS

Encryption  
Protects data from attackers

Integrity  
Ensures data is not modified

Authentication  
Verifies server identity

---

11. Simple Analogy for TLS

Think of TLS like

Step 1 You ask for a secure lock  
Step 2 Server gives lock and certificate  
Step 3 You verify lock is genuine  
Step 4 You create secret key and lock it  
Step 5 Server opens it  
Step 6 Now both use same key to talk privately

---

12. Final Quick Revision

HTTP sends data in plain text  
HTTPS uses TLS for security  
SSL is old TLS is new  
TLS handshake creates secure session  
After handshake communication is encrypted