---
sidebar_position: 15
title: Setup SSL on IBMI
---
## Generate Local Cert

- create file .cnf

:::warning
CN and DNS ตรง subjectaltname ต้องตรงกัน
:::
```bash title="req.cnf"
[req]
distinguished_name = req_distinguished_name
x509_extensions = v3_req
prompt = no
[req_distinguished_name]
C = TH
ST = Bangkok
L = Bangkok
O = MSC
OU = IT
CN = edupgmr
[v3_req]
subjectAltName = DNS:edupgmr
basicConstraints     = CA:TRUE
subjectKeyIdentifier = hash
```
- Input Command to Create key
```bash
openssl req -x509 -sha256 -newkey rsa:2048 -keyout cert.key -out cert.crt -days 365 -nodes -config req.cnf
```

- compose .key and .crt to .pfx
:::warning
password '12345' (use in create digital cert)
:::

```bash 
openssl pkcs12 -export -nodes -out edupgmr.pfx -inkey cert.key -in cert.crt
```

## Mapping cert to Application
- Mapping cert to application server [Click](../docs/web-service/mapping-ssl.md)

## Mapping cert to Node.js
- Mapping cert to Node.js

```javascript
const https = require('https')
const path = require('path')
const fs = require('fs')

const sslServer = https.createServer({
  key: fs.readFileSync(path.join('/www/phpcom/cert','cert.key')),
  cert : fs.readFileSync(path.join('/www/phpcom/cert','cert.crt'))
}, app)

  sslServer.listen(9107 , () => console.log(`Run SSL Server in port 9107`))
```

