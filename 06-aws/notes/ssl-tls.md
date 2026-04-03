# SSL/TLS

### Keywords & Connections:

- **SSL/TLS**: Protocol for encrypting data traveling over a network. TLS is the newer more secure version of SSL but people still call it SSL.
- **Certificate**: proves the identity of a website and enables encryption. Certificates are given by third party authorities like *Lets Encrypt* or *DigiCert*, they expire after a while and needs to be renewed.
    Encryption explained: 
        1. The certificate contains the website's identity (verified by the Certificate Authorities) and a public key used for encryption 
        2. When users try to send data to website it is given the public key by the website which it uses to encrypt a **session key** with.
        3. The encrypted session key is then sent and can only be opened by the website since it has a **private key (linked to the public key given)** which is used to decrypt the session key with.
        4. After the connection is established both sides use this session key to encrypt all communication with.
- **ACM (AWS Certificate Manager)**: AWS service that creates, manages and auto-renews certificates for free when used alongside AWS services like ALB.
- **SNI (Server Name Indication)**: A TLS protocol feature that serves up the right certificate within a LB based on hostname used by the user. (Cannot be used by CLB)

### What problem does this solve?

- **SSL/TLS**: Data often travel through several checkpoints (routers, ISPs, wifi networks and other infrastructure) before reaching its destination, without SSL/TLS encryption anyone sitting in any of these checkpoints could get a hold of your data.
- **SNI**: simplifies the managment of certificates by allowing you to keep them all withing one LB
- **ACM**: removes the manual work of buying, installing, and renewing certificates.
