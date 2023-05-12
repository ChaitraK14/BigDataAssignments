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
               count(employee_id) OVER(PARTITION BY team_id) AS team_size 
        FROM Employee
        ORDER BY employee_id;
    
Q55. Write an SQL query to find the countries where this company can invest.
Return the result table in any order.

A:

        SELECT 
            c.name
        FROM
            (SELECT 
                caller_id AS id, duration
            FROM
                calls2 UNION ALL SELECT 
                callee_id AS id, duration
            FROM
                calls2) u
                INNER JOIN
            person p ON u.id = p.id
                INNER JOIN
            country c ON CAST(SUBSTRING(p.phone_number, 1, 3) AS UNSIGNED) = CAST(c.country_code AS UNSIGNED)
        GROUP BY c.name
        HAVING AVG(duration) > (SELECT 
                AVG(duration)
            FROM
                calls2);

        

        SELECT employee_id, 
               SUM(employee_id) OVER(PARTITION BY team_id) AS team_size 
        FROM Employee
        ORDER BY employee_id;
    
Q55. Write an SQL query to report the device that is first logged in for each player.
Return the result table in any order.

A:

        SELECT player_id,
               device_id 
        FROM
            (SELECT player_id,
                    device_id,
                    RANK() OVER(PARTITION BY player_id ORDER BY event_date) AS r 
             FROM activity3)temp
        WHERE r=1;
        
Q56. Write an SQL query to find the customer_number for the customer who has placed the largest
number of orders.
The test cases are generated so that exactly one customer will have placed more orders than any
other customer.

A:


        SELECT 
            customer_number
        FROM
            orders6
        GROUP BY customer_number
        ORDER BY COUNT(order_number) DESC
        LIMIT 1;
        
Follow up: What if more than one customer has the largest number of orders, can you find all the
customer_number in this case?

        SELECT 
            customer_number
        FROM
            Orders
        GROUP BY customer_number
        HAVING COUNT(order_number) = (SELECT 
                MAX(order_count)
            FROM
                (SELECT 
                    COUNT(order_number) AS order_count
                FROM
                    Orders
                GROUP BY customer_number) temp);
                
 Q57. Write an SQL query to report all the consecutive available seats in the cinema.
Return the result table ordered by seat_id in ascending order.

A:


