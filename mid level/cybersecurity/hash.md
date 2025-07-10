A cryptographic hash function is a mathematical algorithm that converts an input (or 'message') into a fixed-size string of bytes, typically a hash, which appears random. The output is unique to each unique input.

**Key Characteristics:**

- The same input will always produce the same output.
- The hash value is quickly computed from its input.
- It should be computationally infeasible to reverse the hash function (i.e., find the input from its hash).
- A minor change in the input (even a single bit) should produce a significantly different output.
- It should be highly unlikely (computationally infeasible) to find two different inputs that produce the same output. (this has happened with the first hashes like MD5)

**Common Algorithms:**

- **Argon2**: One of the currently best algorithms 
- **SHA-256**: Part of the SHA-2 family, widely used and considered secure.
- **SHA-3**: Newest member, an alternative to SHA-2, not a replacement.
- **MD5**: Mostly obsolete due to vulnerabilities.
- **SHA-1**: Initially designed by the NSA, now considered weak against well-funded attackers.

**Use Cases:**

1. **Data Integrity**: Ensuring that data has not been altered.
2. **Password Storage**: Storing passwords securely in a database.
3. **Digital Signatures**: Part of the process for creating a [[digital signatures]].
4. **Blockchain and Cryptocurrencies**: Fundamental in the mechanism of blockchain technology.

**Considerations:**

- **Security**: Continuously evolving; what is secure today may not be secure tomorrow due to advances in computing power and cryptographic research such like [[post quantum cryptography]].
- **Hash Speed vs. Security**: Faster hash functions are desirable for performance but can be less secure; slower hash functions are more secure but can be computationally expensive.
- **Applications**: The choice of hash function depends on the specific use case, considering factors like sensitivity of data, required security level, and system performance constraints.
### Salt (is public)

1. A salt is a random value that is added to the input of a hash function to create a unique hash.
2. The primary purpose of a salt is to defend against [[some attacks|dictionary attacks]] or attacks using pre-computed hash tables, like rainbow tables.
3. Should be unique for each password, so it should be stored on the [[mid level/databases/Database]]
4. **Usage**:
    - When a password is stored, a new, random salt is generated and concatenated with the password.
    - The hash function is then applied to this combination, and both the salt and the hashed result are stored.
    - To verify a password, the stored salt is added to the provided password, and the hash is computed again. If the computed hash matches the stored hash, the password is correct.
5. **Characteristics**:
    - Salts are unique for each user or password instance.
    - They are **not secret** and can be stored in the open, typically alongside the hash in the database.
    - The effectiveness of a salt lies in its ability to ensure that the hash results for the same password are unique across different instances, thus thwarting pre-computed hash table attacks.

### Pepper (private)

1. A pepper is similar to a salt but is used as a secret key added to the password before hashing.
2. The pepper adds an additional layer of security by incorporating a value unknown to potential attackers, making [[some attacks|brute force]] attacks more difficult.
3. **Usage**:
    - Unlike a salt, a pepper is typically a fixed value used across all password hashes.
    - The pepper can be stored separately from the database, often in application code or a separate configuration file or environment variable.
    - It's combined with the password (and possibly a salt) before applying the hash function.
4. **Characteristics**:
    - The pepper is a **secret value** and should be protected accordingly.
    - Since it's not stored with each password hash, it significantly increases the difficulty of brute-force attacks even if the database is compromised.
    - The use of a pepper is less common than a salt and is typically implemented for high-security applications.

### Salt and Pepper Together

- Using both a salt and a pepper provides two layers of security: the **salt** ensures **uniqueness** and defends against pre-computed attacks, while the **pepper** adds an **extra secret component** to guard against database compromises.
- This dual approach is more robust but requires careful implementation to maintain the secrecy of the pepper and the uniqueness of the salt.

>[!important]
>Most of the libraries include a random salt for each hash, argon2 and bcrypt for node do this, in this cases you don't need to store the salt on the database. for example on argon2 the hash:
>`$argon2id\$v=19\$m=65536,t=3,p=4\$Q77HkNUphNWymMjFywdqdg\$cxvoNJeliASdBufFQn/GDJ2qAFQz7/YPSMcNrqnqFr8 `
>in between the `\$\$` has the data as what algorithms is, the version, memory, paralelism, and the cicles. And after that, there is the salt, in this case `Q77`... is the salt of that hash
>
### code example

```node
const argon2 = require('argon2');
const crypto = require('crypto');
const pepper = 'yourSecurePepperHere';
async function hashPassword(password) {
    try {
        const salt = crypto.randomBytes(16);
        const pepperedPassword = password + pepper;
        const hash = await argon2.hash(pepperedPassword, { salt: salt });
        return { hash, salt: salt.toString('hex') };
    } catch (err) {
        console.error(err);
    }
}

async function verifyPassword(storedHash, storedSalt, passwordToVerify) {
    try {
        const pepperedPassword = passwordToVerify + pepper;
        const saltBuffer = Buffer.from(storedSalt, 'hex');
        const match = await argon2.verify(storedHash, pepperedPassword, { salt: saltBuffer });
        return match;
    } catch (err) {
        console.error(err);
    }
}

// Example usage
(async () => {
    const password = 'examplePassword';
    const { hash, salt } = await hashPassword(password);

    console.log('Hash:', hash);
    console.log('Salt:', salt);

    const isVerified = await verifyPassword(hash, salt, password);
    console.log('Password is verified:', isVerified);
})();

```