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
            
  Q110. 


