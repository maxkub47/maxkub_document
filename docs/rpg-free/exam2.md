---
sidebar_position: 4
title: Example_1 Flight
---

```SQLRPGLE
**free
ctl-opt nomain 
        pgminfo(*PCML:
                *MODULE:*DCLCASE) ;


dcl-c H_OK             200 ; 
dcl-c H_CREATED        201 ;
dcl-c H_NOCONTENT      204 ;
dcl-c H_BADREQUEST     400 ;
dcl-c H_NOTFOUND       404 ;  
dcl-c H_CONFLICT       409 ;
dcl-c H_GONE           410 ;   
dcl-c H_SERVERERROR    500 ;  

// dcl-s test1 like(customers.CUSTO00002);

// dcl-ds orders extname('FLGHT400/ORDERS') qualified end-ds;
// dcl-ds flights extname('FLGHT400/FLIGHTS') qualified end-ds;
// dcl-ds customers extname('FLGHT400/CUSTOMERS') qualified end-ds;
// dcl-ds airline extname('FLGHT400/AIRLINE') qualified end-ds;

dcl-ds data  qualified ; 
    textTrip char(50);
    customerName char(64);
    orders zoned(9:0);
    airLine char(3);
    airlineName char(16);
    flightNumber zoned(9:0);
    departureInitials char(16);
    departure char(16);
    departureDate char(32);
    departureTime char(32);
    arrivalTime char(32);
    mileage zoned(9:0);
    arrivalInitials char(16);
    arrival char(16);
    class char(1);
    ticketsOrdered zoned(9:0); 
    ticketPrice char(22) ;
    tax zoned(12:2);
    total zoned(12:2);
end-ds;

///
// APPERRC template
// Used for error capturing
///
dcl-ds APIERRC_T Qualified Template;
  bytesProvided Int(10:0); // Inz(%size(ApiErrC))
  bytesAvailable Int(10:0);
  exceptionID Char(7);
  reserved Char(1);
  exceptionData Char(3000);
end-ds;

dcl-pr getData ;
    orders       zoned(9:0) const ;
    datas        likeds(data) ;
    httpStatus   int(10:0);
    httpHeaders  char(100) dim(10);
end-pr;
// ------------------------------------------------------------------------------------
// Get lib All
// ------------------------------------------------------------------------------------
dcl-proc getData export ;

    dcl-pi getData ;
        orders       zoned(9:0) const ;
        datas        likeds(data) ;
        httpStatus   int(10:0);
        httpHeaders  char(100) dim(10);
    end-pi;

    clear httpHeaders;
    clear datas ; 

    exec sql select 
        varchar_format(flght400.orders.departure_date, 'dd MON YYYY') || ' TRIP TO ' || Upper(flght400.flights.ARRIVAL) as text1 , 
        flght400.customers.customer_name,
        flght400.orders.order_number,
        FLGHT400.AIRLINE.AIRLIN,
        FLGHT400.AIRLINE.AIRLNM,
        flght400.orders.flight_number,
        flght400.flights.DEPARTURE_INITIALS,
        flght400.flights.DEPARTURE,
        flght400.orders.DEPARTURE_DATE,
        flght400.flights.departure_time,
        flght400.flights.ARRIVAL_TIME,
        flght400.flights.MILEAGE,
        flght400.flights.ARRIVAL_INITIALS,
        flght400.flights.ARRIVAL,
        flght400.orders.class,
        flght400.orders.TICKETS_ORDERED,
        flght400.flights.TICKET_PRICE,
        cast(flght400.flights.TICKET_PRICE as int) * 0.04 as tax ,
        cast(flght400.flights.TICKET_PRICE as int) + (cast(flght400.flights.TICKET_PRICE as int) * 0.04) as total 
    into 
        :datas
    from flght400.orders 
    join flght400.flights on flght400.orders.flight_number = flght400.flights.flight_number
    join flght400.customers on flght400.orders.customer_no = flght400.customers.customer_no
    join flght400.airline on flght400.airline.airlin = FLGHT400.FLIGHTS.airlines
    where
        flght400.orders.ORDER_NUMBER = :orders ;
    

    if sqlstt <> '00000';
        httpStatus = H_SERVERERROR;
        return;
    endif;
       
    httpStatus = H_OK;
    httpHeaders(1) = 'Cache-Control: no-cache, no-store' ;
    
end-proc;
```
