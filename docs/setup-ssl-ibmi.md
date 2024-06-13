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

## Setup in NGINX

```javascript
events {}
http {
  # server {
  #   listen       9190;
  #   server_name EDUPGMR.METROSYSTEMS.CO.TH;
  #   return 301 https://172.16.1.240:9191$request_uri;
  #   location / {
  #     root   /qopensys/etc/nginx/html;
  #     index  index.html;
  #   }
  # }
  # upstream node_servers {
  #   server 172.16.1.240:9106;  
  # }
  server {

        location / {
          root  "/qopensys/etc/nginx/html/demo_aeon";  
          index  index.html index.htm;
          include /qopensys/etc/nginx/mime.types;
        }
        
        location /api {
          proxy_pass http://172.16.1.240:9106/;
          #proxy_pass https://172.16.1.240:9107/;
        }

        listen       9191 ssl;
        ssl_certificate      /www/phpcom/cert/certificate.crt;
        ssl_certificate_key  /www/phpcom/cert/certificate.key;
        ssl_session_cache    shared:SSL:1m;
        ssl_session_timeout  5m;
        ssl_protocols        TLSV1.1 TLSV1.2 TLSV1.3;

        ssl_ciphers  HIGH:!aNULL:!MD5;
        ssl_prefer_server_ciphers  on;

        server_name edupgmr EDUPGMR;
        # root  "/QOpenSys/etc/nginx/html/";  
    }
}
```

- command for nginx

```bash
nginx               //run
nginx -s stop       //stop
nginx -s reload     //restart
nginx -t            //test config
```
