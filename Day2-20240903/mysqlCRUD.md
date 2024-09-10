# mysql basic commands 

1. setup the environment 

2. mysql -uroot 
    - this is without password

3. mysql -uroot -p
    - with password

4. mysql -uroot -p -P3307
    - with password plus specified PORT

5. use mysql    
    - for using any existing database
    - after use word write the database name 
    - here mysql is database name
    - note: never use mysql named db

6. CREATE DATABASE db1
    - for creating new database
    - after DATABASE add db name 
    - here db1 is new dababase name
    - after petfoming this command my new database called as db1 will be created.

7. use db1
    - change the db whatever you want to use.

8. CREATE TABLE table_name ( // add your fields );
    - for creating tables
    - after TABLE enter the name of table 
    - here table_name is the name of table
    - ex.   
        - CREATE TABLE employees (
            id INT AUTO_INCREMENT PRIMARY KEY,
            name VARCHAR(100) NOT NULL,
            position VARCHAR(100),
            salary DECIMAL(10, 2)
        );
        
9. INSERT INTO employees (name, position, salary)
    VALUES ('John Doe', 'Developer', 60000);
    - for insert column in row of table

10. SELECT * FROM table_name;
    - check the table

11. UPDATE employees
    SET salary = 65000
    WHERE name = 'John Doe';
     - update any data of column in row of table

12. DELETE FROM table_name
    WHERE condition;
     - delete any data based on specific condition
     - ex.
        - DELETE FROM employees
            WHERE name = 'John Doe';


13. ALTER TABLE table_name
    ADD column_name datatype constraints;
    - Alter the table
    - adding new column
    - ex.
        - ALTER TABLE employees
        ADD hire_date DATE;

14. ALTER TABLE table_name
    MODIFY column_name new_datatype constraints;
    - Modify an existing column
    - ex.
        - ALTER TABLE employees
            MODIFY salary DECIMAL(12, 2);

15. ALTER TABLE table_name
    DROP COLUMN column_name;
    - delete/drop any column
    - ex.
        - ALTER TABLE employees
            DROP COLUMN hire_date;

16. DROP TABLE table_name;
    - delete/drop any table
    - ex.
        - DROP TABLE employees;

17. CREATE USER 'username'@'localhost' IDENTIFIED BY 'password';
    - Create a User and Assign a Password
    - ex.   
        - CREATE USER 'my_user'@'localhost' IDENTIFIED BY 'my_password';

18. GRANT ALL PRIVILEGES ON database_name.* TO 'username'@'localhost';
    - Grant Privileges to the User
    - Grant all privileges on the database to the user
    - ex.
        - GRANT ALL PRIVILEGES ON my_database.* TO 'my_user'@'localhost';

19. FLUSH PRIVILEGES;
    - Apply changes.

20. SHOW TABLES;
    - Show Tables in a Database

21. DESCRIBE table_name;
    - This command shows the structure of the table, including columns, data types, and constraints.

22. OPTIMIZE TABLE table_name;
    - The OPTIMIZE TABLE command is used to defragment a table and reclaim unused space. 
    - It's particularly useful after you have made many updates or deletions in a table. 
    - The command works by reorganizing the physical storage of the data and index pages.
    - When to Use OPTIMIZE TABLE:
        - After deleting a large number of rows.
        - After performing many UPDATE operations that modify data extensively.
        - To reclaim unused space and improve performance.
    - ex.
        - OPTIMIZE TABLE employees;

23. REPAIR TABLE table_name [QUICK] [EXTENDED];
    - ex.
        - REPAIR TABLE employees;

24. 


