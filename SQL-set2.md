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

        SELECT 
            MIN(ABS(p1.x - p2.x)) AS shortest
        FROM
            point p1,
            point p2
        WHERE
            p1.x <> p2.x;
            
 Follow up: How could you optimise your query if the Point table is ordered in ascending order?
 
        SELECT min(distance) AS shortest 
        FROM   
	        (SELECT abs(x-LEAD(x) OVER(ORDER BY x)) AS distance 
	        FROM point)tmp;
            
Q62. Write a SQL query for a report that provides the pairs (actor_id, director_id) where the actor has
cooperated with the director at least three times.
Return the result table in any order.

A:

        SELECT 
            actor_id, director_id
        FROM
            ActorDirector
        GROUP BY actor_id , director_id
        HAVING COUNT(*)>=3;
        
Q63. Write an SQL query that reports the product_name, year, and price for each sale_id in the Sales table.
Return the resulting table in any order.

A:

        SELECT 
            product_name, year, price
        FROM
            Sales s
                INNER JOIN
            Product p ON s.product_id = p.product_id;
            
Q64. Write an SQL query that reports the average experience years of all the employees for each project,
rounded to 2 digits.
Return the result table in any order.

A:

        SELECT 
            project_id, ROUND(AVG(experience_years), 2) AS average_years
        FROM
            Project p
                INNER JOIN
            Employee e ON p.employee_id = e.employee_id
        GROUP BY project_id;
        
Q65. Write an SQL query that reports the best seller by total sales price, If there is a tie, report them all.
Return the result table in any order.

A:

	SELECT 
	    seller_id
	FROM
	    sales4
	GROUP BY seller_id
	HAVING SUM(price) = (SELECT 
		SUM(price)
	    FROM
		sales4
	    GROUP BY seller_id
	    ORDER BY SUM(price) DESC
	    LIMIT 1);
	    
Q66. Write an SQL query that reports the buyers who have bought S8 but not iPhone. Note that S8 and
iPhone are products present in the Product table.
Return the result table in any order.

A:

	SELECT 
	    buyer_id
	FROM
	    Sales
	WHERE
	    buyer_id IN (SELECT 
		    buyer_id
		FROM
		    P ,roduct p
			INNER JOIN
		    sales6 s ON p.product_id = s.product_id
		WHERE
		    product_name = 'S8')
		AND buyer_id NOT IN (SELECT 
		    buyer_id
		FROM
		    product7 p
			INNER JOIN
		    sales6 s ON p.product_id = s.product_id
		WHERE
		    product_name = 'iPhone');
		    
Q67. Write an SQL query to compute the moving average of how much the customer paid in a seven days
window (i.e., current day + 6 days before). average_amount should be rounded to two decimal places.
Return result table ordered by visited_on in ascending order.

A:

		SELECT 
			visited_on, amount_sum AS amount, average_amount
		FROM
			(SELECT 
				visited_on,
				COUNT(SUM(amount)) OVER(ORDER BY visited_on ROWS BETWEEN 6 PRECEDING AND CURRENT ROW) AS days_count,
				SUM(SUM(amount)) OVER(ORDER BY visited_on ROWS BETWEEN 6 PRECEDING AND CURRENT ROW) AS amount_sum,
				avg(sum(amount)) OVER(ORDER BY visited_on ROWS BETWEEN 6 PRECEDING AND CURRENT ROW) AS average_amount
			FROM Customer2 
			GROUP BY visited_on) temp
		WHERE days_count=7;
		
Q68. Write an SQL query to find the total score for each gender on each day.
Return the result table ordered by gender and day in ascending order.

A:

		SELECT 
			gender,day,SUM(score_points) OVER(PARTITION BY gender ORDER BY gender,day) AS total 
		FROM scores;
		
Q69. Write an SQL query to find the start and end number of continuous ranges in the table Logs.
Return the result table ordered by start_id.

A:

		SELECT 
			MIN(d.log_id) AS start_id, MAX(d.log_id) AS end_id 
		FROM
			(SELECT r.log_id,(r.log_id-rn) AS diff 
			FROM
				(SELECT log_id,ROW_NUMBER() OVER() AS rn 
			FROM logs) r)d
		GROUP BY diff;
		
Q70. Write an SQL query to find the number of times each student attended each exam.
Return the result table ordered by student_id and subject_name.

A:

		SELECT 
		    s.student_id,
		    s.student_name,
		    s.subject_name,
		    IFNULL(attended_exams, 0)
		FROM
		    (SELECT 
			*
		    FROM
			Students2
		    CROSS JOIN Subjects) s
			LEFT JOIN
		    (SELECT 
			*, COUNT(*) AS attended_exams
		    FROM
			Examinations
		    GROUP BY student_id , subject_name) e ON s.student_id = e.student_id
			AND s.subject_name = e.subject_name
		ORDER BY s.student_id , s.subject_name;
		
Q71. Write an SQL query to find employee_id of all employees that directly or indirectly report their work to
the head of the company.
The indirect relation between managers will not exceed three managers as the company is small.
Return the result table in any order.

A:

		SELECT 
		    employee_id
		FROM
		    Employees2
		WHERE
		    manager_id IN (SELECT 
			    employee_id
			FROM
			    Employees2
			WHERE
			    manager_id IN (SELECT 
				    employee_id
				FROM
				    Employees2
				WHERE
				    manager_id = 1))
			AND employee_id <> 1;
			
Q72. Write an SQL query to find for each month and country, the number of transactions and their total
amount, the number of approved transactions and their total amount.
Return the result table in any order.

A:

		SELECT 
		    date_format(trans_date,"%Y-%m") AS month,
		    country,
		    COUNT(*) AS trans_count,
		    COUNT(state = 'approved') AS approved_count,
		    SUM(amount) AS trans_total_amount,
		    SUM(CASE
			WHEN state = 'approved' THEN amount
		    END) AS approved_total_amount
		FROM
		    Transactions
		GROUP BY month, country;
		
Q73. Write an SQL query to find the average daily percentage of posts that got removed after being
reported as spam, rounded to 2 decimal places.

A:

		SELECT 
		    ROUND(AVG(daily_percent), 2) AS average_daily_percent
		FROM
		    (SELECT 
			COUNT(DISTINCT r.post_id) / COUNT(DISTINCT a.post_id) * 100 AS daily_percent
		    FROM
			Actions a
		    LEFT JOIN Removals r ON a.post_id = r.post_id
		    WHERE
			extra = 'spam'
		    GROUP BY action_date) temp;
		    
Q74. Write an SQL query to report the fraction of players that logged in again on the day after the day they
first logged in, rounded to 2 decimal places. In other words, you need to count the number of players
that logged in for at least two consecutive days starting from their first login date, then divide that
number by the total number of players.

A:

		WITH login AS
		(SELECT 
		    player_id, MIN(event_date) AS first_login
		FROM
		    Activity
		GROUP BY player_id)

		SELECT 
		    ROUND(COUNT(DISTINCT a.player_id) / (SELECT 
				    COUNT(DISTINCT player_id)
				FROM
				    Activity),
			    2)
		FROM
		    Activity a
			INNER JOIN
		    login l ON a.player_id = l.player_id
			AND DATEDIFF(event_date, first_login) = 1;
			
Q75. Same as Q74

Q76. Write an SQL query to find the salaries of the employees after applying taxes. Round the salary to the
nearest integer.
The tax rate is calculated for each company based on the following criteria:
● 0% If the max salary of any employee in the company is less than $1000.
● 24% If the max salary of any employee in the company is in the range [1000, 10000] inclusive.
● 49% If the max salary of any employee in the company is greater than $10000.
Return the result table in any order.

A:

		SELECT 	
			company_id,employee_id,employee_name,
			CASE
				WHEN MAX(salary) OVER(PARTITION BY company_id)<1000 THEN ROUND(salary,0)
			WHEN MAX(salary) OVER(PARTITION BY company_id)>10000 THEN ROUND(salary-(0.49*salary),0)
			ELSE ROUND(salary-(0.24*salary),0)
			END AS salary
		FROM Salaries;
		
Q77. Write an SQL query to evaluate the boolean expressions in Expressions table.
Return the result table in any order.

A:

		SELECT 
		    left_operand,
		    operator,
		    right_operand,
		    CASE
			WHEN operator = '<' THEN IF(v1.value < v2.value, 'true', 'false')
			WHEN operator = '>' THEN IF(v1.value > v2.value, 'true', 'false')
			ELSE IF(v1.value = v2.value, 'true', 'false')
		    END AS value
		FROM
		    Expressions e
			INNER JOIN
		    Variables v1 ON e.left_operand = v1.name
			INNER JOIN
		    Variables v2 ON e.right_operand = v2.name;
		    
Q78. Write an SQL query to find the countries where this company can invest.
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
		    
Q79. Write a query that prints a list of employee names (i.e.: the name attribute) from the Employee table in
alphabetical order.

A:

			SELECT 
			    name
			FROM
			    Employee
			ORDER BY name;
			
Q80. 







