---
id: 1
sidebar_position: 1
title: Spec
slug: /spec
---

## Spec H

```rpg
**free
ctl-opt     debug(*yes) ;
ctl-opt     option(*nodebugio: *srcstmt: *noshowcpy) ;
ctl-opt     copyright('www.Maxkub.com');
ctl-opt     DftActGrp(*no) actgrp(*caller)
ctl-opt     bnddir('bnddir1')
ctl-opt     nomain;
ctl-opt     alwnull(*usrctl)
ctl-opt     fixnbr(*zoned:*inputpacked)
ctl-opt     datfmt(*ISO)
ctl-opt     timfmt(*ISO)
ctl opt     ccsid(*ucs2 : 1200)
```

## Spec F

### Declare File

```RPGLE

       FFilename++IPEASF.....L.....A.Device+.Keywords+++++++++++++++++++++++++ */
       FFILE1     IF   E             DISK

/*free
    dcl-f File1 ;
//or
    dcl-f File1 disk(*ext)  usage (*input);
    dcl-f File1 disk  usage (*input);
*/
```

### Declare File with keys

```RPGLE
FFilename++IPEASF.....L.....A.Device+.Keywords+++++++++++++++++++++++++ */
       FFILE1     IF   E           K DISK

/free
    dcl-f File1 keyed ;
//or
    dcl-f File1 disk(*ext) keyed usage (*input);
    dcl-f File1 disk keyed usage (*input);
/endfree
```

### Declare File with keys and rename

```RPGLE
       FFilename++IPEASF.....L.....A.Device+.Keywords+++++++++++++++++++++++++ */
        FFILE1     IF   E           K DISK    RENAME(RFILE1:RFILE1CHG)
                                              PREFIX(X)
/free
    dcl-f File1 keyed rename(rfile1:rfile1chg) prefix(X);
//or
    dcl-f File1 disk(*ext) keyed usage (*input) rename(rfile1:rfile1chg) prefix(X) ;
    dcl-f File1 disk keyed usage (*input)rename(rfile1:rfile1chg) prefix(X) ;
/endfree
```

### Declare File with Update

```RPGLE
       FFilename++IPEASF.....L.....A.Device+.Keywords+++++++++++++++++++++++++ */
        FFILE1     IF   E           K DISK    RENAME(RFILE1:RFILE1CHG)
                                              PREFIX(X)
/free
    dcl-f File1 keyed rename(rfile1:rfile1chg) prefix(X);
//or
    dcl-f File1 disk(*ext) keyed usage (*input) rename(rfile1:rfile1chg) prefix(X) ;
    dcl-f File1 disk keyed usage (*input)rename(rfile1:rfile1chg) prefix(X) ;
/endfree
```

### Declare File with read and write

```freeformat
       FFilename++IPEASF.....L.....A.Device+.Keywords+++++++++++++++++++++++++ */
        FFILE1     IF A E           K DISK

/free
    dcl-f File1 keyed usage(*input:*output)
//or
    dcl-f File1 disk(*ext) keyed usage (*input:*output)  ;
    dcl-f File1 disk keyed usage (*input*output) ;
/endfree

```

### Declare File with external file

```freeformat
      FFilename++IPEASF.....L.....A.Device+.Keywords+++++++++++++++++++++++++ */
         FFILE1     IF A E           K DISK    EXTFILE('EASYCLASS/FILE1')

/free
    dcl-f File1 keyed EXTFILE('EASYCLASS/FILE1')
//or
    dcl-f File1 disk(*ext) keyed usage (*input:*output) EXTFILE('EASYCLASS/FILE1')  ;
    dcl-f File1 disk keyed usage (*input*output) EXTFILE('EASYCLASS/FILE1') ;
/endfree

```

### Declare File with external Member

```freeformat
     FFilename++IPEASF.....L.....A.Device+.Keywords+++++++++++++++++++++++++ */
         FFILE1     IF A E           K DISK    EXTMBR('MBR1')

/free
    dcl-f File1 keyed EXTMBR('MBR1')
//or
    dcl-f File1 disk(*ext) keyed usage (*input:*output) EXTMBR('MBR1')  ;
    dcl-f File1 disk keyed usage (*input*output) EXTMBR('MBR1');
/endfree
```
