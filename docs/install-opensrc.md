---
sidebar_position: 12
title: Install Opensource in IBM i
---

## install YUM

link : [ https://bitbucket.org/ibmi/opensource/src/20192a55b76d99a839815f61100e427ac75cdd11/docs/yum/#markdown-header-offline-install-instructions-without-acs ]

- Download bootstrap.sh and bootstrap.tar.Z to your PC
- Upload bootstrap.sh and bootstrap.tar.Z to your IBM i

``` shell
scp -r ./bootstrap.sh ./bootstrap.tar.Z ibmi@192.168.1.10:/tmp
```

- From a 5250 terminal run the following.

``` shell
QSH CMD('touch -C 819 /tmp/bootstrap.log; /QOpenSys/usr/bin/ksh /tmp/bootstrap.sh > /tmp/bootstrap.log 2>&1')
```

- check the log file

``` shell
cat /tmp/bootstrap.log
```

- check the /QOpenSys/etc must found ***yum*** Use for online
- check the /QOpenSys/pkgs/lib must found ***rpm*** Use for offine
- check repo for yum in /QOpenSys/etc/yum

``` shell
cat /QOpenSys/etc/yum/repos.d/ibmi-base.repo
```

## Export PATH

``` shell
cd /home         *for all user profile 
cd /home/max     *for user profile max

touch .profile
echo 'PATH=/QOpenSys/pkgs/bin:$PATH' >> .profile
echo 'export PATH' >> .profile
export PATH=/QOpenSys/pkgs/lib/
```

## Install opensource via online

``` shell
yum install -y opensource
```

## Install opensource via offine

link for download : [ https://public.dhe.ibm.com/software/ibmi/products/pase/rpms/repo-base-7.3/ppc64/ ]

``` shell
rpm -i filename.rpm

### before unixODBC-2.3.9-1.ppc64
rpm -i grep-gnu-3.0-2.ibmi7.2.ppc64.rpm
rpm -i libtool-2.4.6-5.ibmi7.2.ppc64.rpm
rpm -i libodbc2-2.3.9-1.ibmi7.2.ppc64.rpm

rpm -i unixODBC-2.3.9-1.ppc64.rpm
```

## Install PM2

``` shell
npm install -g pm2

##create .PM2
cd /QopenSys/pkgs/lib/nodejs20/lib/node_modules/pm2/bin
pm2 list

##set $PATH
PATH=/QOpenSys/pkgs/lib/nodejs20/lib/node_modules/pm2/bin:$PATH

```

## Text NodeJS

``` shell
cd /www/apachedft/htdocs
touch node.js
```

``` javascript title='EXAMPLE'
// server.mjs
var http = require('http');

http.createServer(function(req, res) => {
  res.writeHead(200, { 'Content-Type': 'text/plain' });
  res.end('Hello World!');
}).listen(8080);

```

``` javascript title='EXAMPLE2'
// server.mjs
import { createServer } from 'node:http';

const server = createServer((req, res) => {
  res.writeHead(200, { 'Content-Type': 'text/plain' });
  res.end('Hello World!\n');
});

// starts a simple http server locally on port 3000
server.listen(3000, '127.0.0.1', () => {
  console.log('Listening on 127.0.0.1:3000');
});

// run with `node server.mjs`
```

### Command use

``` shell
yum install -y [opensource]
rpm -i [filename.rpm]
ps -ef
kill [PID]
yum list
```
