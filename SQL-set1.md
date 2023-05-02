Q1. Query all columns for all American cities in the CITY table with populations larger than 100000.
The CountryCode for America is USA.

A:
      
      SELECT * FROM City WHERE CountryCode='USA' AND Population > 100000;

Q2. Query the NAME field for all American cities in the CITY table with populations larger than 120000.
The CountryCode for America is USA.

A:
      
      SELECT Name FROM City WHERE CountryCode = 'USA' AND Population > 120000;
      
Q3. Query all columns (attributes) for every row in the CITY table.

A:
      
      SELECT * FROM City;
      
Q4. Query all columns for a city in CITY with the ID 1661.

A:
      
      SELECT * FROM City WHERE Id = 1661;
      
Q5. Query all attributes of every Japanese city in the CITY table. The COUNTRYCODE for Japan is
JPN.

A:
      
      SELECT * FROM City WHERE CountryCode = 'JPN';

Q6. Query the names of all the Japanese cities in the CITY table. The COUNTRYCODE for Japan is
JPN.

A:
      
      SELECT Name FROM City WHERE COuntryCode = 'JPN';
      
Q7. Query a list of CITY and STATE from the STATION table.

A:
      
      SELECT City, State FROM Station;
      
Q8. Query a list of CITY names from STATION for cities that have an even ID number. Print the results
in any order, but exclude duplicates from the answer.

A: 
      
      SELECT DISTINCT City FROM Station WHERE Id%2=0 ORDER BY City;
      
Q9. Find the difference between the total number of CITY entries in the table and the number of
distinct CITY entries in the table.

A:
      
      SELECT COUNT(City)-COUNT(DISTINCT City) as Diff_between_total_cities_and_distinct_cities FROM Station;
      
Q10. Query the two cities in STATION with the shortest and longest CITY names, as well as their
respective lengths (i.e.: number of characters in the name). If there is more than one smallest or
largest city, choose the one that comes first when ordered alphabetically.

A:
      
      SELECT City, length(City) as Length_of_CityName FROM Station ORDER BY length(City),City LIMIT 1;
      SELECT City, length(City) as Length_of_CityName FROM Station ORDER BY length(City) DESC,City LIMIT 1;
      
Q11. Query the list of CITY names starting with vowels (i.e., a, e, i, o, or u) from STATION. Your result
cannot contain duplicates.

A:
      
      SELECT DISTINCT City FROM Station WHERE SUBSTRING(City,1,1) IN ('A','E','I','O','U'); 
      
Q12. Query the list of CITY names ending with vowels (a, e, i, o, u) from STATION. Your result cannot
contain duplicates.

A:
      
      SELECT DISTINCT City FROM Station WHERE SUBSTRING(City,-1,1) IN ('A','E','I','O','U');
      
Q13. Query the list of CITY names from STATION that do not start with vowels. Your result cannot
contain duplicates.

A:
      
      SELECT DISTINCT City FROM Station WHERE SUBSTRING(City,1,1) NOT IN ('A','E','I','O','U'); 
      
Q14. Query the list of CITY names from STATION that do not end with vowels. Your result cannot
contain duplicates.

A:
      
      SELECT DISTINCT City FROM Station WHERE SUBSTRING(City,-1,1) NOT IN ('A','E','I','O','U');
      
Q15. Query the list of CITY names from STATION that either do not start with vowels or do not end
with vowels. Your result cannot contain duplicates.

A:
      
      SELECT DISTINCT City 
      FROM Station 
      WHERE SUBSTRING(City,1,1) NOT IN ('A','E','I','O','U') OR SUBSTRING(City,-1,1) NOT IN ('A','E','I','O','U'); 
      
Q16. Query the list of CITY names from STATION that do not start with vowels and do not end with
vowels. Your result cannot contain duplicates.

A:
       
       SELECT DISTINCT City 
       FROM Station 
       WHERE SUBSTRING(City,1,1) NOT IN ('A','E','I','O','U') AND SUBSTRING(City,-1,1) NOT IN ('A','E','I','O','U');
       

      

      
