Mutual [[SSL|TLS]], also known as two-way [[SSL|TLS]], refers to a security protocol that ensures **bidirectional** authentication between two parties — typically a client and a server. It builds upon the standard TLS protocol by requiring both the server and the client to **authenticate each other** before any data is exchanged. This is particularly vital in **zero trust** environments where trust is never assumed and must be explicitly verified.

# theory

## How Mutual TLS Works

### The Handshake Process

In mutual TLS, the handshake process involves a few more steps than the typical [[SSL|TLS]] handshake:

1. The client begins the handshake by sending a "***ClientHello***" message to the server.
2. The server responds with a "***ServerHello***" message, along with its certificate and, optionally, a request for the client's certificate.
3. The client **verifies** the server's certificate against a **list of trusted CAs**.
4. If the server has requested client authentication, the client sends its certificate.
5. The server verifies the client's certificate.
6. Once mutual authentication is successful, symmetric encryption is established, and secure communication can begin. This is the same process that on [[SSL|TLS]] 
![[mTLS handshake.png]]

### Certificate Verification

Both parties must have a trusted **certificate authority** (CA) certificate to verify the identity of the other. The CA issues digital certificates that contain a public key and the identity of the owner.

## Where Mutual TLS Works

Mutual TLS is not limited by application protocols and can work with any that operate over TLS, such as [[REST]] or [[RPC]]

## Why Use Mutual TLS

### Security in Zero Trust Environments

In zero trust environments, trust is never implicit, and security is enforced by strict identity verification. mTLS provides such an identity assurance by requiring both ends of the communication to prove their identity to each other before any transaction of information.

### Data Protection

mTLS ensures that the data transmitted is only between the authenticated parties, reducing the risk of [[some attacks#man in the middle|Man in the middle]] attacks.
### Non-repudiation

With mTLS, both parties in the communication are authenticated, so actions and transactions cannot be repudiated later.

### when Not

In **most cases**, mTLS is an **over kill**, if you are creating a normal service you don't need it, only if you are a bank or something really important you should apply it. In other cases is mostly over engineering 
# practice

## create all necessary files
All of this process was done using oppenssl and a [[docker]] [[linux]] machine. 
### Create CA Key and Certificate
#### Generate the Root CA's Private Key
```bash
openssl genpkey -algorithm RSA -out ca-private-key.pem
```
#### Create the Root CA Certificate
```bash
openssl req -x509 -new -nodes -key ca-private-key.pem -sha256 -days 1024 -out ca-certificate.crt -extensions v3_ca
```
Using the private key, this command generates a new Root CA certificate which will be used to sign the server and client certificates.
**IMPORTANT** the Common name must be the same in all of the following steps, including the step bellow

###  Generate Server and Client Keys and Certificates 
#### Server Key and Certificate Signing Request (CSR)
##### Generate the Server's Private Key
```shell
openssl genpkey -algorithm RSA -out server-private-key.pem
```
##### Generate the CSR for the Server
```shell
openssl req -new -key server-private-key.pem -out server.csr -subj "/CN=127.0.0.1" -addext "subjectAltName = IP:127.0.0.1"
```
**IMPORTANT** as you can see, i set the common name (CN) to `127.0.0.1` that is the localhost ip, this means that only if the server gets a call from localhost it will approve, this is **NEEDS** to be changed for the cloud environment that you use 

#### Client Key and Certificate Signing Request (CSR)
##### Generate the Client's Private Key
```shell
openssl genpkey -algorithm RSA -out client-private-key.pem
```
##### Generate the CSR for the Client
```shell
openssl req -new -key client-private-key.pem -out client.csr -subj "/CN=127.0.0.1" -addext "subjectAltName = IP:127.0.0.1"
```
**IMPORTANT** once again, i have the CN as localhost, change it to your [[server]] [[IP]]
### Sign the Certificates Using the CA
#### Sign the Server's CSR to Create the Server Certificate
```shell
openssl x509 -req -in server.csr -CA ca-certificate.crt -CAkey ca-private-key.pem -CAcreateserial -out server-certificate.crt -days 365 -sha256 -extfile <(printf "subjectAltName=IP:127.0.0.1")
```
**IMPORTANT** the `subjectAltName` (SAN) is crucial for modern applications. SANs allow a certificate to be valid for multiple domain names or IP addresses, not just the CN. Currently i have it set up to an ip. but i could do it like this `-extfile <(printf "subjectAltName=DNS:your_domain")` this way it applies to any IP under the [[DNS]], making multiple machines save.

Either way, change it to your server ip or dns
#### Sign the Client's CSR to Create the Client Certificate
```shell
openssl x509 -req -in client.csr -CA ca-certificate.crt -CAkey ca-private-key.pem -CAcreateserial -out client-certificate.crt -days 365 -sha256 -extfile <(printf "subjectAltName=IP:127.0.0.1")
```
**IMPORTANT** once again, the value is on localhost, change it if needed
### Combine the keys and certificates
To use less files i recommend joining the private keys and certificates on a single file
```shell
cat server-private-key.pem server-certificate.crt > server-key-pair.pem 
cat client-private-key.pem client-certificate.crt > client-key-pair.pem
```

now you are done, transfer the files to your machine
These are the final files

![[mTLS files.png]]

## files to transfer
To your **Server**:
- `server-private-key.pem`
- `server-certificate.crt`
- `ca-certificate.crt`
To your **Client**:
- `client-private-key.pem`
- `client-certificate.crt`
- `ca-certificate.crt`

take into account that these are the exclusively necessary files for the mTLS to work, you can also keep your `ca-private-key.pem` if you want to modify these certificates
## Implementing the certificates 
Most of the current libraries that support TLS also support mTLS, so it's trivial to add it.
To see extended code of this check the project [[YoutubeClone]]
### typescript examples
#### fastify
```typescript
App.fastifyInstance = Fastify({
	https:{
		key: fs.readFileSync('./cert/server-private-key.pem'),
		cert: fs.readFileSync('./cert/server-certificate.crt'),
		ca: fs.readFileSync('./cert/ca-certificate.crt'),
		requestCert: true, // Request a certificate from clients
		rejectUnauthorized: true // clients need to provide a valid certificate  
            },
            logger: false
        });
```

#### gRPC server
```typescript
const serverKey = fs.readFileSync('./cert/server-private-key.pem');
const serverCert = fs.readFileSync('./cert/server-certificate.crt');
const caCert = fs.readFileSync('./cert/ca-certificate.crt');

const serverCredentials = ServerCredentials.createSsl(
  caCert,
  [{ cert_chain: serverCert, private_key: serverKey }],
  true // This enables client certificate checking, making the connection mutually authenticated
);

server.bindAsync("127.0.0.1:50000", serverCredentials, (error, port) => {
  if (error) {
	logger.error(`Failed to bind server: ${error}`);
	return;
	}
  server.start();
  logger.info(`gRPC server listening on port ${port}`);
});
```

#### gRPC client
```javascript
//grpc definition
const packageDef = loadSync("./src/proto/videoQueue.proto", {});
const grpcObject = loadPackageDefinition(packageDef);
const videoPackage = grpcObject.videoPackage;


const caCert = fs.readFileSync('./HighQualityMicroservice/cert/ca-certificate.crt');
const clientCert = fs.readFileSync('./HighQualityMicroservice/cert/client-certificate.crt');
const clientKey = fs.readFileSync('./HighQualityMicroservice/cert/client-private-key.pem');
  
const sslCreds = credentials.createSsl(caCert, clientKey, clientCert);
const client = new videoPackage.Video("127.0.0.1:50000", sslCreds);
```
### go examples


### what can go wrong

