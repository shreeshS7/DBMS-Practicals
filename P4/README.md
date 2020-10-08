
# P4

## Design at least 10 SQL queries for suitable database application using SQL DML statements: all types of Join, Sub-Query and View.


*We will first create two tables and insert some values*

```
mysql> create table customer(
    -> id integer primary key,
    -> name varchar(20) not null,
    -> salary float not null);
Query OK, 0 rows affected (0.61 sec)

```

```
insert into customer values (1,'Shree',25000);
insert into customer values (2,'Krishna',50000.75);
insert into customer values (3,'Govind',33000);
insert into customer values (4,'Madhav',82000);
insert into customer values (5,'Murari',10000);
```
```
mysql> select * from customer;
+----+---------+---------+
| id | name    | salary  |
+----+---------+---------+
|  1 | Shree   |   25000 |
|  2 | Krishna | 50000.8 |
|  3 | Govind  |   33000 |
|  4 | Madhav  |   82000 |
|  5 | Murari  |   10000 |
+----+---------+---------+
5 rows in set (0.00 sec)

```

```
mysql> create table orders(
    -> order_id integer primary key,
    -> customer_id integer references customer,
    -> amount integer not null);
Query OK, 0 rows affected (0.72 sec)

```

```
insert into orders values (1,2,200);
insert into orders values (2,2,1200);
insert into orders values (3,3,2300);
insert into orders values (4,4,2100);
insert into orders values (5,1,100);

```

```
mysql> select * from orders;
+----------+-------------+--------+
| order_id | customer_id | amount |
+----------+-------------+--------+
|        1 |           2 |    200 |
|        2 |           2 |   1200 |
|        3 |           3 |   2300 |
|        4 |           4 |   2100 |
|        5 |           1 |    100 |
+----------+-------------+--------+
5 rows in set (0.00 sec)

```

**JOIN**

> INNER JOIN

```
mysql> select name,salary,amount from customer inner join orders on customer.id = orders.customer_id;
+---------+---------+--------+
| name    | salary  | amount |
+---------+---------+--------+
| Krishna | 50000.8 |    200 |
| Krishna | 50000.8 |   1200 |
| Govind  |   33000 |   2300 |
| Madhav  |   82000 |   2100 |
| Shree   |   25000 |    100 |
+---------+---------+--------+
5 rows in set (0.00 sec)

```

> LEFT JOIN

```
mysql> select name,salary,amount from customer left join orders on customer.id = orders.customer_id;
+---------+---------+--------+
| name    | salary  | amount |
+---------+---------+--------+
| Shree   |   25000 |    100 |
| Krishna | 50000.8 |   1200 |
| Krishna | 50000.8 |    200 |
| Govind  |   33000 |   2300 |
| Madhav  |   82000 |   2100 |
| Murari  |   10000 |   NULL |
+---------+---------+--------+
6 rows in set (0.01 sec)

```

> RIGHT JOIN

```
mysql> select name,salary,amount from customer right join orders on customer.id = orders.customer_id;
+---------+---------+--------+
| name    | salary  | amount |
+---------+---------+--------+
| Krishna | 50000.8 |    200 |
| Krishna | 50000.8 |   1200 |
| Govind  |   33000 |   2300 |
| Madhav  |   82000 |   2100 |
| Shree   |   25000 |    100 |
+---------+---------+--------+
5 rows in set (0.00 sec)

```

> FULL JOIN

```
mysql> select name,salary,amount from customer full join orders on id = orders.customer_id;
+---------+---------+--------+
| name    | salary  | amount |
+---------+---------+--------+
| Krishna | 50000.8 |    200 |
| Krishna | 50000.8 |   1200 |
| Govind  |   33000 |   2300 |
| Madhav  |   82000 |   2100 |
| Shree   |   25000 |    100 |
+---------+---------+--------+
5 rows in set (0.00 sec)

```

> SELF JOIN

```
mysql> select a.id,b.name,a.salary from customer a, customer b where a.salary > b.salary;
+----+---------+---------+
| id | name    | salary  |
+----+---------+---------+
|  4 | Shree   |   82000 |
|  3 | Shree   |   33000 |
|  2 | Shree   | 50000.8 |
|  4 | Krishna |   82000 |
|  4 | Govind  |   82000 |
|  2 | Govind  | 50000.8 |
|  4 | Murari  |   82000 |
|  3 | Murari  |   33000 |
|  2 | Murari  | 50000.8 |
|  1 | Murari  |   25000 |
+----+---------+---------+
10 rows in set (0.01 sec)

```

> CARTESIAN OR CROSS JOIN

```
mysql> select id,name,amount from customer,orders;
+----+---------+--------+
| id | name    | amount |
+----+---------+--------+
|  5 | Murari  |    200 |
|  4 | Madhav  |    200 |
|  3 | Govind  |    200 |
|  2 | Krishna |    200 |
|  1 | Shree   |    200 |
|  5 | Murari  |   1200 |
|  4 | Madhav  |   1200 |
|  3 | Govind  |   1200 |
|  2 | Krishna |   1200 |
|  1 | Shree   |   1200 |
|  5 | Murari  |   2300 |
|  4 | Madhav  |   2300 |
|  3 | Govind  |   2300 |
|  2 | Krishna |   2300 |
|  1 | Shree   |   2300 |
|  5 | Murari  |   2100 |
|  4 | Madhav  |   2100 |
|  3 | Govind  |   2100 |
|  2 | Krishna |   2100 |
|  1 | Shree   |   2100 |
|  5 | Murari  |    100 |
|  4 | Madhav  |    100 |
|  3 | Govind  |    100 |
|  2 | Krishna |    100 |
|  1 | Shree   |    100 |
+----+---------+--------+
25 rows in set (0.00 sec)

```

**SUB-QUERY**

> SELECT

```
mysql> select name from customer where id in (select customer_id from orders);
+---------+
| name    |
+---------+
| Krishna |
| Govind  |
| Madhav  |
| Shree   |
+---------+
4 rows in set (0.00 sec)

```

> UPDATE

```
mysql> update customer set salary=salary+1000 where id in (select customer_id from orders);
Query OK, 4 rows affected (0.21 sec)
Rows matched: 4  Changed: 4  Warnings: 0

```
**VIEW**

[**View**](https://shreeshs7.github.io/DBMS-Practicals/P2)

*Refer view from Practical-2*
