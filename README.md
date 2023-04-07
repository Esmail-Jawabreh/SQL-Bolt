# SQL Bolt

### What is SQL?
#### SQL, or Structured Query Language, is a language designed to allow both technical and non-technical users query, manipulate, and transform data from a relational database. And due to its simplicity, SQL databases provide safe and scalable storage for millions of websites and mobile applications.

### SQL Bolt:
#### SQLBolt is a series of interactive lessons and exercises designed to help you quickly learn SQL right in your browser.
---
- Link: [SQLBolt](https://sqlbolt.com/).
---
### And Here is the solution for every level: 
#### "please make sure to get benefits and understand it, not only copy and paste."
---
### SQL Lesson 1: SELECT queries 101
#### 1. Find the title of each film
```
SELECT Title FROM Movies;
```
#### 2. Find the director of each film
```
SELECT Director FROM Movies;
```
#### 3. Find the title and director of each film
```
SELECT Title, Director FROM Movies;
```
#### 4. Find the title and year of each film
```
SELECT Title, year FROM Movies;
```
#### 5. Find all the information about each film
```
SELECT * FROM Movies; 
```

---

### SQL Lesson 2: Queries with constraints (Pt. 1)
#### 1. Find the movie with a row id of 6
```
SELECT * FROM Movies 
WHERE Id = 6;
```
#### 2. Find the movies released in the years between 2000 and 2010
```
SELECT * FROM Movies 
WHERE Year BETWEEN 2000 AND 2010;
```
#### 3. Find the movies not released in the years between 2000 and 2010
```
SELECT * FROM Movies 
WHERE Year NOT BETWEEN 2000 AND 2010;
```
#### 4. Find the first 5 Pixar movies and their release year
```
SELECT * FROM Movies 
WHERE Id BETWEEN 1 AND 5;
```



### SQL Lesson 3: Queries with constraints (Pt. 2)
#### 1. Find all the Toy Story movies 
```
SELECT * FROM Movies 
WHERE Title LIKE "%Toy Story%";
```
#### 2. Find all the movies directed by John Lasseter
```
SELECT * FROM Movies 
WHERE Director = "John Lasseter";
```
#### 3. Find all the movies (and director) not directed by John Lasseter
```
SELECT * FROM Movies 
WHERE Director != "John Lasseter";
```
#### 4. Find all the WALL-* movies
```
SELECT * FROM Movies 
WHERE Title LIKE "%WALL%";
```

---

### SQL Lesson 4: Filtering and sorting Query results
### 1. List all directors of Pixar movies (alphabetically), without duplicates
```
SELECT DISTINCT Director FROM Movies 
ORDER BY Director;
```
#### 2. List the last four Pixar movies released (ordered from most recent to least)
```
SELECT * FROM Movies 
ORDER BY Year DESC LIMIT 4;
```
#### 3. List the first five Pixar movies sorted alphabetically
```
SELECT * FROM Movies 
ORDER BY Title ASC LIMIT 5;
```
#### 4. List the next five Pixar movies sorted alphabetically
```
SELECT * FROM Movies 
ORDER BY Title ASC LIMIT 5 OFFSET 5;
```

---

### SQL Review: Simple SELECT Queries
#### 1. List all the Canadian cities and their populations
```
SELECT * FROM North_american_cities 
WHERE Country LIKE "Canada";
```
#### 2. Order all the cities in the United States by their latitude from north to south
```
SELECT * FROM North_american_cities 
WHERE Country = "United States" 
ORDER BY Latitude DESC;
```
#### 3. List all the cities west of Chicago, ordered from west to east
```
SELECT * FROM North_american_cities 
WHERE Longitude < -87.69 
ORDER BY Longitude ASC;
```
#### 4. List the two largest cities in Mexico (by population)
```
SELECT * FROM North_american_cities 
WHERE Country LIKE "Mexico" 
ORDER BY Population DESC LIMIT 2;
```
#### 5. List the third and fourth largest cities (by population) in the United States and their population
```
SELECT * FROM North_american_cities 
WHERE Country LIKE "United States" 
ORDER BY Population DESC LIMIT 2 OFFSET 2;
```

---

### SQL Lesson 6: Multi-table queries with JOINs
#### 1. Find the domestic and international sales for each movie
```
SELECT Title, International_sales, Domestic_sales FROM Movies JOIN Boxoffice
ON Id=Movie_id;
```
#### 2. Show the sales numbers for each movie that did better internationally rather than domestically
```
SELECT Title, International_sales, Domestic_sales FROM Movies JOIN Boxoffice
ON Id=Movie_id
WHERE International_sales > Domestic_sales;
```
#### 3. List all the movies by their ratings in descending order
```
SELECT Title, Rating FROM Movies JOIN Boxoffice
ON Id=Movie_id
ORDER BY Rating DESC;
```

---

### SQL Lesson 7: OUTER JOINs
#### 1. Find the list of all buildings that have employees
```
SELECT DISTINCT Building FROM Employees
LEFT JOIN Buildings ON Building=Building_name
WHERE Years_employed NOT NULL;
```
#### 2. Find the list of all buildings and their capacity
```
SELECT * FROM Buildings;
```
#### 3. List all buildings and the distinct employee roles in each building (including empty buildings)
```
SELECT DISTINCT Building_name, Role FROM Buildings 
LEFT JOIN employees ON building_name = building;
```

--- 

### SQL Lesson 8: A short note on NULLs
#### 1. Find the name and role of all employees who have not been assigned to a building
```
SELECT * FROM Employees
LEFT JOIN Buildings ON Building_name = Building
WHERE Building IS NULL;

```
#### 2. Find the names of the buildings that hold no employees
```
SELECT * FROM Buildings
LEFT JOIN Employees ON Building_name = Building
WHERE Building IS NULL;
```

--- 

### SQL Lesson 9: Queries with expressions
#### 1. List all movies and their combined sales in millions of dollars
```
SELECT Title, (Domestic_sales + International_sales)/1000000 AS Total_Sales_Millions FROM Movies
LEFT JOIN Boxoffice ON Id=Movie_Id;

```
#### 2. List all movies and their ratings in percent
```
SELECT Title, Rating*10 as Percent FROM Movies
LEFT JOIN Boxoffice ON Id=Movie_Id;
```
#### 3. List all movies that were released on even number years
```
SELECT Title, Year FROM Movies
LEFT JOIN Boxoffice ON Id=Movie_Id
WHERE Year % 2 = 0;

```

--- 

### SQL Lesson 10: Queries with aggregates (Pt. 1)
#### 1. Find the longest time that an employee has been at the studio
```
SELECT MAX(Years_employed) FROM Employees;

```
#### 2. For each role, find the average number of years employed by employees in that role
```
SELECT Role, AVG(Years_Employed)  FROM Employees
GROUP BY Role;
```
#### 3. Find the total number of employee years worked in each building
```
SELECT Building, SUM(Years_Employed) FROM Employees
GROUP BY Building;

```

--- 

### SQL Lesson 11: Queries with aggregates (Pt. 2)
#### 1. Find the number of Artists in the studio (without a HAVING clause)
```
SELECT Role, COUNT(*) AS Number_of_Artists FROM Employees
WHERE Role = "Artist";

```
#### 2. Find the number of Employees of each role in the studio
```
SELECT Role, COUNT(*) FROM Employees
GROUP BY Role;
```
#### 3. Find the total number of years employed by all Engineers
```
SELECT Role, SUM(Years_Employed) FROM Employees
GROUP BY Role
HAVING Role = "Engineer";

```

---

### SQL Lesson 12: Order of execution of a Query
#### 1. Find the number of movies each director has directed
```
SELECT *, COUNT(Title) FROM Movies
GROUP BY Director;

```
#### 2. Find the total domestic and international sales that can be attributed to each director
```
SELECT Director, sum(Domestic_sales + International_Sales) as Total_Sales FROM Movies
LEFT JOIN Boxoffice ON Id = Movie_ID
GROUP BY Director;
```

---

### SQL Lesson 13: Inserting rows
#### 1. Add the studio's new production, Toy Story 4 to the list of movies (you can use any director)
```
INSERT INTO Movies
VALUES (4, "Toy Story 4", "John Lasseter", 2017, 123);

```
#### 2. Toy Story 4 has been released to critical acclaim! It had a rating of 8.7, and made 340 million domestically and 270 million internationally. Add the record to the BoxOffice table.
```
INSERT INTO Boxoffice
VALUES (4, 8.7, 340000000, 270000000);

```

---

### SQL Lesson 14: Updating rows
#### 1. The director for A Bug's Life is incorrect, it was actually directed by John Lasseter
```
UPDATE Movies
SET Director = "John Lasseter"
WHERE Id = 2;

```
#### 2. The year that Toy Story 2 was released is incorrect, it was actually released in 1999
```
UPDATE Movies
SET Year = "1999"
WHERE Id = 3;

```
#### 3. Both the title and director for Toy Story 8 is incorrect! The title should be "Toy Story 3" and it was directed by Lee Unkrich
```
UPDATE Movies
SET Title = "Toy Story 3", Director = "Lee Unkrich"
WHERE Id = 11;

```

---

### SQL Lesson 15: Deleting rows
#### 1. This database is getting too big, lets remove all movies that were released before 2005.
```
DELETE FROM Movies
WHERE Year < 2005;

```
#### 2. Andrew Stanton has also left the studio, so please remove all movies directed by him.
```
DELETE FROM Movies
WHERE Director = "Andrew Stanton";

```

---

### SQL Lesson 16: Creating tables
#### 1. Create a new table named Database with the following columns:
#### – Name A string (text) describing the name of the database
#### – Version A number (floating point) of the latest version of this database
#### – Download_count An integer count of the number of times this database was downloaded
#### This table has no constraints.
```
CREATE TABLE Database (
    Name TEXT,
    Version FLOAT,
    Download_Count INTEGER);

```

---

### SQL Lesson 17: Altering tables
#### 1. Add a column named Aspect_ratio with a FLOAT data type to store the aspect-ratio each movie was released in.
```
ALTER TABLE Movies
  ADD COLUMN Aspect_ratio FLOAT DEFAULT 3;

```
#### Add another column named Language with a TEXT data type to store the language that the movie was released in. Ensure that the default for this language is English.
```
ALTER TABLE Movies
  ADD COLUMN Language TEXT DEFAULT "English";

```

---

### SQL Lesson 18: Dropping tables
#### 1. We've sadly reached the end of our lessons, lets clean up by removing the Movies table
```
DROP TABLE Movies;
```
#### And drop the BoxOffice table as well
```
DROP TABLE BoxOffice;

```

---
![END](./END.png)
---
---

**- Esmail Jawabreh**







