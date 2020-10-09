
# P6

## Write a PL/SQL block of code using parameterized Cursor, that will merge the data available in the newly created table N_RollCall with the data available in the table O_RollCall. If the data in the first table already exist in the second table then that data should be skipped.

### Cursor

*Let's create a table first and insert some values*

```
SQL> create table oroll(
  2  roll integer primary key,
  3  name varchar(10) not null,
  4  year varchar(3) not null);

Table created.
```

> INSERT some values

```
insert into oroll values(1,'Shree','TE');
insert into oroll values(1,'Shree','TE');
insert into oroll values(1,'Shree','TE');
insert into oroll values(1,'Shree','TE');

```

```
SQL> create table nroll(
  2  roll integer primary key,
  3  name varchar(10) not null,
  4  year varchar(3) not null);

Table created.

```

```
insert into oroll values(1,'Shree','TE');
insert into oroll values(1,'Shree','TE');
insert into oroll values(1,'Shree','TE');

```
