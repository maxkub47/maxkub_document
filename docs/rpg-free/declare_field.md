---
id: 2
sidebar_position: 2
title: Structure
slug: /rpg-free/declare-field
---

### declare field

```RPGLE
**free

dcl-s string    char(10);
dcl-s num       zoned(7:0);
dcl-s num2      packed(7:2);
dcl-s num3      int(10);
dcl-s date1      date;
dcl-s ts        timestamp;
dcl-s Ind       ind;
dcl-c pi        3.14;

string  = 'hello';
num     = 10 ;
num2    = 11.5 ;
num3    = 20 ;
date1   = %date();
ts      = %timestamp();
Ind     = *on;

dsply string ;
dsply num;
dsply num2;
dsply num3;
dsply date1;
dsply ts ;
dsply Ind ;
dsply pi ;

*inlr = *on ;
```

### Data structure

```RPGLE
**free

dcl-ds ContractInfo_T Template;
    Mobile      packed(10);
    Email       char(50);
end-ds ;

dcl-ds StudentInfo inz Qualified;
    FullName    char(30);
        FirstName   char(15) Pos(1);
        LastName    char(15) Pos(16);
    Age         Packed(3);
    ContractInfo    likeds(ContractInfo_T);
end-ds ;

StudentInfo.FirstName = 'Rattapon';
StudentInfo.LastName = 'Liganporn' ;
StudentInfo.Age = 29;
StudentInfo.ContractInfo.Mobile = 08900000;
*inlr = *on  ;
```

```RPGLE
**free

dcl-ds GenericDate Qualified;
    Year        char(4);
    *N          Char(1);
    Month       char(2);
    *N          char(1);
    Day         char(2);
end-ds ;

GenericDate = '2022-08-25';
Dsply ('Year' + GenericDate.Year);
Dsply ('Month' + GenericDate.Month);
Dsply ('Day' + GenericDate.Day);

*inlr = *on ;
```

### Procedure

```RPGLE
**free

ctl-opt DftActGrp(*no);

dcl-pr TestPR End-pr ;

TestPR();
*inlr = *on ;

dcl-proc  TestPR ;
    dsply 'Inside Proc' ;
end-proc ;
```

### Procedure with parameter

```RPGLE
**free

ctl-opt DftActGrp(*no);

dcl-pr TestPR char(50);
    *N char(10);
End-pr ;

dcl-s name char(10);
dcl-s msg  char(50);
name = 'maxkub' ;
msg = TestPR(name);
*inlr = *on ;

dcl-proc  TestPR ;
    dcl-pi TestPR char(50);
        name char(10);
    end-pi;
    return ('Welcome' + name);
end-proc ;
```

### External Program

```RPGLE
**free

    ctl-opt DftActGrp(*no);

    dcl-pr Main     Extpgm('Exam7');
        *n      char(10);
    end-pr;

    dcl-pi Main ;
        Username    char(10);
    end-pi ;

    dsply ('Welcome' + %trim(Username) + ' to IBMi');
    *inlr = *on;
```
