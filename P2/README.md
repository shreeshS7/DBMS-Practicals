# P2

## Design and Develop SQL DDL statements which demonstrate the use of SQL objects such as Table, View, Index, Sequence, Synonym

### DDL

> Create, Alter, Drop

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
mysql> create table students( id integer primary key, name varchar(20), year integer);

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

```
mysql> alter view stud as select name,year from students;
Query OK, 0 rows affected (0.14 sec)

mysql> select * from stud;
+---------+------+
| name    | year |
+---------+------+
| Shree   |    3 |
| Krishna |    2 |
| Govind  |    4 |
| Madhav  |    1 |
+---------+------+
4 rows in set (0.00 sec)

```

**Drop View**

> drop view view_name;

```
mysql> drop view stud;
Query OK, 0 rows affected (0.11 sec)

```


# Index

**Create Index**

> create index index_name on table_name(column_name);

```
mysql> create index stud_index on students(name);
Query OK, 0 rows affected (0.97 sec)
Records: 0  Duplicates: 0  Warnings: 0

```

**Alter OR Drop**

> alter table table_name drop index index_name;

```
mysql> alter table students drop index stud_index;
Query OK, 0 rows affected (0.34 sec)
Records: 0  Duplicates: 0  Warnings: 0

```


# Sequence

**Create Sequence while creating a table**

```
mysql> create table user(
    -> id integer auto_increment,
    -> primary key(id),
    -> name varchar(20));
Query OK, 0 rows affected (0.92 sec)
```

**Alter previously created table**

```
mysql> alter table students modify id integer auto_increment;
Query OK, 4 rows affected (1.53 sec)
Records: 4  Duplicates: 0  Warnings: 0

```

**Drop Sequence**

*For dropping the sequence we just remove auto_increment constraint*

```
mysql> alter table students modify id integer;
Query OK, 4 rows affected (1.21 sec)
Records: 4  Duplicates: 0  Warnings: 0
```

# Synonym

*Here we will be using Oracle's Sqlplus since Mysql has no support for Synonym*

*Again we will create a table in sqlplus and insert some values*

```
Connected to:
Oracle Database 11g Express Edition Release 11.2.0.2.0 - 64bit Production

SQL> create table students( id integer primary key, name varchar(20), year integer);

Table created.

```

```
insert into students values (1,'Shree',3);
insert into students values (2,'Krishna',2);
insert into students values (3,'Govind',4);
insert into students values (4,'Madhav',1);
```

**Create Synonym**

> create synonym synonym_name for table_name;

```
SQL> create synonym stud_syn for students;

```

**Drop Synonym**

> drop synonym synonym_name;

```
SQL> drop synonym stud_syn;

```
