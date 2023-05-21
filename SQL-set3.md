Q101. Write an SQL query to show the second most recent activity of each user.
If the user only has one activity, return that one. A user cannot perform more than one activity at the
same time.
Return the result table in any order.

A:

          SELECT 
            username,
              activity,
              startDate,
              endDate 
          FROM
            (SELECT 
              *,
              COUNT(*) OVER(PARTITION BY username) AS count,
              RANK() OVER(PARTITION BY username ORDER BY startDate) AS r 
            FROM 
              useractivity) temp
            WHERE 	
              r=2 OR count<2;
              
Q102. same as Q101

Q103. Query the Name of any student in STUDENTS who scored higher than 75 Marks. Order your output by
the last three characters of each name. If two or more students both have names ending in the same
last three characters (i.e.: Bobby, Robby, etc.), secondary sort them by ascending ID.

A:

            SELECT 
                Name
            FROM
                students3
            WHERE
                Marks > 75
            ORDER BY RIGHT(Name, 3) , Id;
            
Q104. Write a query that prints a list of employee names (i.e.: the name attribute) for employees in
Employee having a salary greater than $2000 per month who have been employees for less than 10
months. Sort your result by ascending employee_id.

A:

            SELECT 
                name
            FROM
                Employee
            WHERE
                salary > 2000 AND months < 10
            ORDER BY employee_id;
            
Q105. Write a query identifying the type of each record in the TRIANGLES table using its three side lengths.
Output one of the following statements for each record in the table:
● Equilateral: It's a triangle with sides of equal length.
● Isosceles: It's a triangle with sides of equal length.
● Scalene: It's a triangle with sides of differing lengths.
● Not A Triangle: The given values of A, B, and C don't form a triangle.

A:

            SELECT 
                CASE
                    WHEN A = B AND B = C THEN 'Equilateral'
                    WHEN A = B OR B = C OR A = C THEN 'Isosceles'
                    WHEN A + B < C OR A + C < B OR B + C < A THEN 'Not A Triangle'
                    WHEN A <> B AND B<> C THEN 'Scalene'
                END AS Type_of_Triangle
            FROM
                Triangles;
                
Q106. Samantha was tasked with calculating the average monthly salaries for all employees in the
EMPLOYEES table, but did not realise her keyboard's 0 key was broken until after completing the
calculation. She wants your help finding the difference between her miscalculation (using salaries
with any zeros removed), and the actual average salary.
Write a query calculating the amount of error (i.e.: actual - miscalculated average monthly salaries),
and round it up to the next integer.

A:  

            SELECT 
                CEILING(AVG(Salary) - AVG(CAST(REPLACE(CAST(Salary AS NCHAR), '0', '') AS SIGNED)))
            FROM
                Employees3;
                
Q107. We define an employee's total earnings to be their monthly salary * months worked, and the
maximum total earnings to be the maximum total earnings for any employee in the Employee table.
Write a query to find the maximum total earnings for all employees as well as the total number of
employees who have maximum total earnings. Then print these values as 2 space-separated
integers.

A:

            SELECT 
                months * salary as earning, COUNT(*) as no_of_employees
            FROM
                Employee8
            GROUP BY earning
            ORDER BY earning DESC
            LIMIT 1;
            
Q108. Query an alphabetically ordered list of all names in OCCUPATIONS, immediately followed by
the first letter of each profession as a parenthetical (i.e.: enclosed in parentheses). For
example: AnActorName(A), ADoctorName(D), AProfessorName(P), and ASingerName(S).
Query the number of occurrences of each occupation in OCCUPATIONS. Sort the occurrences in
ascending order, and output them in the following format:
Level - Medium
There are a total of [occupation_count] [occupation]s.
2. where [occupation_count] is the number of occurrences of an occupation in OCCUPATIONS and
[occupation] is the lowercase occupation name. If more than one Occupation has the same
[occupation_count], they should be ordered alphabetically.

A:

            SELECT 
                CONCAT(Name, '(', LEFT(Occupation, 1), ')') AS Name
            FROM
                Occupations
            ORDER BY Name;

            SELECT 
                CONCAT('There are a total of',
                        ' ',
                        COUNT(*),
                        ' ',
                        Occupation,
                        's') AS Output
            FROM
                Occupations
            GROUP BY Occupation
            ORDER BY COUNT(*) , Occupation;
            
Q109. Pivot the Occupation column in OCCUPATIONS so that each Name is sorted alphabetically and
displayed underneath its corresponding Occupation. The output column headers should be Doctor,
Professor, Singer, and Actor, respectively.
 
 A:
 
            WITH cte AS
            (SELECT 
              CASE WHEN Occupation='Doctor' THEN NAME END AS Doctor,
                CASE WHEN Occupation='Professor' THEN NAME END ASProfessor,
                CASE WHEN Occupation='Singer' THEN NAME END AS Singer,
                CASE WHEN Occupation='Actor' THEN NAME END AS Actor,
                ROW_NUMBER() OVER(PARTITION BY Occupation ORDER BY Name) AS rn 
            FROM Occupations)

            SELECT 
                MAX(Doctor) AS Doctor,
                MAX(Professor) AS Professor,
                MAX(Singer) AS Singer,
                MAX(Actor) AS Actor
            FROM
                cte
            GROUP BY rn
            ORDER BY rn;
            
Q110. Write a query to find the node type of Binary Tree ordered by the value of the node. Output one of the
following for each node:
● Root: If node is root node.
● Leaf: If node is leaf node.
● Inner: If node is neither root nor leaf node.

A:

                    SELECT 
                        N,
                        CASE
                            WHEN P IS NULL THEN 'Root'
                            WHEN
                                N IN (SELECT 
                                        P
                                    FROM
                                        BST)
                            THEN
                                'Inner'
                            ELSE 'leaf'
                        END AS Type_of_BinaryTree
                    FROM
                        BST
                    ORDER BY N;
                    
Q111. Given the table schemas below, write a query to print the company_code, founder name, total number
of lead managers, total number of senior managers, total number of managers, and total number of
employees. Order your output by ascending company_code.

A:

                    SELECT 
                        c.company_code,
                        founder,
                        COUNT(DISTINCT l.lead_manager_code) No_of_LMs,
                        COUNT(DISTINCT s.senior_manager_code) No_of_SMs,
                        COUNT(DISTINCT m.manager_code) No_of_Managers,
                        COUNT(DISTINCT e.employee_code) No_of_Employees
                    FROM
                        Company c
                            INNER JOIN
                        Lead_Manager l ON c.company_code = l.company_code
                            INNER JOIN
                        Senior_Manager s ON l.lead_manager_code = s.lead_manager_code
                            INNER JOIN
                        Manager m ON s.senior_manager_code = m.senior_manager_code
                            INNER JOIN
                        Employee e ON m.manager_code = e.manager_code
                    GROUP BY c.company_code , c.founder
                    ORDER BY c.company_code;
                    
Q112. Write a query to print all prime numbers less than or equal to 1000. Print your result on a single line,
and use the ampersand () character as your separator (instead of a space).

A:

Q113. P(R) represents a pattern drawn by Julia in R rows. The following pattern represents P(5):
*
* *
* * *
* * * *
* * * * *
Write a query to print the pattern P(20).

A:

Q114. P(R) represents a pattern drawn by Julia in R rows. The following pattern represents P(5):
* * * * *
* * * *
* * *
* *
*
Write a query to print the pattern P(20).

A:

Q115. Query the Name of any student in STUDENTS who scored higher than 75 Marks. Order your output by
the last three characters of each name. If two or more students both have names ending in the same
last three characters (i.e.: Bobby, Robby, etc.), secondary sort them by ascending ID.

A:

                    SELECT 
                        Name
                    FROM
                        Students
                    WHERE
                        Marks > 75
                    ORDER BY RIGHT(Name, 3) , Id;

Q116. Write a query that prints a list of employee names (i.e.: the name attribute) from the Employee table
in alphabetical order.

A:

                    SELECT 
                        name
                    FROM
                        Employee
                    ORDER BY name;
                    
Q117. Write a query that prints a list of employee names (i.e.: the name attribute) for employees in
Employee having a salary greater than $2000 per month who have been employees for less than 10
months. Sort your result by ascending employee_id.

A:

                    SELECT 
                        name
                    FROM
                        Employee8
                    WHERE
                        salary > 2000 AND months < 10
                    ORDER BY employee_id;
                    
Q118. Write a query identifying the type of each record in the TRIANGLES table using its three side
lengths. Output one of the following statements for each record in the table:
● Equilateral: It's a triangle with sides of equal length.
● Isosceles: It's a triangle with sides of equal length.
● Scalene: It's a triangle with sides of differing lengths.
● Not A Triangle: The given values of A, B, and C don't form a triangle.

A:

            SELECT 
                CASE
                    WHEN A = B AND B = C THEN 'Equilateral'
                    WHEN A = B OR B = C OR A = C THEN 'Isosceles'
                    WHEN A + B < C OR A + C < B OR B + C < A THEN 'Not A Triangle'
                    WHEN A <> B AND B<> C THEN 'Scalene'
                END AS Type_of_Triangle
            FROM
                Triangles;
                
Q119. Assume you are given the table below containing information on user transactions for
particular products. Write a query to obtain the year-on-year growth rate for the total spend of each
product for each year.
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
                    
Q120. Amazon wants to maximise the number of items it can stock in a 500,000 square feet
warehouse. It wants to stock as many prime items as possible, and afterwards use the remaining
square footage to stock the most number of non-prime items.
Write a SQL query to find the number of prime and non-prime items that can be stored in the 500,000
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
          
Q121. Assume you have the table below containing information on Facebook user actions. Write a
query to obtain the active user retention in July 2022. Output the month (in numerical format 1, 2, 3)
and the number of monthly active users (MAUs).

A:

Q122. Google's marketing team is making a Superbowl commercial and needs a simple statistic to
put on their TV ad: the median number of searches a person made last year.
However, at Google scale, querying the 2 trillion searches is too costly. Luckily, you have access to the
summary table which tells you the number of searches made last year and how many Google users
fall into that bucket.
Write a query to report the median of searches made by a user. Round the median to one decimal
point.

A:

Q123. Write a query to update the Facebook advertiser's status using the daily_pay table. Advertiser is
a two-column table containing the user id and their payment status based on the last payment and
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
          
Q124. Amazon Web Services (AWS) is powered by fleets of servers. Senior management has
requested data-driven solutions to optimise server usage.
Write a query that calculates the total time that the fleet of servers was running. The output should be
in units of full days.

A:

	WITH up_time AS(
	SELECT
		server_id,
	    status_time AS start_time,
	    LEAD(status_time) OVER(PARTITION BY server_id ORDER BY status_time) AS stop_time
	FROM server_utilization)

	SELECT sum(TIMESTAMPDIFF(DAY,start_time,stop_time)) AS total_uptime_days FROM up_time;
          
Q125. Sometimes, payment transactions are repeated by accident; it could be due to user error, API
failure or a retry error that causes a credit card to be charged twice.
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
         
Q126. DoorDash's Growth Team is trying to make sure new users (those who are making orders in
their first 14 days) have a great experience on all their orders in their 2 weeks on the platform.
Unfortunately, many deliveries are being messed up because:
● the orders are being completed incorrectly (missing items, wrong order, etc.)
● the orders aren't being received (wrong address, wrong drop off spot)
● the orders are being delivered late (the actual delivery time is 30 minutes later than when the
order was placed). Note that the estimated_delivery_timestamp is automatically set to 30
minutes after the order_timestamp.
Hint- Use Where Clause and joins
Write a query to find the bad experience rate in the first 14 days for new users who signed up in June
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
                    
Q127. A competition is held between the female team and the male team.
Each row of this table indicates that a player_name and with gender has scored score_point in
someday.
Gender is 'F' if the player is in the female team and 'M' if the player is in the male team.
Write an SQL query to find the total score for each gender on each day.
Return the result table ordered by gender and day in ascending order.

A:

	SELECT 
		gender,
	    day,
	    sum(score_points) over(partition by gender order by gender,day) as total 
	FROM Scores;
          
Q128. A telecommunications company wants to invest in new countries. The company intends to invest in
the countries where the average call duration of the calls in this country is strictly greater than the
global average call duration.
Write an SQL query to find the countries where this company can invest.
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
              
Q129. The median is the value separating the higher half from the lower half of a data sample.
Write an SQL query to report the median of all the numbers in the database after decompressing the
Numbers table. Round the median to one decimal point.

A:

Q130. Write an SQL query to report the comparison result (higher/lower/same) of the average salary of
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
          
Q131. The install date of a player is the first login day of that player.
We define day one retention of some date x to be the number of players whose install date is x and
they logged back in on the day right after x, divided by the number of players whose install date is x,
rounded to 2 decimal places.
Write an SQL query to report for each install date, the number of players that installed the game on
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
          
Q132. The winner in each group is the player who scored the maximum total points within the group. In the
case of a tie, the lowest player_id wins.
Write an SQL query to find the winner in each group.
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
                    
Q133. A quiet student is the one who took at least one exam and did not score the high or the low score.
Write an SQL query to report the students (student_id, student_name) being quiet in all exams. Do not
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
                        
Q134. Same as Q133
 
Q135. Write an SQL query to show the second most recent activity of each user.
If the user only has one activity, return that one. A user cannot perform more than one activity at the
same time.
Return the result table in any order.

A:

          SELECT 
            username,
              activity,
              startDate,
              endDate 
          FROM
            (SELECT 
              *,
              COUNT(*) OVER(PARTITION BY username) AS count,
              RANK() OVER(PARTITION BY username ORDER BY startDate) AS r 
            FROM 
              useractivity) temp
            WHERE 	
              r=2 OR count<2;
              
Q136. Same as 135

Q137. Samantha was tasked with calculating the average monthly salaries for all employees in the
EMPLOYEES table, but did not realise her keyboard's 0 key was broken until after completing the
calculation. She wants your help finding the difference between her miscalculation (using salaries
with any zeros removed), and the actual average salary.
Write a query calculating the amount of error (i.e.: actual - miscalculated average monthly salaries),
and round it up to the next integer.

A:

            SELECT 
                CEILING(AVG(Salary) - AVG(CAST(REPLACE(CAST(Salary AS NCHAR), '0', '') AS SIGNED)))
            FROM
                Employees3;
                
Q138. We define an employee's total earnings to be their monthly salary * months worked, and the
maximum total earnings to be the maximum total earnings for any employee in the Employee table.
Write a query to find the maximum total earnings for all employees as well as the total number of
employees who have maximum total earnings. Then print these values as 2 space-separated
integers.

A:


            SELECT 
                months * salary as earning, COUNT(*) as no_of_employees
            FROM
                Employee8
            GROUP BY earning
            ORDER BY earning DESC
            LIMIT 1;
            
 Q139. Generate the following two result sets:
1. Query an alphabetically ordered list of all names in OCCUPATIONS, immediately followed by
the first letter of each profession as a parenthetical (i.e.: enclosed in parentheses). For
example: AnActorName(A), ADoctorName(D), AProfessorName(P), and ASingerName(S).
Query the number of occurrences of each occupation in OCCUPATIONS. Sort the occurrences in
ascending order, and output them in the following format:
Level - Medium
There are a total of [occupation_count] [occupation]s.
2. where [occupation_count] is the number of occurrences of an occupation in OCCUPATIONS and
[occupation] is the lowercase occupation name. If more than one Occupation has the same
[occupation_count], they should be ordered alphabetically.

A:

            SELECT 
                CONCAT(Name, '(', LEFT(Occupation, 1), ')') AS Name
            FROM
                Occupations
            ORDER BY Name;

            SELECT 
                CONCAT('There are a total of',
                        ' ',
                        COUNT(*),
                        ' ',
                        Occupation,
                        's') AS Output
            FROM
                Occupations
            GROUP BY Occupation
            ORDER BY COUNT(*) , Occupation;
            
Q140. Pivot the Occupation column in OCCUPATIONS so that each Name is sorted alphabetically and
displayed underneath its corresponding Occupation. The output column headers should be Doctor,
Professor, Singer, and Actor, respectively.

A:

            WITH cte AS
            (SELECT 
              CASE WHEN Occupation='Doctor' THEN NAME END AS Doctor,
                CASE WHEN Occupation='Professor' THEN NAME END ASProfessor,
                CASE WHEN Occupation='Singer' THEN NAME END AS Singer,
                CASE WHEN Occupation='Actor' THEN NAME END AS Actor,
                ROW_NUMBER() OVER(PARTITION BY Occupation ORDER BY Name) AS rn 
            FROM Occupations)

            SELECT 
                MAX(Doctor) AS Doctor,
                MAX(Professor) AS Professor,
                MAX(Singer) AS Singer,
                MAX(Actor) AS Actor
            FROM
                cte
            GROUP BY rn
            ORDER BY rn;
            
Q141. Write a query to find the node type of Binary Tree ordered by the value of the node. Output one of the
following for each node:
● Root: If node is root node.
● Leaf: If node is leaf node.
● Inner: If node is neither root nor leaf node.

A:

                    SELECT 
                        N,
                        CASE
                            WHEN P IS NULL THEN 'Root'
                            WHEN
                                N IN (SELECT 
                                        P
                                    FROM
                                        BST)
                            THEN
                                'Inner'
                            ELSE 'leaf'
                        END AS Type_of_BinaryTree
                    FROM
                        BST
                    ORDER BY N;
                    
Q142. Given the table schemas below, write a query to print the company_code, founder name, total number
of lead managers, total number of senior managers, total number of managers, and total number of
employees. Order your output by ascending company_code.

A:  

                    SELECT 
                        c.company_code,
                        founder,
                        COUNT(DISTINCT l.lead_manager_code) No_of_LMs,
                        COUNT(DISTINCT s.senior_manager_code) No_of_SMs,
                        COUNT(DISTINCT m.manager_code) No_of_Managers,
                        COUNT(DISTINCT e.employee_code) No_of_Employees
                    FROM
                        Company c
                            INNER JOIN
                        Lead_Manager l ON c.company_code = l.company_code
                            INNER JOIN
                        Senior_Manager s ON l.lead_manager_code = s.lead_manager_code
                            INNER JOIN
                        Manager m ON s.senior_manager_code = m.senior_manager_code
                            INNER JOIN
                        Employee e ON m.manager_code = e.manager_code
                    GROUP BY c.company_code , c.founder
                    ORDER BY c.company_code;
                    
 Q143. 










