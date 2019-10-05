oracle sql links

https://www.oracle.com/database/technologies/appdev/sql.html

execution paths
- explain plan predicts how oracle will process your query
- execution plan describes steps oracle actually took

oracle playground
https://www.oracle.com/technetwork/database/application-development/livesql/index.html



https://www.webucator.com/database-training/course/oracle-sql.cfm

Idempotent - same results 


Update using correlated subquery

This statement uses a correlated subquery to update a single column across multiple rows in the FLIGHTS table. It increases the duration of all BA flights by thirty minutes.

The subquery returns all flights with OPERATING_CARRIER_CODE set to 'BA'. This result is used as the predicate value in the UPDATE statement. Thus, the value of the FLIGHT_DURATION column is updated for all rows FLIGHT_ID matches those returned by the query.

The SELECT statement displays the data in the FLIGHTS table and is used to verify that the update operation completed successfully.


update flights f1 
set    f1.flight_duration = f1.flight_duration + interval '30' minute 
where  f1.flight_id in (select f2.flight_id  
                        from   flights f2 
                        where  f2.operating_carrier_code = 'BA');
                        
select * from flights;


--------


Correlated update

This statement performs a correlated update of the rows in the FLIGHTS table. For all flights with OPERATING_CARRIER_CODE='BA' that depart on 1 Jan 2015 , it appends zero to the flight number and sets the flight duration to the duration of the AA flight on the same day and same route. It also sets the departure times for these flights to 11AM GMT.

The SELECT statement displays the updated contents of the FLIGHTS table and enables you to verify that the data has been successfully updated.


update flights f1 
set    f1.departure_datetime = timestamp'2015-01-01 11:00:00 -00:00', 
       (f1.flight_number, f1.flight_duration) = ( 
          select f2.flight_number || '0', f2.flight_duration 
          from   flights f2 
          where  f2.departure_airport_code = f1.departure_airport_code 
          and    f2.destination_airport_code = f1.destination_airport_code 
          and    trunc(f2.departure_datetime) = trunc(f2.departure_datetime) 
          and    f2.operating_carrier_code = 'AA' 
        ) 
where  f1.operating_carrier_code = 'BA' 
and    trunc(f1.departure_datetime) = date'2015-01-01';

select * from flights;
