The name many times is used to refer to TSL, NO se debe usar SSL. 

usa SHA-256


# con oppenssl

```bash
openssl genpkey -algorithm RSA -out private-key.pem

openssl req -new -key private-key.pem -out certificate.csr

cat private-key.pem signed-certificate.crt > key-pair.pem


openssl x509 -signkey key-pair.pem -in certificate.csr -req -days 365 -out certificate.crt
```

estos tienen que estar en algun web [[server]] software [[nginx]] or [[httpd]] 