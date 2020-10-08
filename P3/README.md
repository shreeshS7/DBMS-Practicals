
# P3

## Design at least 10 SQL queries for suitable database application using SQL DML statements: Insert, Select, Update, Delete with operators, functions, and set operator.

### DML

> INSERT, UPDATE, DELETE  (SELECT)

*Lets create a table first and insert some values*

```
mysql> create table employee(
    -> id integer primary key,
    -> name varchar(20) not null,
    -> age integer not null,
    -> salary double not null);
Query OK, 0 rows affected (2.29 sec)
```

**INSERT**

```
insert into employee values (1,'Shree',20,25000.50);
insert into employee values (2,'Krishna',21,50000.75);
insert into employee values (3,'Govind',23,75000.50);
insert into employee values (4,'Madhav',19,2500.50);
insert into employee values (5,'Kanha',21,700.25);

```

```
mysql> select * from employee;
+----+---------+-----+----------+
| id | name    | age | salary   |
+----+---------+-----+----------+
|  1 | Shree   |  20 |  25000.5 |
|  2 | Krishna |  21 | 50000.75 |
|  3 | Govind  |  23 |  75000.5 |
|  4 | Madhav  |  19 |   2500.5 |
|  5 | Kanha   |  21 |   700.25 |
+----+---------+-----+----------+
5 rows in set (0.00 sec)

```

**SELECT**

> Comparison operator

```
mysql> select name from employee where salary > 25000;
+---------+
| name    |
+---------+
| Shree   |
| Krishna |
| Govind  |
+---------+
3 rows in set (0.00 sec)

```

> Logical operator

```
mysql> select * from employee where age >= 20 and salary > 2000;
+----+---------+-----+----------+
| id | name    | age | salary   |
+----+---------+-----+----------+
|  1 | Shree   |  20 |  25000.5 |
|  2 | Krishna |  21 | 50000.75 |
|  3 | Govind  |  23 |  75000.5 |
+----+---------+-----+----------+
3 rows in set (0.01 sec)

```

> Functions

```
mysql> select count(*) from employee where age > 20;
+----------+
| count(*) |
+----------+
|        3 |
+----------+
1 row in set (0.03 sec)

```

```
mysql> select avg(salary) from employee where age < 20;
+-------------+
| avg(salary) |
+-------------+
|      2500.5 |
+-------------+
1 row in set (0.00 sec)


```
> Set operators

*Again create another table employee2, this time in Oracle's SqlPlus*

```
create table employee( id integer primary key, name varchar(20) not null, age integer not null, salary float not null);
create table employee2( id integer primary key, name varchar(20) not null, age integer not null, salary float not null);

```

```
insert into employee values (1,'Shree',20,25000.50);
insert into employee values (2,'Krishna',21,50000.75);
insert into employee values (3,'Govind',23,75000.50);
insert into employee values (4,'Madhav',19,2500.50);
insert into employee values (5,'Kanha',21,700.25);

insert into employee2 values (1,'Murari',20,88000.00);
insert into employee2 values (2,'Manohar',21,60000.75);
insert into employee2 values (3,'Govind',23,75000.50);


```

```

SQL> select * from employee union select * from employee2;

	ID               NAME 		       AGE       SALARY
---------- -------------------- ---------- ----------
	 1              Murari			      20	     88000
	 1              Shree			        20       25000.5
	 2              Krishna			      21       50000.75
	 2              Manohar			      21       60000.75
	 3              Govind			      23       75000.5
	 4              Madhav			      19       2500.5
	 5              Kanha			        21       700.25

7 rows selected.

```

> psst: Copying clean table from Oracle's Sqlplus is a tough task


```
SQL> select * from employee intersect select * from employee2;

	ID                NAME 		       AGE     SALARY
---------- -------------------- ---------- ----------
	 3               Govind			       23    75000.5

```


**UPDATE**

```
SQL> update employee2 set age=21 where id=1;

1 row updated.

```

**DELETE**

```
SQL> delete from employee where salary < 2000;

1 row deleted.

```

> Arithmetic + Comparison operator

```
SQL> delete from employee where age+20 >= 40;

3 rows deleted.

```
