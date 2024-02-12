HTTPS is an extension of [[HTTP]] and is used for secure communication over a computer [[network]] within a [[web browser]]. It incorporates an additional layer of encryption intended to enhance security of data as it travels across the network.
## Core Features of HTTPS
### Encryption
HTTPS uses [[SSL]]/TLS [[protocols#Main Network Protocols||protocols]] to encrypt the data exchange, making it secure from [[some attacks#Eavesdropping||eavesdropping]] and tampering. This encryption makes sure that any data transmitted is only understood by the intended recipient.
### Integrity
Data integrity is assured in HTTPS, meaning that the data cannot be modified or corrupted during transfer without detection.
### Authentication
HTTPS includes a mechanism for the web browser to verify the authenticity of the web server. This ensures that the user is communicating with the actual website as intended and not a malicious imposter (protecting against attacks like [[some attacks#phishing||phishing]]).
### Port
The default port for HTTPS is `443`, as opposed to HTTP which uses port `80`.

## How it works / [[ssl||TLS]] handshake

this whole process is greatly detailed on the [[SSL||TLS]] note, please see it

## Defense Against [[some attacks||Common Attacks]]
### Man-in-the-Middle (MitM) Attacks
By encrypting the data transferred between the client and server, HTTPS defends against MitM attacks, where a third party could potentially intercept and alter the communication.
### Eavesdropping Attacks
HTTPS encrypts the data being transmitted, which prevents unauthorized parties from reading the information as it travels through the network.
### Tampering
Data integrity checks in HTTPS help detect any tampering of transmitted data, ensuring the data arrives as intended without unauthorized alterations.

## Extra information
### Digital Certificates
Websites use [[digital certificates]] to authenticate themselves to users. Certificates are issued by Certificate Authorities (CAs), trusted entities that verify the identity of the certificate holder.
### Public Key Infrastructure (PKI)
HTTPS relies on PKI for the issuance, management, and revocation of digital certificates.
### SEO Benefits
Search engines favor HTTPS websites, often ranking them higher in search results, which incentivizes the adoption of HTTPS for webmasters.
### HTTP/2
HTTPS is often a prerequisite for using the newer HTTP/2 protocol, which provides significant performance improvements over HTTP/1.x.
