---
id: 4
sidebar_position: 4
title: Generate Certifiacate by Command
slug: /generate-cert-by-command
---

Ref. Doc : [Download](../assets/Create%20local%20cert%20from%20redhat%20,%20AS400%20and%20config%20https%20revise.xls)

## in Redhat

### create cert with this command

![](./img/generate-cert-by-command/1.png)

require <Hilight color="red"> subj </Hilight> information for browser google chrome
<br/>

<br/>

```shell
openssl req -x509 -sha256 -newkey rsa:2048 -keyout certificate.key -out certificate.crt -days 365 -nodes -subj "/CN=qcinspectiondev"
-addext "subjectAltName=DNS:qcinspectiondev"
```

![](./img/generate-cert-by-command/2.png)
![](./img/generate-cert-by-command/3.png)

### Setup HTTPD config

```shell
nano /etc/httpd/conf/httpd.conf
```

![](./img/generate-cert-by-command/4.png)

### Restart HTTPD Service

```shell
systemctl restart httpd
```

### Export Cert from chrome

![](./img/generate-cert-by-command/5.png)

![](./img/generate-cert-by-command/6.png)

![](./img/generate-cert-by-command/7.png)

![](./img/generate-cert-by-command/8.png)

![](./img/generate-cert-by-command/9.png)

![](./img/generate-cert-by-command/10.png)

![](./img/generate-cert-by-command/11.png)

![](./img/generate-cert-by-command/12.png)

### Certificate Install

![](./img/generate-cert-by-command/13.png) Double Click

![](./img/generate-cert-by-command/14.png)

![](./img/generate-cert-by-command/15.png)

## In AS400

### Upload config file to server

```cnf title="req.cnf"
[req]
distinguished_name = req_distinguished_name
x509_extensions = v3_req
prompt = no
[req_distinguished_name]
C = TH
ST = Samutprakan
L = Samutprakan
O = Isuzu Ltd
OU = IT
CN = isuzudev
[v3_req]
//highlight-start
subjectAltName = DNS:isuzudev
basicConstraints     = CA:TRUE
//highlight-end
subjectKeyIdentifier = hash
```

![](./img/generate-cert-by-command/16.png)

### access to terminal in AS400

```cmd
call qp2term
```

### Command for Create cert

```cmd
openssl req -x509 -sha256 -newkey rsa:2048 -keyout certificate.key -out certificate.crt -days 365 -nodes -config req.cnf
```

![](./img/generate-cert-by-command/17.png)

![](./img/generate-cert-by-command/18.png)

### Compose .key and .crt to .pfx

```cmd
openssl pkcs12 -export -nodes -out isuzudev.pfx -inkey certificate.key -in certificate.crt
```

<Hilight color="blue"> Password : 12345 </Hilight> <br/> <br/>

![](./img/generate-cert-by-command/19.png)

### Import to Digital Cert Manager

![](./img/generate-cert-by-command/19.png)

![](./img/generate-cert-by-command/20.png)

![](./img/generate-cert-by-command/21.png)

![](./img/generate-cert-by-command/22.png)

![](./img/generate-cert-by-command/23.png)

![](./img/generate-cert-by-command/24.png)

![](./img/generate-cert-by-command/25.png)

![](./img/generate-cert-by-command/26.png)

![](./img/generate-cert-by-command/27.png)

![](./img/generate-cert-by-command/28.png)

![](./img/generate-cert-by-command/29.png)

![](./img/generate-cert-by-command/30.png)

![](./img/generate-cert-by-command/31.png)

![](./img/generate-cert-by-command/32.png)

![](./img/generate-cert-by-command/33.png)

### config SSL

![](./img/generate-cert-by-command/34.png)

![](./img/generate-cert-by-command/35.png)

![](./img/generate-cert-by-command/36.png)

![](./img/generate-cert-by-command/37.png)

![](./img/generate-cert-by-command/38.png)

![](./img/generate-cert-by-command/39.png)

![](./img/generate-cert-by-command/40.png)

export const Hilight = ({children, color}) => (
<span
style={{
      backgroundColor: color,
      borderRadius: '20px',
      color: '#fff',
      padding: '10px',
      cursor: 'pointer',
    }}
onClick={() => {
alert(`You clicked the color ${color} with label ${children}`);
}}>
{children}
</span>
);
