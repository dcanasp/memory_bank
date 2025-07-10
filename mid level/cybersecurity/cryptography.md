Cryptography is the science and art of securing communication and information through the use of mathematical techniques. It plays a crucial role in ensuring the confidentiality, integrity, and authenticity of data in various applications.

## Key Concepts

### **Confidentiality**

- Confidentiality ensures that unauthorized individuals or systems cannot access or understand the protected information.

### **Integrity**

- Integrity guarantees that the information remains unaltered during storage, transmission, or processing.

### **Authentication**

- Authentication verifies the identity of parties involved in a communication, ensuring that each party is who they claim to be.

### **Non-Repudiation**

- Non-repudiation prevents a party from denying the authenticity of their communication or actions.

## Types of Cryptography

### **Symmetric Key Cryptography**

- **Key Sharing:** The same key is used for both encryption and decryption.
- **Examples:** DES (Data Encryption Standard), AES (Advanced Encryption Standard).
- The key is interchanged thought a secure channel (for example a diffie hellman algorithm)

### **Asymmetric Key Cryptography (Public Key Cryptography)**

- **Key Pairs:** Different keys are used for encryption and decryption.
- **Examples:** [[RSA]], ECC (Elliptic Curve Cryptography).

### **[[Hash]] Functions**

- **One-Way Transformation:** Hash functions produce a fixed-size output (hash) from variable-size input.
- **Purpose:** Ensures data integrity, used in digital signatures, password storage.
- **Examples:** SHA-256, MD5 (considered insecure).

### **[[Digital Signatures]]**

- **Authentication and Integrity:** Provides a mechanism for ensuring the authenticity and integrity of digital messages or documents.
- **Examples:** RSA Digital Signatures.

### **Public Key Infrastructure (PKI)**

- **Certificate Authorities (CAs):** Trusted entities that issue digital certificates.
- **Certificates:** Bind public keys to entities, enabling secure communication.

## Key Principles

### **Kerckhoffs's Principle**

- The security of a cryptographic system should **not depend** on the **secrecy of the algorithm** but rather on the secrecy of the keys.
- This means Algorithms should be public, with security relying on the strength of the key.

### **Perfect Forward Secrecy (PFS)**

- Even if a long-term secret key is compromised, past communication should remain secure.
- Use temporary session keys that are discarded after use.

### **Least Privilege Principle**

- Entities should have the minimum level of access necessary for their tasks.
- Limit access to cryptographic keys to only those who require them.