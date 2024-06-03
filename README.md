# SQL_HW1

What are joins?
They are to fetch the rows from two or more related tables
Columns being joined have be compatiable with each other meaning the terms of data type and based on that common field the MySQL JOINS retrieves the data. 

It should be used when you have to use multiple queries because it puts it into one query with any search parameters making it easier compare to subqueries

Types of joins:

Inner Join:
The Inner join returns only the matching records from both the tables involved in the Join. Non-matching records are eliminated.
Outer Join:
The Outer Join retrieves the matching records as well as non-matching records from both the tables involved in the join in MySQL.
Cross Join:
If two or more tables are combined with each other without any condition then we call it cross join in MySQL. In cross join, each record of a table is joins with each record of another table.

(Inner and Outer Join use ON clauses while Cross Join doesn't!!!1)


Inner Join
An INNER JOIN returns the rows that have matching values of both table1 and table2. The ON clause specifies which columns to compare and what condition must be met for the rows to match.
To use enter either KeyWord: INNER JOIN / JOIN 
They both mean the same thing but for its better to use INNER JOIN because you know whats happening

Example:
mysql> SELECT Id as EmployeeID, Name, Department, City, Title as Project, ClientId
    -> FROM Employee
    -> INNER JOIN Projects
    -> ON Employee.Id = Projects.EmployeeId;
+------------+-------------------+------------+--------+--------------------------------------------+----------+
| EmployeeID | Name              | Department | City   | Project                                    | ClientId |
+------------+-------------------+------------+--------+--------------------------------------------+----------+
|       1001 | John Doe          | IT         | London | Hosting account is not working             |        3 |
|       1002 | Mary Smith        | HR         | London | WordPress website for our company          |        1 |
|       1003 | James Brown       | Finance    | London | Develop ecommerse website from scratch     |        1 |
|       1004 | Mike Walker       | Finance    | London | Android Application development            |        4 |
|       1007 | Priyanla Dewangan | HR         | Mumbai | Manage our company servers                 |        2 |
|       1008 | Sambit Mohanty    | IT         | Mumbai | MySQL database from my desktop application |        4 |
|       1009 | Pranaya Kumar     | IT         | Mumbai | Hosting account is not working             |        3 |
|       1010 | Hina Sharma       | HR         | Mumbai | MySQL database from my desktop application |        4 |
+------------+-------------------+------------+--------+--------------------------------------------+----------+
8 rows in set (0.00 sec)
The query only got matching things and discarded anyhting that wasn't like NULL values

Like said before you can interchange INNER JOIN with JOIN 


Outer Join
An OUTER JOIN returns returns all the matching rows from both tables, plus any unmatched rows from both tables. While also having three types which are:
-> Left Outer Join
-> Right Outer Join
-> Full Outer Join

A. Left Outer Join
The left Outer Join returns all the matching rows from both tables also any unmatched rows from the left table. Left being what table name is on the LEFT side of the KEYWORD and not the right. With that unmatched rows from the left table will have null values for columns from the right table. 

When using the syntax you could use these Keywords: LEFT OUTER JOIN / LEFT JOIN

Example:
mysql> SELECT Id as EmployeeID, Name, Department, City, Title as Project, ClientId
    -> FROM Employee
    -> LEFT OUTER JOIN Projects
    -> ON Employee.Id = Projects.EmployeeId;
+------------+-------------------+------------+--------+--------------------------------------------+----------+
| EmployeeID | Name              | Department | City   | Project                                    | ClientId |
+------------+-------------------+------------+--------+--------------------------------------------+----------+
|       1001 | John Doe          | IT         | London | Hosting account is not working             |        3 |
|       1002 | Mary Smith        | HR         | London | WordPress website for our company          |        1 |
|       1003 | James Brown       | Finance    | London | Develop ecommerse website from scratch     |        1 |
|       1004 | Mike Walker       | Finance    | London | Android Application development            |        4 |
|       1005 | Linda Jones       | HR         | London | NULL                                       |     NULL |
|       1006 | Anurag Mohanty    | IT         | Mumbai | NULL                                       |     NULL |
|       1007 | Priyanla Dewangan | HR         | Mumbai | Manage our company servers                 |        2 |
|       1008 | Sambit Mohanty    | IT         | Mumbai | MySQL database from my desktop application |        4 |
|       1009 | Pranaya Kumar     | IT         | Mumbai | Hosting account is not working             |        3 |
|       1010 | Hina Sharma       | HR         | Mumbai | MySQL database from my desktop application |        4 |
+------------+-------------------+------------+--------+--------------------------------------------+----------+
10 rows in set (0.00 sec)

To select all records from the left table, including those with null values for the foreign key, use a LEFT OUTER JOIN. This gets all matching rows from both tables and also includes non-matching rows from the left table.


B. Right Outer Join
THIS DOES THE SAME THING AS THE LEFT OUTER JOIN!!!!
The only thing different is that the table it gets it from is the right instead of the left

When using the syntax you could use these Keywords: RIGHT OUTER JOIN / RIGHT JOIN

mysql> SELECT Employee.Id as EmployeeId, Name, Department, City, Title as Project
    -> FROM Employee
    -> RIGHT OUTER JOIN Projects
    -> ON Employee.Id = Projects.EmployeeId;
+------------+-------------------+------------+--------+------------------------------------------------------+
| EmployeeId | Name              | Department | City   | Project                                              |
+------------+-------------------+------------+--------+------------------------------------------------------+
|       1003 | James Brown       | Finance    | London | Develop ecommerse website from scratch               |
|       1002 | Mary Smith        | HR         | London | WordPress website for our company                    |
|       1007 | Priyanla Dewangan | HR         | Mumbai | Manage our company servers                           |
|       1009 | Pranaya Kumar     | IT         | Mumbai | Hosting account is not working                       |
|       1010 | Hina Sharma       | HR         | Mumbai | MySQL database from my desktop application           |
|       NULL | NULL              | NULL       | NULL   | Develop new WordPress plugin for my business website |
|       NULL | NULL              | NULL       | NULL   | Migrate web application and database to new server   |
|       1004 | Mike Walker       | Finance    | London | Android Application development                      |
|       1001 | John Doe          | IT         | London | Hosting account is not working                       |
|       1008 | Sambit Mohanty    | IT         | Mumbai | MySQL database from my desktop application           |
|       NULL | NULL              | NULL       | NULL   | Develop new WordPress plugin for my business website |
+------------+-------------------+------------+--------+------------------------------------------------------+
11 rows in set (0.00 sec)
 
To select all records from the right table, including those with null values for the foreign key, use a RIGHT OUTER JOIN. This gets all matching rows from both tables and also includes non-matching rows from the Right table.


C. Full Outer Join
Full Outer Join retrieves all the matching rows from both the tables as well as non-matching rows from both the tables. The difference is that SQL doesn't support this so we have to use a operator called UNION.

Example:
mysql> SELECT Employee.Id as EmployeeId, Name, Department, City, Title as Project
    -> FROM Employee
    -> LEFT OUTER JOIN Projects
    -> ON Employee.Id = Projects.EmployeeId
    -> UNION
    -> SELECT Employee.Id as EmployeeId, Name, Department, City, Title as Project
    -> FROM Employee
    -> RIGHT OUTER JOIN Projects
    -> ON Employee.Id = Projects.EmployeeId;
+------------+-------------------+------------+--------+------------------------------------------------------+
| EmployeeId | Name              | Department | City   | Project                                              |
+------------+-------------------+------------+--------+------------------------------------------------------+
|       1001 | John Doe          | IT         | London | Hosting account is not working                       |
|       1002 | Mary Smith        | HR         | London | WordPress website for our company                    |
|       1003 | James Brown       | Finance    | London | Develop ecommerse website from scratch               |
|       1004 | Mike Walker       | Finance    | London | Android Application development                      |
|       1005 | Linda Jones       | HR         | London | NULL                                                 |
|       1006 | Anurag Mohanty    | IT         | Mumbai | NULL                                                 |
|       1007 | Priyanla Dewangan | HR         | Mumbai | Manage our company servers                           |
|       1008 | Sambit Mohanty    | IT         | Mumbai | MySQL database from my desktop application           |
|       1009 | Pranaya Kumar     | IT         | Mumbai | Hosting account is not working                       |
|       1010 | Hina Sharma       | HR         | Mumbai | MySQL database from my desktop application           |
|       NULL | NULL              | NULL       | NULL   | Develop new WordPress plugin for my business website |
|       NULL | NULL              | NULL       | NULL   | Migrate web application and database to new server   |
+------------+-------------------+------------+--------+------------------------------------------------------+
12 rows in set (0.07 sec)

Cross Join
The Cross Join returns matched data rows as well as unmatched data rows from the table. Each record of a table is joined with each record of the other table involved in the join.

Example:
mysql> SELECT Employee.Id as EmployeeId, Name, Department, City, Title as Project
    -> FROM Employee
    -> CROSS JOIN Projects;
+------------+-------------------+------------+--------+------------------------------------------------------+
| EmployeeId | Name              | Department | City   | Project                                              |
+------------+-------------------+------------+--------+------------------------------------------------------+
|       1010 | Hina Sharma       | HR         | Mumbai | Develop ecommerse website from scratch               |
|       1009 | Pranaya Kumar     | IT         | Mumbai | Develop ecommerse website from scratch               |
|       1008 | Sambit Mohanty    | IT         | Mumbai | Develop ecommerse website from scratch               |
|       1007 | Priyanla Dewangan | HR         | Mumbai | Develop ecommerse website from scratch               |
|       1006 | Anurag Mohanty    | IT         | Mumbai | Develop ecommerse website from scratch               |
|       1005 | Linda Jones       | HR         | London | Develop ecommerse website from scratch               |
|       1004 | Mike Walker       | Finance    | London | Develop ecommerse website from scratch               |
|       1003 | James Brown       | Finance    | London | Develop ecommerse website from scratch               |
|       1002 | Mary Smith        | HR         | London | Develop ecommerse website from scratch               |
|       1001 | John Doe          | IT         | London | Develop ecommerse website from scratch               |
|       1010 | Hina Sharma       | HR         | Mumbai | WordPress website for our company                    |
|       1009 | Pranaya Kumar     | IT         | Mumbai | WordPress website for our company                    |
|       1008 | Sambit Mohanty    | IT         | Mumbai | WordPress website for our company                    |
|       1007 | Priyanla Dewangan | HR         | Mumbai | WordPress website for our company                    |
|       1006 | Anurag Mohanty    | IT         | Mumbai | WordPress website for our company                    |
|       1005 | Linda Jones       | HR         | London | WordPress website for our company                    |
|       1004 | Mike Walker       | Finance    | London | WordPress website for our company                    |
|       1003 | James Brown       | Finance    | London | WordPress website for our company                    |
|       1002 | Mary Smith        | HR         | London | WordPress website for our company                    |
|       1001 | John Doe          | IT         | London | WordPress website for our company                    |
|       1010 | Hina Sharma       | HR         | Mumbai | Manage our company servers                           |
|       1009 | Pranaya Kumar     | IT         | Mumbai | Manage our company servers                           |
|       1008 | Sambit Mohanty    | IT         | Mumbai | Manage our company servers                           |
|       1007 | Priyanla Dewangan | HR         | Mumbai | Manage our company servers                           |
|       1006 | Anurag Mohanty    | IT         | Mumbai | Manage our company servers                           |
|       1005 | Linda Jones       | HR         | London | Manage our company servers                           |
|       1004 | Mike Walker       | Finance    | London | Manage our company servers                           |
|       1003 | James Brown       | Finance    | London | Manage our company servers                           |
|       1002 | Mary Smith        | HR         | London | Manage our company servers                           |
|       1001 | John Doe          | IT         | London | Manage our company servers                           |
|       1010 | Hina Sharma       | HR         | Mumbai | Hosting account is not working                       |
|       1009 | Pranaya Kumar     | IT         | Mumbai | Hosting account is not working                       |
|       1008 | Sambit Mohanty    | IT         | Mumbai | Hosting account is not working                       |
|       1007 | Priyanla Dewangan | HR         | Mumbai | Hosting account is not working                       |
|       1006 | Anurag Mohanty    | IT         | Mumbai | Hosting account is not working                       |
|       1005 | Linda Jones       | HR         | London | Hosting account is not working                       |
|       1004 | Mike Walker       | Finance    | London | Hosting account is not working                       |
|       1003 | James Brown       | Finance    | London | Hosting account is not working                       |
|       1002 | Mary Smith        | HR         | London | Hosting account is not working                       |
|       1001 | John Doe          | IT         | London | Hosting account is not working                       |
|       1010 | Hina Sharma       | HR         | Mumbai | MySQL database from my desktop application           |
|       1009 | Pranaya Kumar     | IT         | Mumbai | MySQL database from my desktop application           |
|       1008 | Sambit Mohanty    | IT         | Mumbai | MySQL database from my desktop application           |
|       1007 | Priyanla Dewangan | HR         | Mumbai | MySQL database from my desktop application           |
|       1006 | Anurag Mohanty    | IT         | Mumbai | MySQL database from my desktop application           |
|       1005 | Linda Jones       | HR         | London | MySQL database from my desktop application           |
|       1004 | Mike Walker       | Finance    | London | MySQL database from my desktop application           |
|       1003 | James Brown       | Finance    | London | MySQL database from my desktop application           |
|       1002 | Mary Smith        | HR         | London | MySQL database from my desktop application           |
|       1001 | John Doe          | IT         | London | MySQL database from my desktop application           |
|       1010 | Hina Sharma       | HR         | Mumbai | Develop new WordPress plugin for my business website |
|       1009 | Pranaya Kumar     | IT         | Mumbai | Develop new WordPress plugin for my business website |
|       1008 | Sambit Mohanty    | IT         | Mumbai | Develop new WordPress plugin for my business website |
|       1007 | Priyanla Dewangan | HR         | Mumbai | Develop new WordPress plugin for my business website |
|       1006 | Anurag Mohanty    | IT         | Mumbai | Develop new WordPress plugin for my business website |
|       1005 | Linda Jones       | HR         | London | Develop new WordPress plugin for my business website |
|       1004 | Mike Walker       | Finance    | London | Develop new WordPress plugin for my business website |
|       1003 | James Brown       | Finance    | London | Develop new WordPress plugin for my business website |
|       1002 | Mary Smith        | HR         | London | Develop new WordPress plugin for my business website |
|       1001 | John Doe          | IT         | London | Develop new WordPress plugin for my business website |
|       1010 | Hina Sharma       | HR         | Mumbai | Migrate web application and database to new server   |
|       1009 | Pranaya Kumar     | IT         | Mumbai | Migrate web application and database to new server   |
|       1008 | Sambit Mohanty    | IT         | Mumbai | Migrate web application and database to new server   |
|       1007 | Priyanla Dewangan | HR         | Mumbai | Migrate web application and database to new server   |
|       1006 | Anurag Mohanty    | IT         | Mumbai | Migrate web application and database to new server   |
|       1005 | Linda Jones       | HR         | London | Migrate web application and database to new server   |
|       1004 | Mike Walker       | Finance    | London | Migrate web application and database to new server   |
|       1003 | James Brown       | Finance    | London | Migrate web application and database to new server   |
|       1002 | Mary Smith        | HR         | London | Migrate web application and database to new server   |
|       1001 | John Doe          | IT         | London | Migrate web application and database to new server   |
|       1010 | Hina Sharma       | HR         | Mumbai | Android Application development                      |
|       1009 | Pranaya Kumar     | IT         | Mumbai | Android Application development                      |
|       1008 | Sambit Mohanty    | IT         | Mumbai | Android Application development                      |
|       1007 | Priyanla Dewangan | HR         | Mumbai | Android Application development                      |
|       1006 | Anurag Mohanty    | IT         | Mumbai | Android Application development                      |
|       1005 | Linda Jones       | HR         | London | Android Application development                      |
|       1004 | Mike Walker       | Finance    | London | Android Application development                      |
|       1003 | James Brown       | Finance    | London | Android Application development                      |
|       1002 | Mary Smith        | HR         | London | Android Application development                      |
|       1001 | John Doe          | IT         | London | Android Application development                      |
|       1010 | Hina Sharma       | HR         | Mumbai | Hosting account is not working                       |
|       1009 | Pranaya Kumar     | IT         | Mumbai | Hosting account is not working                       |
|       1008 | Sambit Mohanty    | IT         | Mumbai | Hosting account is not working                       |
|       1007 | Priyanla Dewangan | HR         | Mumbai | Hosting account is not working                       |
|       1006 | Anurag Mohanty    | IT         | Mumbai | Hosting account is not working                       |
|       1005 | Linda Jones       | HR         | London | Hosting account is not working                       |
|       1004 | Mike Walker       | Finance    | London | Hosting account is not working                       |
|       1003 | James Brown       | Finance    | London | Hosting account is not working                       |
|       1002 | Mary Smith        | HR         | London | Hosting account is not working                       |
|       1001 | John Doe          | IT         | London | Hosting account is not working                       |
|       1010 | Hina Sharma       | HR         | Mumbai | MySQL database from my desktop application           |
|       1009 | Pranaya Kumar     | IT         | Mumbai | MySQL database from my desktop application           |
|       1008 | Sambit Mohanty    | IT         | Mumbai | MySQL database from my desktop application           |
|       1007 | Priyanla Dewangan | HR         | Mumbai | MySQL database from my desktop application           |
|       1006 | Anurag Mohanty    | IT         | Mumbai | MySQL database from my desktop application           |
|       1005 | Linda Jones       | HR         | London | MySQL database from my desktop application           |
|       1004 | Mike Walker       | Finance    | London | MySQL database from my desktop application           |
|       1003 | James Brown       | Finance    | London | MySQL database from my desktop application           |
|       1002 | Mary Smith        | HR         | London | MySQL database from my desktop application           |
|       1001 | John Doe          | IT         | London | MySQL database from my desktop application           |
|       1010 | Hina Sharma       | HR         | Mumbai | Develop new WordPress plugin for my business website |
|       1009 | Pranaya Kumar     | IT         | Mumbai | Develop new WordPress plugin for my business website |
|       1008 | Sambit Mohanty    | IT         | Mumbai | Develop new WordPress plugin for my business website |
|       1007 | Priyanla Dewangan | HR         | Mumbai | Develop new WordPress plugin for my business website |
|       1006 | Anurag Mohanty    | IT         | Mumbai | Develop new WordPress plugin for my business website |
|       1005 | Linda Jones       | HR         | London | Develop new WordPress plugin for my business website |
|       1004 | Mike Walker       | Finance    | London | Develop new WordPress plugin for my business website |
|       1003 | James Brown       | Finance    | London | Develop new WordPress plugin for my business website |
|       1002 | Mary Smith        | HR         | London | Develop new WordPress plugin for my business website |
|       1001 | John Doe          | IT         | London | Develop new WordPress plugin for my business website |
+------------+-------------------+------------+--------+------------------------------------------------------+
110 rows in set (0.03 sec)

The total number of times values printed is based on what table start ON THE LEFT and how many rows of each value is based ON THE RIGHT table.



