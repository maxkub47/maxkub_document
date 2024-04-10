---
id: 3
sidebar_position: 3
title: Example 1
slug: /rpg-free/exam1
---

Refference (https://developer.ibm.com/tutorials/i-rest-web-services-server3/)

```RPGLE
ctl-opt nomain
        pgminfo(*PCML:
                *MODULE:
                *DCLCASE) ;

dcl-f STUDENTDB keyed usage(*update:*output:*delete);


dcl-c H_OK             200 ;
dcl-c H_CREATED        201 ;
dcl-c H_NOCONTENT      204 ;
dcl-c H_BADREQUEST     400 ;
dcl-c H_NOTFOUND       404 ;
dcl-c H_CONFLICT       409 ;
dcl-c H_GONE           410 ;
dcl-c H_SERVERERROR    500 ;
dcl-c ERR_DUPLICATE_WRITE   01021;

dcl-ds studentRec   qualified Template ;
    studentID   Char(9);
    firstName   char(50);
    lastName    char(50);
    gender      char(10);
end-ds ;

dcl-pr openStudentDB int(10) end-pr ;
dcl-pr closeStudentDB int(10) end-pr ;


dcl-pr getAll ;
    students_length  int(10:0) ;
    students     likeds(studentRec) dim(1000) options(*varsize);
    httpStatus   int(10:0) ;
    httpHeaders  char(100) dim(10);
end-pr;

dcl-pr getByID ;
    studentID    char(9) const ;
    student      likeds(studentRec) ;
    httpStatus   int(10:0)   ;
    httpHeaders  char(100) dim(10);
end-pr;

dcl-pr create ;
    student      likeds(studentRec) ;
    httpStatus   int(10:0)   ;
    httpHeaders  char(100) dim(10);
end-pr;

dcl-pr update ;
    student      likeds(studentRec) ;
    httpStatus   int(10:0)   ;
end-pr ;

dcl-pr remove ;
    studentID    char(9) const ;
    httpStatus   int(10:0) ;
end-pr ;

// ------------------------------------------------------------------------------------
// openStudentDB
// ------------------------------------------------------------------------------------
dcl-proc openStudentDB;

    dcl-pi openStudentDB int(10) end-pi;

    if NOT %open(STUDENTDB);
        open(e) STUDENTDB;
        if %ERROR;
            return 0;
        endif;
    endif;

    return 1;

end-proc;

// ------------------------------------------------------------------------------------
// closeStudentDB
// ------------------------------------------------------------------------------------
dcl-proc closeStudentDB;

    dcl-pi closeStudentDB int(10) end-pi;
    if  %open(STUDENTDB);
        close(e) STUDENTDB;
        if %ERROR;
            return 0;
        endif;
    endif;

    return 1;

end-proc;


// ------------------------------------------------------------------------------------
// getAll
// ------------------------------------------------------------------------------------
dcl-proc getAll export ;
    dcl-pi getAll  ;
        students_length     int(10:0)  ;
        students            likeds(studentRec) dim(1000) options(*varsize);
        httpStatus          int(10:0)   ;
        httpHeaders         char(100) dim(10);
    end-pi;

    clear httpHeaders;
    clear students;
    students_length = 0;

    openStudentDB();

    setll *loval studentDB ;
    read(e) studentR;

    if (%ERROR);
        httpStatus = H_SERVERERROR ;
        return;
    endif;

    dow (NOT %eof);
        students_length = students_length + 1 ;
        students(students_length).StudentID = studentID ;
        students(students_length).FirstName = firstName ;
        students(students_length).LastName = lastName ;
        students(students_length).Gender = gender ;

        read(e) studentR;
        if (%ERROR);
        httpStatus = H_SERVERERROR ;
        return;
        endif;
    enddo;
    httpStatus = H_OK;
    httpHeaders(1) = 'Cache-Control: no-cache, no-store';

    closeStudentDB();
end-proc;

// ------------------------------------------------------------------------------------
// getByID
// ------------------------------------------------------------------------------------
dcl-proc getByID export ;

    dcl-pi getByID ;
        studentID           char(9) const;
        student             likeds(studentRec) ;
        httpStatus          int(10:0)   ;
        httpHeaders          char(100) dim(10);
    end-pi;
    clear httpHeaders;
    clear student;

    openStudentDB();

    chain(e) studentID STUDENTDB;
    if (%ERROR);
        httpStatus = H_SERVERERROR;
        return;
    elseif %FOUND;
        student.studentID = studentID;
        student.firstName = firstName;
        student.lastName  = lastName;
        student.gender    = gender;

        httpStatus = H_OK;
    else;
        httpStatus = H_NOTFOUND;
    endif;

 httpHeaders(1) = 'Cache‑Control: no‑cache, no‑store';

 closeStudentDB();

end-proc;

// ------------------------------------------------------------------------------------
// create
// ------------------------------------------------------------------------------------
dcl-proc create export ;

    dcl-pi create ;
        student             likeds(studentRec);
        httpStatus          int(10:0)   ;
        httpHeaders          char(100) dim(10);
    end-pi;

    openStudentDB();

    studentID = student.studentID;
    firstName = student.firstName;
    lastName  = student.lastName;
    gender    = student.gender;

    write(e) studentR;
    if NOT %ERROR;
        httpStatus = H_CREATED;
        httpHeaders(1) = 'LOCATION: ' + 'http://server/web/service/maxtest1/' + studentID;
    elseif %STATUS = ERR_DUPLICATE_WRITE;
        httpStatus = H_CONFLICT;
    else;
        httpStatus = H_SERVERERROR;
    endif;

 closeStudentDB();
end-proc;

// ------------------------------------------------------------------------------------
// update
// ------------------------------------------------------------------------------------
dcl-proc update export ;

    dcl-pi update ;
        student             likeds(studentRec) ;
        httpStatus          int(10:0)   ;
    end-pi;

    openStudentDB();

    chain(e) student.studentID STUDENTDB;
    if (%ERROR);
        httpStatus = H_SERVERERROR;
        return;
    elseif %FOUND;
        studentID = student.studentID;
        firstName = student.firstName;
        lastName  = student.lastName;
        gender    = student.gender;

    update(e) studentR;
    if NOT %ERROR;
        httpStatus = H_NOCONTENT;
    else;
        httpStatus = H_NOTFOUND;
    endif;
    else;
        httpStatus = H_NOTFOUND;
    endif;

    closeStudentDB();

end-proc;

// ------------------------------------------------------------------------------------
// remove
// ------------------------------------------------------------------------------------
dcl-proc remove export ;

    dcl-pi remove ;
        studentID    char(9) const ;
        httpStatus          int(10:0)   ;
    end-pi;

    openStudentDB();

    chain(e) studentID STUDENTDB;
    if (%ERROR);
        httpStatus = H_SERVERERROR;
        return;
    elseif %FOUND;
        delete(e) studentR;
        if NOT %ERROR;
            httpStatus = H_NOCONTENT;
        elseif NOT %FOUND;
            httpStatus = H_NOTFOUND;
        else;
        httpStatus = H_SERVERERROR;
        endif;
    else;
        httpStatus = H_NOTFOUND;
    endif;

    closeStudentDB();

end-proc;
```
