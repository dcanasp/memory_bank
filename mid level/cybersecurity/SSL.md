The name many times is used to refer to TSL, SSL is the older version and should NOT be used. 

uses the [[hash]] SHA-256
## creating [[digital certificates]] with oppenssl
first of all 
`apk add openssl`

```bash
openssl genpkey -algorithm RSA -out private-key.pem

openssl req -new -key private-key.pem -out certificate.csr

cat private-key.pem signed-certificate.crt > key-pair.pem


openssl x509 -signkey key-pair.pem -in certificate.csr -req -days 365 -out certificate.crt
```


this have to be in some web [[server]] software, so you can add it to your express server on typescript, or on your net/http client on Go. The other way is to do it on a reverse proxy like [[nginx]] or [[httpd]] 
