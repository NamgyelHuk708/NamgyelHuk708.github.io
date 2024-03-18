---
Title: DBS101 Flipped Class 4
categories: [DBS101, Flipped_Class4]
tags: [DBS101]
---

### Topic :  Advanced Aggregation Functions
----
**Take away points**
1. Implement advanced aggregation functions like Ranking, Windowing, Pivoting, Rollup and cube.
2. Understand the need for advanced aggregation functions.

Aggregate functions in SQL are like handy tools for summarizing and analyzing data. They help us crunch a bunch of values into just one. By using these functions, we can do things like calculate totals or averages from groups of data rows. It's super useful for quickly figuring out stats or getting a summary of a big set of data. Ranking, windowing, pivoting, rollup, and cube are advanced SQL concepts related to aggregated functions, each serving a unique purpose in data analysis and reporting.

| Aggregate function | Description | Function |
| ----------- | ----------- | ----------- |
| Ranking |  ordering rows within a partition of a result set | RANK(), DENSE_RANK(), and ROW_NUMBER() | SUM(), AVG(), MIN(), MAX(), and COUNT(), are used with the OVER() |
| Windowing | a technique that allows user to perform calculations across a set of rows that are related to the current row | SUM(), AVG(), MIN(), MAX() and COUNT() |
| Pivoting |  transforming rows into columns to create a more readable format | combination of aggregate functions and the CASE statement |
| Rollup |  a type of grouping that creates subtotals and grand totals | ROLLUP and GROUP BY |
| Cube | Similar to rollup, but generates subtotals for all combinations of the specified columns | CUBE and GROUP BY |

**Examples**
1. Ranking : For example, To rank employees by salary, we can use the RANK() function. The query will rank the employees based on their salary in descending order.
![alt text](ranking.png)

2. Windowing: For example, To calculate a running total of order totals, we can use the SUM() function with the OVER() clause. The query calculates a running total of order totals, ordered by OrderID.
![alt text](windowing.png)

3. Pivoting: For example, We can pivots sales data by product, showing sales for each product as separate columns.
![alt text](pivoting.png)

4. Rollup: For example, To generate subtotals and grand totals for sales by year, we can use the ROLLUP operator. The query generates subtotals for each year and a grand total. 
![alt text](rollup.png)

5. Cube: For example, To generate subtotals for all combinations of years and products, we can use the CUBE operator. The query generates subtotals for each combination of year and product, as well as grand totals.
![alt text](cube.png)