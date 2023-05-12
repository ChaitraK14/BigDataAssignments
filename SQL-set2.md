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
                calls UNION ALL SELECT 
                callee_id AS id, duration
            FROM
                calls) u
                INNER JOIN
            person p ON u.id = p.id
                INNER JOIN
            country c ON CAST(SUBSTRING(p.phone_number, 1, 3) AS UNSIGNED) = CAST(c.country_code AS UNSIGNED)
        GROUP BY c.name
        HAVING AVG(duration) > (SELECT 
                AVG(duration)
            FROM
                calls);

        

        SELECT employee_id, 
               SUM(employee_id) OVER(PARTITION BY team_id) AS team_size 
        FROM Employee
        ORDER BY employee_id;
    
Q56. Write an SQL query to report the device that is first logged in for each player.
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
        
Q57. Write an SQL query to find the customer_number for the customer who has placed the largest
number of orders.
The test cases are generated so that exactly one customer will have placed more orders than any
other customer.

A:


        SELECT 
            customer_number
        FROM
            Orders
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
                
Q58. Write an SQL query to report all the consecutive available seats in the cinema.
Return the result table ordered by seat_id in ascending order.

A:

        SELECT 
            c1.seat_id
        FROM
            cinema c1,
            cinema c2
        WHERE
            (c1.seat_id = c2.seat_id + 1
                OR c1.seat_id = c2.seat_id - 1)
                AND (c1.free = 1 AND c2.free = 1)
        GROUP BY c1.seat_id
        ORDER BY c1.seat_id;
        
Q59. Write an SQL query to report the names of all the salespersons who did not have any orders related to
the company with the name "RED".
Return the result table in any order.

A:

        SELECT 
            name
        FROM
            salesperson
        WHERE
            sales_id NOT IN (SELECT 
                    sales_id
                FROM
                    orders7 o
                        INNER JOIN
                    company c ON o.com_id = c.com_id
                WHERE
                    c.name = 'RED');
                    
Q60. Write an SQL query to report for every three line segments whether they can form a triangle.
Return the result table in any order.

A:

        SELECT 
            *,
            IF(x + y > z AND y + z > x AND x + z > y,
                'Yes',
                'No') AS triangle
        FROM
            triangle;
            
Q61. Write an SQL query to report the shortest distance between any two points from the Point table.
The query result format is in the following example.

A:




