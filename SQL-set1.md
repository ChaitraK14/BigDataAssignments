Q1. Query all columns for all American cities in the CITY table with populations larger than 100000.
The CountryCode for America is USA.

A:
      
            SELECT 
                *
            FROM
                City
            WHERE
                CountryCode = 'USA'
                    AND Population > 100000;

Q2. Query the NAME field for all American cities in the CITY table with populations larger than 120000.
The CountryCode for America is USA.

A:
      
            SELECT 
                Name
            FROM
                City
            WHERE
                CountryCode = 'USA'
                    AND Population > 120000;
      
Q3. Query all columns (attributes) for every row in the CITY table.

A:
      
            SELECT 
                *
            FROM
                City;
      
Q4. Query all columns for a city in CITY with the ID 1661.

A:
      
            SELECT 
                *
            FROM
                City
            WHERE
                Id = 1661;
      
Q5. Query all attributes of every Japanese city in the CITY table. The COUNTRYCODE for Japan is
JPN.

A:
      
            SELECT 
                *
            FROM
                City
            WHERE
                CountryCode = 'JPN';

Q6. Query the names of all the Japanese cities in the CITY table. The COUNTRYCODE for Japan is
JPN.

A:
      
            SELECT 
                Name
            FROM
                City
            WHERE
                COuntryCode = 'JPN';
      
Q7. Query a list of CITY and STATE from the STATION table.

A:
      
            SELECT 
                City, State
            FROM
                Station;
      
Q8. Query a list of CITY names from STATION for cities that have an even ID number. Print the results
in any order, but exclude duplicates from the answer.

A: 
      
            SELECT DISTINCT
                City
            FROM
                Station
            WHERE
                Id % 2 = 0
            ORDER BY City;
      
Q9. Find the difference between the total number of CITY entries in the table and the number of
distinct CITY entries in the table.

A:
      
            SELECT 
                COUNT(City) - COUNT(DISTINCT City) AS Diff_between_total_cities_and_distinct_cities
            FROM
                Station;
      
Q10. Query the two cities in STATION with the shortest and longest CITY names, as well as their
respective lengths (i.e.: number of characters in the name). If there is more than one smallest or
largest city, choose the one that comes first when ordered alphabetically.

A:
      
            SELECT 
                City, LENGTH(City) AS Length_of_CityName
            FROM
                Station
            ORDER BY LENGTH(City) , City
            LIMIT 1;
            
            SELECT 
                City, LENGTH(City) AS Length_of_CityName
            FROM
                Station
            ORDER BY LENGTH(City) DESC , City
            LIMIT 1;
      
Q11. Query the list of CITY names starting with vowels (i.e., a, e, i, o, or u) from STATION. Your result
cannot contain duplicates.

A:
      
            SELECT DISTINCT
                City
            FROM
                Station
            WHERE
                SUBSTRING(City, 1, 1) IN ('A' , 'E', 'I', 'O', 'U'); 
      
Q12. Query the list of CITY names ending with vowels (a, e, i, o, u) from STATION. Your result cannot
contain duplicates.

A:
      
            SELECT DISTINCT
                City
            FROM
                Station
            WHERE
                SUBSTRING(City, - 1, 1) IN ('A' , 'E', 'I', 'O', 'U');
      
Q13. Query the list of CITY names from STATION that do not start with vowels. Your result cannot
contain duplicates.

A:
      
            SELECT DISTINCT
                City
            FROM
                Station
            WHERE
                SUBSTRING(City, 1, 1) NOT IN ('A' , 'E', 'I', 'O', 'U'); 
      
Q14. Query the list of CITY names from STATION that do not end with vowels. Your result cannot
contain duplicates.

A:
      
            SELECT DISTINCT
                City
            FROM
                Station
            WHERE
                SUBSTRING(City, - 1, 1) NOT IN ('A' , 'E', 'I', 'O', 'U');
      
Q15. Query the list of CITY names from STATION that either do not start with vowels or do not end
with vowels. Your result cannot contain duplicates.

A:
      
            SELECT DISTINCT
                City
            FROM
                Station
            WHERE
                SUBSTRING(City, 1, 1) NOT IN ('A' , 'E', 'I', 'O', 'U')
                    OR SUBSTRING(City, - 1, 1) NOT IN ('A' , 'E', 'I', 'O', 'U');
      
Q16. Query the list of CITY names from STATION that do not start with vowels and do not end with
vowels. Your result cannot contain duplicates.

A:
       
            SELECT DISTINCT
                City
            FROM
                Station
            WHERE
                SUBSTRING(City, 1, 1) NOT IN ('A' , 'E', 'I', 'O', 'U')
                    AND SUBSTRING(City, - 1, 1) NOT IN ('A' , 'E', 'I', 'O', 'U');
       
Q17. Write an SQL query that reports the products that were only sold in the first quarter of 2019. That is,
between 2019-01-01 and 2019-03-31 inclusive.
A:

            SELECT 
                product_id, product_name
            FROM
                product
            WHERE
                product_id NOT IN (SELECT 
                        product_id
                    FROM
                        sales
                    WHERE
                        sale_date NOT BETWEEN '2019-01-01' AND '2019-03-31'); 
                          
Q18. Write an SQL query to find all the authors that viewed at least one of their own articles.
Return the result table sorted by id in ascending order.

A:

            SELECT DISTINCT
                author_id AS id
            FROM
                Views
            WHERE
                author_id = viewer_id
            ORDER BY author_id;
       
Q19. Write an SQL query to find the percentage of immediate orders in the table, rounded to 2 decimal
places.

A:

            SELECT 
                ROUND(Immediate_orders.Immediate / Total_orders.Total * 100,
                        2) AS percentage_of_immediate_orders
            FROM
                (SELECT 
                    COUNT(delivery_id) AS Immediate
                FROM
                    Delivery
                WHERE
                    order_date = customer_pref_delivery_date) Immediate_orders,
                (SELECT 
                    COUNT(*) AS Total
                FROM
                    Delivery) Total_orders;
       
Q20. Write an SQL query to find the ctr of each Ad. Round ctr to two decimal points.
Return the result table ordered by ctr in descending order and by ad_id in ascending order in case of a
tie.

A:


            SELECT 
                ad_id,
                ROUND(IFNULL(SUM(CASE
                                    WHEN action = 'Clicked' THEN 1
                                    ELSE 0
                                END) * 100 / (SUM(CASE
                                    WHEN action = 'Viewed' THEN 1
                                    ELSE 0
                                END) + SUM(CASE
                                    WHEN action = 'Clicked' THEN 1
                                    ELSE 0
                                END)),
                                0),
                        2) AS CTR
            FROM
                Ads
            GROUP BY ad_id
            ORDER BY CTR DESC , ad_id ASC;
       
Q21. Write an SQL query to find the team size of each of the employees.
Return result table in any order.

A:

        SELECT employee_id,
	         count(team_id) over(partition by team_id) as team_size 
        FROM employee 
        ORDER BY employee_id;
        
Q22. Write an SQL query to find the type of weather in each country for November 2019.
The type of weather is:
● Cold if the average weather_state is less than or equal 15,
● Hot if the average weather_state is greater than or equal to 25, and
● Warm otherwise.
Return result table in any order.

A:

            SELECT 
                country_name,
                CASE
                    WHEN AVG(weather_id) <= 15 THEN 'Cold'
                    WHEN AVG(weather_id) >= 25 THEN 'Hot'
                    ELSE 'Warm'
                END AS weather_type
            FROM
                Countries c
                    INNER JOIN
                Weather w ON c.country_id = w.country_id
            WHERE
                MONTH(day) = 11
            GROUP BY country_name
            ORDER BY weather_type;
        
Q23. Write an SQL query to find the average selling price for each product. average_price should be
rounded to 2 decimal places.
Return the result table in any order.

A:

            SELECT 
                p.product_id,
                ROUND(SUM(p.price * u.units) / SUM(u.units), 2) AS average_price
            FROM
                Prices p
                    INNER JOIN
                UnitsSold u ON p.product_id = u.product_id
                    AND u.purchase_date BETWEEN p.start_date AND p.end_date
            GROUP BY p.product_id
            ORDER BY p.product_id;
            
Q24. Write an SQL query to report the first login date for each player.
Return the result table in any order.

A:

            SELECT 
                player_id, MIN(event_date) AS first_login
            FROM
                Activity
            GROUP BY player_id;
         
Q25. Write an SQL query to report the device that is first logged in for each player.
Return the result table in any order.

A:

            SELECT 
                player_id, device_id
            FROM
                Activity
            WHERE
                (player_id , event_date) IN (SELECT 
                        player_id, MIN(event_date) AS first_login
                    FROM
                        Activity
                    GROUP BY player_id);
		    
Q26. Write an SQL query to get the names of products that have at least 100 units ordered in February 2020
and their amount.
Return result table in any order.

A:

		SELECT 
		    p.product_name, SUM(o.unit) AS unit
		FROM
		    Products p
			INNER JOIN
		    Orders o ON p.product_id = o.product_id
		WHERE
		    MONTH(order_date) = 2
		GROUP BY p.product_name
		HAVING SUM(o.unit) >= 100
		ORDER BY SUM(o.unit) DESC;
		
Q27. Write an SQL query to find the users who have valid emails.
A valid e-mail has a prefix name and a domain where:
● The prefix name is a string that may contain letters (upper or lower case), digits, underscore
'_', period '.', and/or dash '-'. The prefix name must start with a letter.
● The domain is '@leetcode.com'.
Return the result table in any order.

A:

		SELECT 
		    *
		FROM
		    Users
		WHERE
		    mail REGEXP '^[a-zA-Z][a-zA-Z0-9\_.-]*@leetcode.com';
		
Q28. Write an SQL query to report the customer_id and customer_name of customers who have spent at
least $100 in each month of June and July 2020.
Return the result table in any order.

A:

		SELECT 
		    c.customer_id, c.name
		FROM
		    Product p
			INNER JOIN
		    Orders o ON p.product_id = o.product_id
			INNER JOIN
		    Customers c ON o.customer_id = c.customer_id
		GROUP BY c.customer_id , c.name
		HAVING (SUM(CASE
		    WHEN MONTH(o.order_date) = 6 THEN price * quantity
		    ELSE 0
		END) >= 100
		    AND SUM(CASE
		    WHEN MONTH(o.order_date) = 7 THEN price * quantity
		    ELSE 0
		END) >= 100);
		
Q29. Write an SQL query to report the distinct titles of the kid-friendly movies streamed in June 2020.
Return the result table in any order.

A:

		SELECT DISTINCT
		    c.title
		FROM
		    TVProgram t
			INNER JOIN
		    Content c ON t.content_id = c.content_id
		WHERE
		    t.program_date LIKE '2020-06-%'
			AND c.Kids_content = 'Y'
			AND c.content_type = 'Movies';
			
Q30. Write an SQL query to find the npv of each query of the Queries table.
Return the result table in any order.

A:

		SELECT 
		    q.id, q.year, IFNULL(n.npv, 0) AS npv
		FROM
		    Queries q
			LEFT JOIN
		    NPV n ON n.id = q.id AND n.year = q.year
		ORDER BY q.id , q.year;
		
Q31. Write an SQL query to find the npv of each query of the Queries table.
Return the result table in any order.

A:

		Same
		
Q32. Write an SQL query to show the unique ID of each user, If a user does not have a unique ID replace just
show null.
Return the result table in any order.

A:

		SELECT 
		    unique_id, name
		FROM
		    Employees e
			LEFT JOIN
		    EmployeeUNI u ON e.id = u.id;
		    
Q33. Write an SQL query to report the distance travelled by each user.
Return the result table ordered by travelled_distance in descending order, if two or more users
travelled the same distance, order them by their name in ascending order.

A:

		SELECT 
		    u.name, IFNULL(SUM(distance), 0) AS travelled_distance
		FROM
		    Users u
			LEFT JOIN
		    Rides r ON u.id = r.user_id
		GROUP BY u.id , u.name
		ORDER BY travelled_distance DESC, u.name ASC;
		
Q34. Write an SQL query to get the names of products that have at least 100 units ordered in February 2020
and their amount.
Return result table in any order.

A:

		SELECT 
		    p.product_name, SUM(unit) AS unit
		FROM
		    Products p
			INNER JOIN
		    Orders o ON p.product_id = o.product_id
		WHERE
		    order_date LIKE '2020-02%'
		GROUP BY p.product_id , p.product_name
		HAVING unit >= 100;
		
Q35. Write an SQL query to:
● Find the name of the user who has rated the greatest number of movies. In case of a tie,
return the lexicographically smaller user name.
● Find the movie name with the highest average rating in February 2020. In case of a tie, return
the lexicographically smaller movie name.

A:

		SELECT 
		    u.name
		FROM
		    Users3 u
			INNER JOIN
		    MovieRating r ON u.user_id = r.user_id
		GROUP BY u.user_id , u.name
		ORDER BY COUNT(*) DESC , u.name ASC
		LIMIT 1;
		
		SELECT 
		    m.title
		FROM
		    Movies m
			INNER JOIN
		    MovieRating r ON m.movie_id = r.movie_id
		WHERE r.created_at LIKE '2020-02%'
		GROUP BY m.movie_id , m.title
		ORDER BY avg(rating) DESC , m.title ASC
		LIMIT 1;
		
Q36. Write an SQL query to report the distance travelled by each user.
Return the result table ordered by travelled_distance in descending order, if two or more users
travelled the same distance, order them by their name in ascending order.

A:

		SELECT 
		    u.name, IFNULL(SUM(distance), 0) AS travelled_distance
		FROM
		    Users u
			LEFT JOIN
		    Rides r ON u.id = r.user_id
		GROUP BY u.id , u.name
		ORDER BY travelled_distance DESC, u.name ASC;
		
Q37. Write an SQL query to show the unique ID of each user, If a user does not have a unique ID replace just
show null.
Return the result table in any order.

A:

		SELECT 
		    unique_id, name
		FROM
		    Employees e
			LEFT JOIN
		    EmployeeUNI u ON e.id = u.id;
		    
Q38. Write an SQL query to find the id and the name of all students who are enrolled in departments that no
longer exist.
Return the result table in any order.

A:  

		SELECT 
		    *
		FROM
		    Students
		WHERE
		    department_id NOT IN (SELECT 
			    id
			FROM
			    Departments);
			    
Q39. Write an SQL query to report the number of calls and the total call duration between each pair of
distinct persons (person1, person2) where person1 < person2.
Return the result table in any order.

A:

		SELECT 
		    LEAST(from_id, to_id) AS person1,
		    GREATEST(from_id, to_id) AS person2,
		    COUNT(*) AS call_count,
		    SUM(duration) AS total_duration
		FROM
		    Calls
		GROUP BY person1 , person2;
		
Q40. Write an SQL query to find the average selling price for each product. average_price should be
rounded to 2 decimal places.
Return the result table in any order.

A:

		SELECT 
		    p.product_id,
		    ROUND(SUM(price * units) / SUM(units), 2) AS average_price
		FROM
		    prices p
			INNER JOIN
		    UnitsSold u ON p.product_id = u.product_id
			AND u.purchase_date BETWEEN p.start_date AND p.end_date
		GROUP BY p.product_id;
		
Q41. Write an SQL query to report the number of cubic feet of volume the inventory occupies in each
warehouse.
Return the result table in any order.

A:

		SELECT 
		    w.name, SUM(units * Width * Length * Height) AS volume
		FROM
		    Warehouse w
			INNER JOIN
		    Products p ON w.product_id = p.product_id
		GROUP BY w.name;
		
Q42. Write an SQL query to report the difference between the number of apples and oranges sold each day.
Return the result table ordered by sale_date.

A:

		SELECT 
		    sale_date,
		    SUM(CASE
			WHEN fruit = 'apples' THEN sold_num
		    END) - SUM(CASE
			WHEN fruit = 'oranges' THEN sold_num
		    END) AS Diff
		FROM
		    Sales
		GROUP BY sale_date;
		
Q43. Write an SQL query to report the fraction of players that logged in again on the day after the day they
first logged in, rounded to 2 decimal places. In other words, you need to count the number of players
that logged in for at least two consecutive days starting from their first login date, then divide that
number by the total number of players.

A:

A:



       
       

      

      
