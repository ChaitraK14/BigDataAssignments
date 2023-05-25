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
			
Q80. Write a query to obtain the year-on-year growth rate for the total spend of each product for
each year.
Output the year (in ascending order) partitioned by product id, current year's spend, previous year's
spend and year-on-year growth rate (percentage rounded to 2 decimal places).

A:

		SELECT 
			*,
		    round(((curr_year_spend-prev_year_spend)/prev_year_spend)*100,2) AS yoy_rate 
		FROM
			(SELECT 
				YEAR(transaction_date) AS year,
			product_id,spend as curr_year_spend,
				LAG(spend) OVER(PARTITION BY product_id ORDER BY product_id, YEAR(transaction_date)) AS prev_year_spend
			FROM user_transactions2) temp;
			
Q81. Write a SQL query to find the number of prime and non-prime items that can be stored in the 500,000
square feet warehouse. Output the item type and number of items to be stocked.

A:

		WITH summary AS
		(SELECT 
			item_type,
		    SUM(square_footage) AS total_sqft,
		    COUNT(*) AS item_count 
		FROM inventory GROUP BY item_type),
		prime_occupied_area AS
		(SELECT 
			item_type,
			total_sqft,
			FLOOR(500000/total_sqft) AS prime_item_comb_area,
		    FLOOR(500000/total_sqft)*item_count AS prime_item_count 
		FROM summary
		WHERE item_type='prime_eligible')

		SELECT 
			item_type,
			CASE
				WHEN item_type='prime_eligible'
					THEN floor(500000/total_sqft)*item_count
			WHEN item_type='not_prime'
					THEN floor((500000-
						(SELECT floor(500000/total_sqft)*total_sqft 
				FROM prime_occupied_area))/total_sqft)*item_count
			END AS item_count
		FROM summary;

Q82. Write a query to obtain the active user retention in July 2022. Output the month (in numerical format 1, 2, 3) and the
number of monthly active users (MAUs).

A:

		SELECT 
		  EXTRACT(MONTH FROM curr_month.event_date) AS month, 
		  COUNT(DISTINCT curr_month.user_id) AS monthly_active_users 
		FROM user_actions AS curr_month
		WHERE EXISTS (
		  SELECT last_month.user_id 
		  FROM user_actions AS last_month
		  WHERE last_month.user_id = curr_month.user_id
		    AND EXTRACT(MONTH FROM last_month.event_date) =
		    EXTRACT(MONTH FROM curr_month.event_date - interval 1 month)
		)
		  AND EXTRACT(MONTH FROM curr_month.event_date) = 6
		  AND EXTRACT(YEAR FROM curr_month.event_date) = 2022
		GROUP BY EXTRACT(MONTH FROM curr_month.event_date);

Q83. Write a query to report the median of searches made by a user. Round the median to one decimal
point.

A:

		WITH cte AS 
		(SELECT 
			*,
		    SUM(num_users) OVER(ORDER BY searches) as running_sum , 
		    SUM(num_users) OVER () usersum
		FROM 
			search_frequency )

		SELECT 
		    ROUND(SUM(searches) * 1.0 / 2, 1) AS median
		FROM
		    cte
		WHERE
		    usersum / 2.0 BETWEEN (running_sum - num_users) AND running_sum;

Q84. Write a query to update the Facebook advertiser's status using the daily_pay table. Advertiser is a
two-column table containing the user id and their payment status based on the last payment and
daily_pay table has current information about their payment. Only advertisers who paid will show up in
this table.
Output the user id and current payment status sorted by the user id.

A:

		WITH payment_status AS(
		SELECT 
		    a.user_id,
		    a.status,
		    d.paid
		FROM advertiser a LEFT JOIN daily_pay d
		ON a.user_id=d.user_id
		UNION
		SELECT
		    d.user_id,
		    a.status,
		    d.paid
		FROM advertiser a RIGHT JOIN daily_pay d
		ON a.user_id=d.user_id)

		SELECT 
			user_id,
			CASE
			WHEN status IS NULL AND paid IS NOT NULL THEN 'NEW'
			WHEN paid IS NULL THEN 'CHURN'
			WHEN status='CHURN' AND paid IS NOT NULL THEN 'RESURRENT'
			WHEN status!='CHURN' and paid IS NOT NULL THEN 'EXISTING'
			END AS new_status
		FROM payment_status
		ORDER BY user_id;
		
Q85. Write a query that calculates the total time that the fleet of servers was running. The output should be
in units of full days.

A:

		WITH up_time AS(
		SELECT
			server_id,
		    status_time AS start_time,
		    LEAD(status_time) OVER(PARTITION BY server_id ORDER BY status_time) AS stop_time
		FROM server_utilization)

		SELECT sum(TIMESTAMPDIFF(DAY,start_time,stop_time)) AS total_uptime_days FROM up_time;
		
Q86. Sometimes, payment transactions are repeated by accident; it could be due to user error, API failure or
a retry error that causes a credit card to be charged twice.
Using the transactions table, identify any payments made at the same merchant with the same credit
card for the same amount within 10 minutes of each other. Count such repeated payments.

A:

		SELECT
			COUNT(merchant_id) AS payment_count 
		FROM
		(SELECT 
			*,
			LEAD(transaction_timestamp) 
				OVER(PARTITION BY merchant_id,credit_card_id,amount 
			ORDER BY transaction_timestamp) AS lead_time
		FROM transactions3) temp
		WHERE TIMESTAMPDIFF(MINUTE,transaction_timestamp,lead_time)<10;
		
Q87. Write a query to find the bad experience rate in the first 14 days for new users who signed up in June
2022. Output the percentage of bad experience rounded to 2 decimal places.

A:

		WITH total_orders AS
		(SELECT 
		    c.customer_id,
		    o.order_id,
		    t.trip_id,
		    o.status,
		    c.signup_timestamp,
		    t.estimated_delivery_timestamp,
		    t.actual_delivery_timestamp
		FROM
		    Orders8 o
			INNER JOIN
		    customers2 c ON o.customer_id = c.customer_id
			AND TIMESTAMPDIFF(DAY,
			c.signup_timestamp,
			o.order_timestamp) <= 14
			AND MONTH(signup_timestamp) = 6
			INNER JOIN
		    trips t ON o.trip_id = t.trip_id)

		SELECT 
		    ROUND(100 * COUNT(order_id) / (SELECT 
				    COUNT(order_id)
				FROM
				    total_orders),
			    2) AS bad_experience_pct
		FROM
		    total_orders
		WHERE
		    status <> 'completed successfully'
			OR actual_delivery_timestamp IS NULL
			OR actual_delivery_timestamp > estimated_delivery_timestamp;
			
Q88. Write an SQL query to find the total score for each gender on each day.
Return the result table ordered by gender and day in ascending order.

A:

		SELECT 
			gender,
		    day,
		    sum(score_points) over(partition by gender order by gender,day) as total 
		FROM Scores;
		
Q89. Write an SQL query to find the countries where this company can invest.
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
		    
Q90. Write an SQL query to report the median of all the numbers in the database after decompressing the
Numbers table. Round the median to one decimal point.

A:

Q91. Write an SQL query to report the comparison result (higher/lower/same) of the average salary of
employees in a department to the company's average salary.
Return the result table in any order.

A:

		WITH cte1 AS
		(SELECT 
			DATE_FORMAT(pay_date, '%Y- %m') AS pay_month, 
		    AVG(amount) AS avg_salary 
		FROM Salary s INNER JOIN Employee7 e 
		ON s.employee_id=e.employee_id
		GROUP BY pay_month),
		cte2 AS
		(SELECT 
			DATE_FORMAT(pay_date, '%Y- %m') AS pay_month,
			department_id,AVG(amount) AS avg_dept_salary
		FROM Salary s INNER JOIN Employee7 e 
		ON s.employee_id=e.employee_id
		GROUP BY pay_month,department_id)

		SELECT 
			cte1.pay_month,department_id,
			CASE 
				WHEN avg_dept_salary>avg_salary THEN 'higher'
				WHEN avg_dept_salary<avg_salary THEN 'lower'
				ELSE 'same'
			END AS comparison
		FROM cte1 INNER JOIN cte2
		ON cte1.pay_month=cte2.pay_month
		ORDER BY 2,1;
		
Q92. Write an SQL query to report for each install date, the number of players that installed the game on
that day, and the day one retention.
Return the result table in any order.

A:

		WITH cte1 AS
		(SELECT 
		    player_id, MIN(event_date) AS installed_on
		FROM
		    Activity4
		GROUP BY player_id)

		SELECT 
		    installed_on AS installed_dt,
		    COUNT(installed_on) AS installs,
		    ROUND(COUNT(event_date) / COUNT(installed_on),
			    2) AS Day1_retention
		FROM
		    (SELECT 
			c.player_id, c.installed_on, a.event_date
		    FROM
			cte1 c
		    LEFT JOIN Activity4 a ON DATE_ADD(installed_on, INTERVAL 1 DAY) = a.event_date
			AND c.player_id = a.player_id) temp
		GROUP BY installed_on;
		
Q93. Write an SQL query to find the winner in each group.
Return the result table in any order.

A:

	WITH winner_by_match AS
	(SELECT group_id,
		CASE 
			WHEN first_score>second_score THEN first_score
			WHEN first_score<second_score THEN second_score
			ELSE least(first_score,second_score) 
		END AS highest_score,
		CASE 
			WHEN first_score>second_score THEN first_player
			WHEN first_score<second_score THEN second_player
			ELSE least(first_player,second_player) 
		END AS winner
	FROM Players p INNER JOIN Matches m
	ON p.player_id=m.first_player)

	SELECT group_id,winner as player_id 
	FROM
		(SELECT *,RANK()OVER(PARTITION BY group_id ORDER BY highest_score DESC) AS r 
		FROM winner_by_match) tmp 
	WHERE r=1;

Q94. Write an SQL query to report the students (student_id, student_name) being quiet in all exams. Do not
return the student who has never taken any exam.
Return the result table ordered by student_id.

A:

		WITH cte AS
		(SELECT 
			CASE
				WHEN e.score=MAX(score) OVER(PARTITION BY exam_id) OR 
					 e.score=MIN(score) OVER(PARTITION BY exam_id) THEN s.student_id 
				END AS max_min_student_id
		FROM student2 s INNER JOIN exam e
		ON s.student_id=e.student_id)

		SELECT DISTINCT
		    s.student_id, s.student_name
		FROM
		    student2 s
			INNER JOIN
		    exam e ON s.student_id = e.student_id
		WHERE
		    s.student_id NOT IN (SELECT DISTINCT
			    IFNULL(max_min_student_id, 0)
			FROM
			    cte);
			    
Q95. same as Q94

Q96. Write a query to output the user id, song id, and cumulative count of song plays as of 4 August 2022
sorted in descending order.

A:

		WITH cte AS
		(SELECT 
		    user_id, song_id, song_plays
		FROM
		    songs_history 
		UNION SELECT 
		    user_id, song_id, COUNT(*) AS song_plays
		FROM
		    songs_weekly
		WHERE
		    DATE(listen_time) <= '2022-08-04'
		GROUP BY user_id , song_id)

		SELECT 
		    user_id, song_id, SUM(song_plays) AS song_plays
		FROM
		    cte
		GROUP BY user_id , song_id
		ORDER BY song_plays DESC;
		    
Q97. Write a query to find the confirmation rate of users who confirmed their signups with text messages.
Round the result to 2 decimal places.

A:

		SELECT 
		    ROUND(SUM(CASE
				WHEN signup_action = 'Confirmed' THEN 1
				ELSE 0
			    END) / COUNT(DISTINCT user_id),
			    2) AS confirm_rate
		FROM
		    emails e
			LEFT JOIN
		    texts t ON e.email_id = t.email_id;
		    
Q98. Calculate the 3-day
rolling average of tweets published by each user for each date that a tweet was posted. Output the
user id, tweet date, and rolling averages rounded to 2 decimal places.

A:

		SELECT 
			user_id,
		    tweet_date,
			ROUND(AVG(COUNT(*)) 
				OVER(PARTITION BY user_id ORDER BY tweet_date ROWS BETWEEN 2 PRECEDING AND CURRENT ROW),2) 
			AS rolling_avg_3days
		FROM tweets 
		GROUP BY user_id,tweet_date;
		
Q99. Write a query to obtain a breakdown of the time spent
sending vs. opening snaps (as a percentage of total time spent on these activities) for each age
group.

A:

		SELECT 
		    age_bucket,
		    ROUND(sending_time * 100.0 / (opening_time + sending_time),
			    2) AS send_perc,
		    ROUND(opening_time * 100.0 / (opening_time + sending_time),
			    2) AS open_perc
		FROM
		    (SELECT 
			age_bucket,
			    SUM(CASE
				WHEN activity_type = 'open' THEN time_spent
			    END) AS opening_time,
			    SUM(CASE
				WHEN activity_type = 'send' THEN time_spent
			    END) AS sending_time
		    FROM
			activities a
		    INNER JOIN age_breakdown b ON a.user_id = b.user_id
		    WHERE
			activity_type IN ('send' , 'open')
		    GROUP BY age_bucket) temp
		ORDER BY age_bucket;
		
Q100. Write a query to return the IDs of these LinkedIn power creators in ascending order.

A:

		SELECT 
		    profile_id
		FROM
		    (SELECT 
			p.profile_id,
			    p.name,
			    p.followers AS profile_followers,
			    MAX(c.followers) AS company_followers
		    FROM
			personal_profiles p
		    INNER JOIN employee_company e ON p.profile_id = e.personal_profile_id
		    INNER JOIN company_pages c ON e.company_id = c.company_id
		    GROUP BY p.profile_id , p.name , p.followers) temp
		WHERE
		    profile_followers > company_followers
		ORDER BY profile_id;



















