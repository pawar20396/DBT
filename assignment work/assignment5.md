1. Display employees where the first name or last name starts
with S.

->select FIRST_NAME,LAST_NAME from employees
  where FIRST_NAME LIKE'S%' OR LAST_NAME LIKE'S%';

2. Display first name and last name after converting the first letter
of each name to upper case and the rest to lower case.

->SELECT UPPER(FIRST_NAME) FROM employees;

3. Display the first word in job title.

->

4. Display the length of first name for employees where last name
contain character ‘b’ after 3rd position.

->select LENGTH(FIRST_NAME)FIRST_NAME, LAST_NAME from employees
  where LAST_NAME like '___b%';

5. Display first name in upper case and email address in lower
case for employees where the first name and email address are
same irrespective of the case.

-> select UPPER(FIRST_NAME),LOWER(EMAIL) from employees
   where FIRST_NAME=EMAIL;

6. Display first name, salary, and round the salary to thousands.

-> SELECT FIRST_NAME,SALARY,ROUND(SALARY) FROM employees;
   

7. Display manager ID and number of employees managed by the
manager.

->select MANAGER_ID,count(EMPLOYEE_ID) from employees
  group by MANAGER_ID;

8. Display employee ID and the date on which he ended his
previous job.

->select EMPLOYEE_ID, DATE_SUB(HIRE_DATE,INTERVAL 1 DAY) from employees; 							 

9. Display the country ID and number of cities we have in the
country.

->select l.COUNTRY_ID,count(CITY)
FROM locations l INNER JOIN countries c
ON l.COUNTRY_ID=c.COUNTRY_ID
GROUP BY l.COUNTRY_ID;

10. Display average salary of employees in each department who
have commission percentage.

->select DEPARTMENT_ID ,AVG(SALARY) FROM employees
  where COMMISSION_PCT!=0
  GROUP BY DEPARTMENT_ID;


11. Display job ID, number of employees, sum of salary, and
difference between highest salary and lowest salary of the
employees of the job.

-> select JOB_ID,COUNT(EMPLOYEE_ID),SUM(SALARY),MAX(SALARY)-MIN(SALARY) FROM employees
   group by JOB_ID;


12. Display job ID for jobs with average salary more than 10000.

-> select JOB_ID,AVG(SALARY) FROM employees
   WHERE SALARY>10000
   GROUP BY JOB_ID;


13. Display years in which more than 10 employees joined.

->select YEAR(HIRE_DATE) new,EMPLOYEE_ID  FROM employees
 group by EMPLOYEE_ID 
having new>10; 									


14. Display departments in which more than five employees have
commission percentage.

->SELECT DEPARTMENT_ID, count(EMPLOYEE_ID) from employees
 where COMMISSION_PCT > 0 
group by DEPARTMENT_ID;


15. Display employee ID for employees who did more than one job
in the past.

->select e.EMPLOYEE_ID 
  from employees e INNER JOIN job_history jh
  ON e.EMPLOYEE_ID=jh.EMPLOYEE_ID

16. Display job ID of jobs that were done by more than 3
employees for more than 100 days

->select JOB_ID,COUNT(EMPLOYEE_ID) from employees
  group by JOB_ID
  having COUNT(EMPLOYEE_ID)>3;


17. Display department ID, year, and Number of employees
joined.

->select DEPARTMENT_ID,count(EMPLOYEE_ID) from employees			// not complete
  where year(HIRE_DATE)
  group by DEPARTMENT_ID;
  

18. Display departments where any manager is managing more
than 5 employees.

->SELECT MANAGER_ID,COUNT(EMPLOYEE_ID) FROM employees
  GROUP BY MANAGER_ID;
 

19. Display first name and date of first salary of the employees.

->SELECT FIRST_NAME,DATE_ADD(HIRE_DATE,INTERVAL 30 DAY) FROM employees;


20. Display first name and experience of the employees.

->SELECT FIRST_NAME,FROM_DAYS(DATEDIFF(CURDATE(),HIRE_DATE)) as experi from employees; 								    //NOT OK


21. Display first name of employees who joined in 2001.

->SELECT FIRST_NAME FROM employees
  where year(HIRE_DATE) = 2001;


22. Display employees who joined in the current year.

->select EMPLOYEE_ID from employees
  where year(HIRE_DATE) = year(CURDATE());

23. Display the number of days between system date and 1st
January 2011

->select DATEDIFF(CURDATE(),'2011-01-01');


24. Display how many employees joined in each month of the
current year.

->select EMPLOYEE_ID from employees
  where month(HIRE_DATE) = month(CURDATE());

25. Display number of employees joined after 15th of the month.

->select EMPLOYEE_ID from employees
  where DATE(HIRE_DATE) > 15; 

26. Display details of departments in which the maximum salary
is more than 10000.

->SELECT salary,DEPARTMENT_ID from employees
  where salary >10000 AND (select DEPARTMENT_NAME from departments where departments.DEPARTMENT_ID= employees.DEPARTMENT_ID );   // NOT OK

27. Display details of departments managed by ‘Smith’.

->


28. Display jobs into which employees joined in the current year.

->


30. Display job title and average salary for employees who did a
job in the past.

->select j.JOB_TITLE,AVG(e.SALARY)
from employees e INNER JOIN job_history jh
ON e.EMPLOYEE_ID=jh.EMPLOYEE_ID
INNER JOIN jobs j
ON e.JOB_ID=j.JOB_ID
group by JOB_TITLE;


31. Display details of manager who manages more than 5
employees.

->select DISTINCT MANAGER_ID,count(EMPLOYEE_ID) from employees
group by MANAGER_ID
HAVING count(EMPLOYEE_ID)>5; 

32. Display the departments into which no employee joined in last
two years.

->

33. Display the details of departments in which the max salary is
greater than 10000 for employees who did a job in the past.

-> SELECT e.DEPARTMENT_ID, MAX(e.SALARY)
   from employees e INNER JOIN job_history jh
   ON e.EMPLOYEE_ID=jh.EMPLOYEE_ID
   group by e.DEPARTMENT_ID
   HAVING MAX(e.SALARY)>10000;


34. Display details of current job for employees who worked as IT
Programmers in the past.

Select e.* 
from employees e INNER JOIN job_history jh
ON e.EMPLOYEE_ID=jh.EMPLOYEE_ID
where jh.DEPARTMENT_ID=60;


35. Display third highest salary of all employees

select DISTINCT SALARY from employees
ORDER BY SALARY DESC
LIMIT 2,1;


36. Display details of the employees where commission
percentage is null and salary in the range 5000 to 10000 and
department is 30.

select * from employees
where COMMISSION_PCT=0 AND SALARY BETWEEN 5000 AND 10000;

---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

1. Write two different queries that would produce all orders taken
on October 3 rd or 4 th , 1990.

select * from ORDERS 
where onum =ANY (select onum from ORDERS where odate='1990-10-03' OR  odate='1990-10-04');

2. Write a query that selects all of the customers serviced by Peel
or Motika. (Hint:the snum field relates the two tables to one
another).

SELECT C.cname 
FROM CUSTOMERS C INNER JOIN SALESPEOPLE S
ON S.snum=C.snum
WHERE S.snum=1001 OR S.snum=1004;

3. Write a query that will produce all the customers whose names
begin with a letter from ‘A’ to ‘G’.

SELECT cname FROM CUSTOMERS
WHERE cname LIKE 'A%' AND'G%';


4. Write a query that selects all customers whose names begin
with the letter ‘C’.

SELECT cname FROM CUSTOMERS
WHERE cname LIKE 'C%';

5. Write a query that selects all orders except those with zeroes or
NULLs in the amt field.

SELECT * FROM ORDERS
WHERE amt>0;

6. Write a query that counts all orders for October 3.

SELECT COUNT(onum) FROM ORDERS
WHERE odate='1990-10-03';

7. Write a query that counts the number of different non-NULL city
values in the Customers table.

8. Write a query that selects each customer’s smallest order.

SELECT C.cnum
FROM CUSTOMERS C INNER JOIN ORDERS O
ON C.cnum = O.cnum
group by C.cnum,MIN(O.amt)
order by O.amt;


9. Write a query that  selects the first customer, in alphabetical
order, whose name begins with G.

select cname from CUSTOMERS 
order by cname
where cname LIKE 'G%' 
LIMIT 1;

10. Write a query that selects the highest rating in each city.

select city, MAX(rating) from CUSTOMERS
group by city ;

11. Write a query that counts the number of salespeople
registering orders for eachday. (If a salesperson has more than
one order on a given day, he or she should be
counted only once.).

SELECT odate,count(snum) FROM ORDERS
where snum  IN (select distinct snum from ORDERS) 
group by odate ;


12. Assume each salesperson has a 12% commission. Write a
query on the orders table that will produce the order number, the
salesperson number, and the amount of the salesperson’s
commission for that order.

select onum,snum,amt * 0.12 COMMISSION from ORDERS;


13. Write a query on the Customers table that will find the highest
rating in each city. Put the output in this form:
For the city (city), the highest rating is : (rating).

select city AS '(city)',MAX(rating) AS "the highest rasting is" from CUSTOMERS
GROUP BY city;

14. Write a query that lists customers in descending order of
rating. Output the rating field first, followed by the customer’s
name and number.

select rating,cname,cnum from CUSTOMERS
order by rating desc;


15. Write a query that totals the orders for each day and places
the results in descending order.

select odate, SUM(amt) from ORDERS
group by odate
order by SUM(amt) desc;


16. Write a query that uses a subquery to obtain all orders for the
customer named Cisneros. Assume you do not know his customer
number (cnum).

select onum from ORDERS
where cnum = (select cnum from CUSTOMERS where cname='Cisneros' );


17. Write a query that produces the names and ratings of all
customers who have above-average orders.

select cname, rating from CUSTOMERS


18. Write a query that selects the total amount in orders for each
salesperson for whom this total is greater than the amount of the
largest order in the table.

select snum,SUM(amt) from ORDERS
group by snum
having  SUM(amt) > ( select MAX(amt) from ORDERS );


19. Write a query that selects all customers whose ratings are
equal to or greater than ANY of Serres’.


20. Write a query using ANY or ALL that will find all salespeople
who have no customers located in their city.

SELECT s.snum 
from SALESPEOPLE s INNER JOIN CUSTOMERS C
ON s.snum = c.snum AND s.city != c.city;

select snum from SALESPEOPLE                                                              /NOT WORKING
WHERE city != ALL (select city from CUSTOMERS);


21. Write a query that selects all orders for amounts greater than
any for the customers in London.

SELECT onum,amt from ORDERS
WHERE cnum = ANY (SELECT cnum FROM CUSTOMERS where city = 'London');


22. Write the above query using MIN or MAX.



23. Count the number of salespeople currently listing orders in the
oreder table.

select count(distinct cnum) from ORDERS;


24. Largest order taken by each salesperson with order value
more than Rs.3000.

select snum from ORDERS
group by snum
having MAX(amt) > 3000;


25. Which day had the highest total amount ordered.

select odate, SUM(amt) from ORDERS
GROUP BY odate
order by SUM(amt) DESC
limit 1;


26. Count all orders for Oct 3.

select odate,count(onum) from ORDERS
group by odate
where odate = "1990-10-03";


27. Select each customer smallest order.

select cnum,MIN(amt) from ORDERS 
group by cnum 
having MIN(amt);


28. First customer in alphabetical order whose name begin with G.

SELECT cname from CUSTOMERS 
where cname LIKE 'G%'
order by cname
LIMIT 1;


29. Get the output like “For dd/mm/yy there are _____ orders”.

select odate, DATE_FORMAT(odate,GET_FORMAT(DATE,'EUR')) from ORDERS;


30. Extract all the orders of Motika.

select * from ORDERS
where snum=1004;


31. All orders that are greater than the average for Oct 4.

SELECT onum from ORDERS
where amt > (SELECT AVG(amt) from ORDERS group by odate where odate = 1990-10-04 );


32. Find avarage commission of salespeople in London.

SELECT city,AVG(comm) from SALESPEOPLE
where city='London';


33. Find all the order attribute to salespeople servicing customers
in London.

select * from SALESPEOPLE
where city= ANY (select city from CUSTOMERS where city='London');


34. Obtain all orders for the customer named Cisnerous.(Assume
you dont know his customer no. (cnum)).

select onum from ORDERS
WHERE cnum=  (SELECT cnum from CUSTOMERS where cname = 'Cisneros');


35. Find total amount in orders for each salesperson for whom this
total is greater than the amount of the largest order in the table.

select snum,SUM(amt) from ORDERS
group by snum
HAVING SUM(amt) > (select MAX(amt) from ORDERS );


