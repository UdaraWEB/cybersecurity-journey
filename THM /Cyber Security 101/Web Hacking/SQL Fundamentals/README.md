TryHackMe - SQL Fundamentals  (Writeup)

Hey everyone! I just finished the Intro to Databases room on TryHackMe. It was a super fun room covering database basics, 
CRUD operations, and SQL functions. Here is a quick and simple writeup of what I learned and how I solved the challenges.

    1. Database Basics
    
First, I learned the difference between Relational (SQL) and Non-Relational (NoSQL) databases.

Relational: Uses structured tables (Rows & Columns) and links them using keys (Primary Key for unique IDs 
and Foreign Key to link tables).


Non-Relational: Flexible and great for unstructured data that varies in format.

    2. Getting Hands-On with MySQL
    
To start interacting with the database, I logged into the MySQL terminal using:

mysql -u root -p

Inside MySQL, I discovered that every command needs to end with a semicolon ;. Here are the basic commands I practiced:

SHOW DATABASES; -> To list all databases.

USE database_name; -> To select a database.

SHOW TABLES; -> To see the tables inside the active database.

    3. CRUD Operations & Clauses
    
CRUD stands for Create, Read, Update, and Delete.

Create: INSERT INTO table_name VALUES (...);

Read: SELECT * FROM table_name;

Update: UPDATE table_name SET column = value WHERE condition;

Delete: DELETE FROM table_name WHERE condition;

I also used Clauses like DISTINCT (to remove duplicates) and ORDER BY name ASC/DESC to sort the data easily.

    4. Solving the Challenges (Tools DB)
    
For the final parts, we had to switch to a database called tools_db and query a table named hacking_tools. 
Here are the key commands used to find the answers:

Finding specific categories:

SELECT category FROM hacking_tools WHERE amount >= 300;


Finding the tool with the longest name:

Using the LENGTH() function:

SELECT name FROM hacking_tools ORDER BY LENGTH(name) DESC LIMIT 1;

Calculating total sum:

Using the SUM() aggregate function:

SELECT SUM(amount) FROM hacking_tools;

Concatenating data:

Using GROUP_CONCAT to combine rows where the amount didn't end in 0:

SELECT GROUP_CONCAT(name SEPARATOR " & ") FROM hacking_tools WHERE amount NOT LIKE '%0';

Takeaway

Understanding SQL is a huge plus for cybersecurity because it helps you understand how SQL Injection (SQLi) vulnerabilities work.
If a web app doesn't safely check user inputs, hackers can inject their own SQL queries to bypass logins or leak the entire database!
