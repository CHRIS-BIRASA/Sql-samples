This LIBRARY MANAGEMENT Project simply focuses on monitoring the Library 
Operations. 
It records all the Customers who borrowed books and it has all the books stored in the library shelves, their publishers and their categories and the transactions made by the customer. 
Database and Tables: Created a simple library management system with tables for categories, customers, books, and borrow transactions.
Insert, Update, Delete Operations: Demonstrated basic SQL operations for inserting, updating, and deleting records.
Foreign Keys: Established relationships between tables (e.g., books linked to categories, borrows linked to customers and books).
Joins: Used a JOIN query to combine information from different tables for comprehensive data retrieval. here are some breakdown of the queries used.
mysql> create database library_system;
Query OK, 1 row affected (0.02 sec)

mysql> use library-system
Database changed

TABLES CREATION
mysql> create table  categories(category_id int primary key, category_name varchar(100)
Query OK, 0 rows affected (0.06 sec)

mysql> create table customers(customer_id int primary key, name varchar(20),email varchar(40),phone_no int(10));
Query OK, 0 rows affected, 1 warning (0.01 sec)

mysql> create table books (book_id int primary key,title varchar(100),author varchar(30),category_id int, constraint fk_categories foreign key (category_id) references categories(category_id));
Query OK, 0 rows affected (0.02 sec)

mysql> create table borrows (borrow_id int primary key, customer_id int,book_id
int, borrow_date date,return_date date,constraint fk_customers foreign key(customer_id)references customers(customer_id),constraint fk_books foreign key(book_id)references books(book_id));
Query OK, 0 rows affected (0.03 sec)

INSERTING  & SELECTING VALUES
mysql> insert into categories (category_id,category_name) values (1,'fiction');
Query OK, 1 row affected (0.01 sec)

mysql> insert into categories (category_id,category_name) values (2,'Non-fiction
');
Query OK, 1 row affected (0.00 sec)

mysql> select * from categories ;
+-------------+---------------+
| category_id | category_name |
+-------------+---------------+
|           1 | fiction       |
|           2 | Non-fiction   |
+-------------+---------------+
2 rows in set (0.00 sec)

mysql> insert into customers (customer_id,name,email,phone_no) values (1,'John Doe','johndoe@gmail.com','0789653732');
Query OK, 1 row affected (0.00 sec)

mysql> insert into customers (customer_id,name,email,phone_no) values (2,'Jane be','janebe@gmail.com','0789653452');
Query OK, 1 row affected (0.00 sec)

mysql> select * from customers;
+-------------+----------+-------------------+-----------+
| customer_id | name     | email             | phone_no  |
+-------------+----------+-------------------+-----------+
|           1 | John Doe | johndoe@gmail.com | 789653732 |
|           2 | Jane be  | janebe@gmail.com  | 789653452 |
+-------------+----------+-------------------+-----------+
2 rows in set (0.01 sec)

mysql> insert into books(book_id,title,author,category_id) values (1,'TOXICITY','Future',2);
Query OK, 1 row affected (0.01 sec)

mysql> select * from books;
+---------+----------+--------+-------------+
| book_id | title    | author | category_id |
+---------+----------+--------+-------------+
|       1 | TOXICITY | Future |           2 |
+---------+----------+--------+-------------+
1 row in set (0.01 sec)

mysql> insert into borrows(borrow_id,customer_id,book_id,borrow_date,return_date) values (1,1,1,'2020-02-02','2020-03-02');
Query OK, 1 row affected (0.00 sec)

mysql> select * from borrows;
+-----------+-------------+---------+-------------+-------------+
| borrow_id | customer_id | book_id | borrow_date | return_date |
+-----------+-------------+---------+-------------+-------------+
|         1 |           1 |       1 | 2020-02-02  | 2020-03-02  |
+-----------+-------------+---------+-------------+-------------+
1 row in set (0.00 sec)
 
UPDATING VALUES
mysql> update customer set email ='doejohn@gmail.com' where customer_id=1;
ERROR 1146 (42S02): Table 'library_system.customer' doesn't exist
mysql> update customers set email ='doejohn@gmail.com' where customer_id=1;
Query OK, 1 row affected (0.01 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> select * from customers;
+-------------+----------+-------------------+-----------+
| customer_id | name     | email             | phone_no  |
+-------------+----------+-------------------+-----------+
|           1 | John Doe | doejohn@gmail.com | 789653732 |
|           2 | Jane be  | janebe@gmail.com  | 789653452 |
+-------------+----------+-------------------+-----------+
2 rows in set (0.00 sec)

DELETING VALUES
mysql> delete from borrows where customer_id =1;
Query OK, 1 row affected (0.01 sec)

mysql> select * from borrows;
Empty set (0.00 sec)

mysql> select c.name,b.borrow_date,b.return_date from borrows b join customers c on b.customer_id=c.customer_id;
Empty set (0.00 sec)

mysql> insert into borrows(borrow_id,customer_id,book_id,borrow_date,return_date) values (1,1,1,'2020-02-02','2020-03-02');
Query OK, 1 row affected (0.00 sec)

JOINS AND VIEWS

mysql> select c.name,b.borrow_date,b.return_date from borrows b join customers c on b.customer_id=c.customer_id;
+----------+-------------+-------------+
| name     | borrow_date | return_date |
+----------+-------------+-------------+
| John Doe | 2020-02-02  | 2020-03-02  |
+----------+-------------+-------------+
1 row in set (0.00 sec)



