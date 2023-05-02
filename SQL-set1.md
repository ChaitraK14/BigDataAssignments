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
                    
                    





        
 


       
       

      

      
