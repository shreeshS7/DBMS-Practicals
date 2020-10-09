
# P8

## Write a database trigger on Library table. The System should keep track of the records that are being updated or deleted. The old value of updated or deleted records should be added in Library_Audit table.

*Let's create a table first and insert some values*

```
SQL> create table books(
  2  id integer primary key,
  3  name varchar(10) not null,
  4  book varchar(5) not null,
  5  status varchar(2) not null);

Table created.

```

> INSERT some values

```
insert into books values (1,'Shree','CN','I');
insert into books values (2,'Krishna','DBMS','I');
insert into books values (3,'Hari','TOC','I');
insert into books values (4,'Govind','SEPM','I');

```

> Create Audit table
```
SQL> create table books_audit(
  2  id integer primary key,
  3  name varchar(10) not null,
  4  book varchar(5) not null,
  5  status varchar(2) not null);

Table created.

```

> And here comes the trigger

```
create or replace trigger backup
  before delete or update on books
for each row
  begin
    insert into books_audit values(:old.id,:old.name,:old.book,:old.status);
    dbms_output.put_line(:OLD.name);
  end;
/

```

> NOTE: Here trigger name is backup

> Output


**UPDATE**

```
SQL> update books set status='R' where id = 3;
Hari

1 row updated.

```

```
SQL> select * from books_audit;

	ID NAME       BOOK  ST
---------- ---------- ----- --
	 3 Hari       TOC   I

```

**DELETE**
```
SQL> delete from books where id=1;
Shree

1 row deleted.

```

> books_audit
```
SQL> select * from books_audit;

	ID NAME       BOOK  ST
---------- ---------- ----- --
	 3 Hari       TOC   I
	 1 Shree      CN    I

```

> books

```
SQL> select * from books;

	ID NAME       BOOK  ST
---------- ---------- ----- --
	 2 Krishna    DBMS  I
	 3 Hari       TOC   R
	 4 Govind     SEPM  I


```
