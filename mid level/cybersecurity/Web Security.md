# When to Implement Security Measures

- Security should be a primary consideration from the **start** of **design** and **architecture**.
- Any point where the **user interacts** with the application, especially during **login**, data **submission**, and data **retrieval**
- Ensuring data is **securely transmitted** and **stored**, particularly sensitive data like personal information and credentials.
- When you are using any type of [[Communication]] to other servers, even if the users don't see this 
- Regularly update and patch the application, having logs and a fallback system
# Must do's for web Security
## Storing Passwords
When storing a password you never stored them on plaint text, you should use:
- **Hashing**, Use cryptographic [[hash]] functions, ensuring passwords can't be easily deciphered if the hash is accessed.
- **Salting**, Add a unique, random string to each password before hashing to prevent attacks [[some attacks#Dictionary Attacks||Dictionary Attacks]]
- **Peppering**, (optional). an additional layer of security by adding a secret value (pepper) to the hashing process

## User verification

### JWT (JSON Web Tokens)
A token that stores a payload, can be seen by anyone, but it's signed as only you can issue a **valid token** with your JWT **secret**
- Ideal for **stateless** authentication in systems.
- JWTs are compact, URL-safe tokens that contain a JSON payload with user identity claims. They are digitally signed for integrity and optionally encrypted.
- Implement robust signature verification, manage **token expiration** effectively, if possible create **2 tokens**, and access one and a refresh one, and secure token storage on the client side.

### Session Tokens
Keeping the users that are currently connected to you on the server, usually on the database
- Traditionally used in web applications where **maintaining state** is required.
- Store session tokens as cookies with appropriate attributes like HttpOnly, Secure, and SameSite.
- Sessions are stored on the server, which maps session tokens to user information. This is more memory-intensive than JWTs.

### OAUTH
A **third party** service that ensures a perfect authentication, They use multiple servers and tokens to do this.
- If you don't trust yourself or want Absolute certainty


## [[HTTPS]]

- **Encrypts** data transmitted between client and server, preventing [[some attacks#Man in the Middle (MitM)||Man in the middle]] attacks and [[some attacks#Eavesdropping||eavesdropping]].
- Use [[SSL||TLS]] (Transport Layer Security) to secure all communications. Employ certificates from trusted Certificate Authorities (CAs).

## CORS

When your server doesn't need to be public, **DON'T** make it **public**, you can authorize only some [[IP]]'s to access it. This Specially applies to the [[database]], They should **NEVER** be public, only the [[server]] [[IP]] should access it  
# recommended  

## logging

Having a good logging system can save your application, it should be allow you to track any user that might have unusual activity. it's very important not overlogging and never logging passwords or anything sensitive
## input validation and sanitization

Most common to prevent [[sql injections]], use Prepared statements. But also prevent any other injection type, images, documents, they could be a breach on security

## rate limiting and CAPTCHA

rate limiters stop [[some attacks#DOS (Denial of Service)||DOS]] attacks, one of the simplest to perform but lethal. You block the [[IP]]'s of the users that are making to many request at a given time. This is fairly simple unless you are using an [[ApiGateway]] or a [[Load balancer]] if so you have to use extra care when implementing this (as all the request will pass first to those entities)

Captchas allows you to identify the humans from the bots, this is incredibly useful for preventing unwanted usage

## database / secrets management

It's worth mentioning that your secrets and passwords should be stored securely, you can use a dedicated service like aws secrets management or GitHub secrets. Please, don't commit .env

In databases is really good to create users with special privileges, the user that the server uses should NEVER have the privilege to drop tables, it should only have the bare minimum

## fallback / backups

Things will go wrong, and you will be attacked, you have to be ready to face this. Have logs, drop the databases, have scripts that stop production if needed, Turn off servers, you have to be ready

Always have backups of your data, but don't store it on the same server, have them scattered, but if something happens you can delete all of the compromised servers if needed
