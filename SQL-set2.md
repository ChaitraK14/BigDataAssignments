Q51. Write an SQL query to report the name, population, and area of the big countries.
Return the result table in any order.

A:

    SELECT name, population, area FROM World WHERE population>=3000000 OR area>=25000000;
    
Q52. Write an SQL query to report the names of the customer that are not referred by the customer with id
= 2.
Return the result table in any order.

A:

    SELECT name FROM Customer WHERE referee_id<>2;
    
Q53. Write an SQL query to report all customers who never order anything.
Return the result table in any order.

A:

    SELECT name FROM Customers WHERE id NOT IN 
      (SELECT id FROM Orders);
      
Q54. Write an SQL query to find the team size of each of the employees.
Return result table in any order.

A:

    SELECT employee_id, 
           SUM(employee_id) OVER(PARTITION BY team_id) AS team_size 
    FROM Employee
    ORDER BY employee_id;
    
Q55. 
