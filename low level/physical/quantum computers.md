Quantum computers represent a revolutionary paradigm in computing, leveraging the principles of quantum mechanics to perform calculations at **speeds** unimaginable with classical computers. Unlike classical computers that use [[binary#Units|bits]], quantum computers use quantum bits or **qubits**, allowing them to perform complex calculations simultaneously.

## Qubits vs. Bits

### Classical Bits

- Classical computers use bits as the basic unit of information, representing either a 0 or a 1.
- The processing of classical bits is sequential, limiting computational speed.

### Quantum Qubits

- Qubits, on the other hand, exploit quantum superposition and entanglement.
- They can exist in **multiple states** simultaneously, enabling parallel computation.
- This **inherent parallelism** contributes to the exponential increase in computational power.

## Quantum Advantage in Cryptography

While quantum computers promise groundbreaking advances, their potential impact on [[cryptography]] raises significant concerns.

### Shor's Algorithm

- Shor's algorithm, a quantum algorithm devised by mathematician Peter Shor, poses a substantial threat to existing cryptographic protocols.
- Classical cryptographic algorithms, like RSA and ECC, rely on the difficulty of certain mathematical problems (factorization and discrete logarithms).
- Shor's algorithm can efficiently solve these problems on a quantum computer, drastically reducing the time required for decryption.

### Accelerated Cryptanalysis

- Cryptographic protocols that would take classical computers an astronomically long time to break can be compromised in a matter of days or even hours using quantum computers.
- This accelerated cryptanalysis undermines the security foundations of current cryptographic systems.

## Post Quantum Cryptography

The vulnerabilities introduced by quantum computing necessitate the development of [[post quantum cryptography]] (PQC). PQC aims to create cryptographic algorithms that resist quantum attacks and maintain security in the quantum computing era.

### Transition Period

- As quantum computers advance, organizations are compelled to transition from classical to post-quantum cryptographic systems.
- PQC involves designing algorithms based on mathematical problems that remain difficult even for quantum computers.
