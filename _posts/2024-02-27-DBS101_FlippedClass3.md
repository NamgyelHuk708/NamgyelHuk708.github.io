---
Title: DBS101 Flipped Class 3
categories: [DBS101, Flipped_Class3]
tags: [DBS101]
---

### Topic : Set Operation and Null value in SQL
----

After learning how Data are used and how its drawn in Entity Relationship Diagram to show its relation. today, we learned what kind of programming language is used in order to access the Data base system to manage and to performe various operation on it.

like python, Java,c++,Java script and many more other programming language to programe a web site or to make a app, we have a programming language know as SQL(Structure Query Language) which is used to access or to modify a Database table. Then we have SQL set operations which are used to combine the results of two or more SQL SELECT statements.Before looking into the types of the operation we have a condition that must be fulfilled inoreder for the operation to take place and that is the number of columbs and the data type must be same across all SELECTED statements.

Now comes the types of Set operation in SQl:
1. Union: Combines the results of two or more SELECT queries into a single result set without the duplicate rows instead it clubs to one row.
2. Union All: It's similar to UNION, but it allows duplicate rows in the result set. 
3. Intersect: It returns the common rows from both the SELECT statements and by default it arranges the data in ascending order.
4. Minus/EXCEPT: It only display the rows which are present in the first query but absent in the second query.

We also learned that a null values in SQL means that the value does not exist in the database. Which might be because they were left blank during the time of record or by some bias it was unfilled. A NULL value is different from a zero value so they can be interpreted as a value that exists but is not known or exists but is purposely not given or not applicable for this entry. Moreover, I also learned that aggregate functions like(SUM, AVG, MIN, MAX) simply ignore the NULL values.
