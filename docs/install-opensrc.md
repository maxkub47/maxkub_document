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
