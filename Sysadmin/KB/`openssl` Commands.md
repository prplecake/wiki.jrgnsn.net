To generate a new CSR with an existing private key:

```
openssl req -new -key <certificate.key> -out <certificate.csr>
```

To export a private key from a PFX:

```
openssl pkcs12 -in <certificate.pfx> -nocerts -out <certificate.key>
```

To combine certificate, certificate chain, and private key into PFX:

```
openssl pkcs12 -out <certificate.pfx> -inkey <certificate.key> -in <certificate.crt> -certfile <cert_bundle.crt>
```

To convert an “encrypted private key” to an “rsa private key”:

```
openssl rsa -in <encrypted.key> -out <rsa.key> -des3
```

To create a new CSR using a config file:

```
openssl req -nodes -newkey rsa:2048 -keyout <certificate.key> -out <certificate.csr>  -config <certificate.cnf>
```

Example config file:

```
[req]
distinguished_name = req_distinguished_name
req_extensions = req_ext
prompt = no

[req_distinguished_name]
C = US
ST = Minnesota
L = Minneapolis
O = Your Company
OU = Your Department
CN = example.com

[req_ext]
subjectAltName = @alt_names

[alt_names]
IP.1 = 192.168.1.5
IP.2 = <public IP>
DNS.1 = example.com
DNS.2 = <server-hostname>.example.com
```
