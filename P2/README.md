# P2

## Design and Develop SQL DDL statements which demonstrate the use of SQL objects such as Table, View, Index, Sequence, Synonym

### DDL

> Create, Alter, Delete

# Table

**Create Table**

> create table table_name();

```
mysql> create table students(
    -> id integer primary key,
    -> name varchar(20),
    -> year integer);
Query OK, 0 rows affected (0.64 sec)

```

> Table Description

```
mysql> desc students;
+-------+-------------+------+-----+---------+-------+
| Field | Type        | Null | Key | Default | Extra |
+-------+-------------+------+-----+---------+-------+
| id    | int         | NO   | PRI | NULL    |       |
| name  | varchar(20) | YES  |     | NULL    |       |
| year  | int         | YES  |     | NULL    |       |
+-------+-------------+------+-----+---------+-------+
3 rows in set (0.01 sec)

```


**Alter Table**

> alter table table_name add/modify/drop column constraints;

```
mysql> alter table students add pointer float;
Query OK, 0 rows affected (0.63 sec)
Records: 0  Duplicates: 0  Warnings: 0

```

```
mysql> desc students;
+---------+-------------+------+-----+---------+-------+
| Field   | Type        | Null | Key | Default | Extra |
+---------+-------------+------+-----+---------+-------+
| id      | int         | NO   | PRI | NULL    |       |
| name    | varchar(20) | YES  |     | NULL    |       |
| year    | int         | YES  |     | NULL    |       |
| pointer | float       | YES  |     | NULL    |       |
+---------+-------------+------+-----+---------+-------+
4 rows in set (0.01 sec)
```

**Drop Table**

> drop table table_name;  

```
mysql> drop table students;
Query OK, 0 rows affected (0.46 sec)
```


# View

*Again create students table, insert some values and use it for view*

```
mysql> create table students(
    -> id integer primary key,
    -> name varchar(20),
    -> year integer);
Query OK, 0 rows affected (0.64 sec)
```

```
insert into students values (1,'Shree',3);
insert into students values (2,'Krishna',2);
insert into students values (3,'Govind',4);
insert into students values (4,'Madhav',1);
```

```
mysql> select * from students;
+----+---------+------+
| id | name    | year |
+----+---------+------+
|  1 | Shree   |    3 |
|  2 | Krishna |    2 |
|  3 | Govind  |    4 |
|  4 | Madhav  |    1 |
+----+---------+------+
4 rows in set (0.00 sec)

```

**Create View**

> create view view_name as select * from table_name;

```
mysql> create view stud as select id,name from students;
Query OK, 0 rows affected (0.75 sec)

mysql> select * from stud;
+----+---------+
| id | name    |
+----+---------+
|  1 | Shree   |
|  2 | Krishna |
|  3 | Govind  |
|  4 | Madhav  |
+----+---------+
4 rows in set (0.00 sec)

```


**Alter View**

> alter view view_name as select something from table;
