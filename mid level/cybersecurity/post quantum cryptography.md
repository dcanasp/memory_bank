Post-Quantum Cryptography (PQC) is a field of study that focuses on cryptographic algorithms designed to **resist** the potential threat posed by [[quantum computers]]. Traditional cryptographic systems, such as [[RSA]] and ECC, rely on the difficulty of certain mathematical problems, like integer factorization or discrete logarithms, which can be efficiently solved by quantum computers using algorithms like Shor's algorithm.

## The Problem

The advent of quantum computers raises concerns about the **security** of current cryptographic systems. Once sufficiently powerful quantum computers become available, they could break widely-used encryption methods, compromising the confidentiality and integrity of sensitive data 
## Potential Attacks

### Gauss-Jordan Attack with Noise
involves introducing noise in the matrix multiplication process, particularly in Gauss-Jordan elimination, a fundamental linear algebra algorithm.

#### How it Works

- Traditional matrix multiplication is modified by adding noise to the result.
- The noise introduced during multiplication is not simply additive but multiplies with the matrix elements.
- This process generates a new matrix that exhibits scaling properties conducive to quantum attacks.
#### Applicability
- The Gauss-Jordan attack with noise is not limited to quantum computers; it can be **executed** on **conventional computers**, even those using the [[von Neumann architecture]].
### Hybrid RSA Certificates

To address the quantum threat, a strategy involves combining classical cryptographic algorithms with post-quantum cryptography. Hybrid RSA certificates are an example of this approach.

#### How it Works

- Hybrid RSA certificates allow the inclusion of post-quantum cryptographic keys alongside traditional RSA keys in digital certificates.
- Even in regions where local authorities might not permit the full adoption of post-quantum algorithms, hybrid certificates provide a means to enhance security.

#### Applicability

- This approach enables organizations to **prepare** for the quantum era without violating **existing regulations**.
- It serves as a practical bridge between conventional and post-quantum cryptographic systems.