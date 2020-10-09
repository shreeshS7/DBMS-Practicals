
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
insert into oroll values(2,'Krishna','BE');
insert into oroll values(3,'Madhav','SE');
insert into oroll values(4,'Govind','TE');

```

```
SQL> create table nroll(
  2  roll integer primary key,
  3  name varchar(10) not null,
  4  year varchar(3) not null);

Table created.

```
> INSERT some values

```
insert into nroll values(1,'Shree','TE');
insert into nroll values(2,'Krishna','BE');

```

> Key Statement here is :

**select * from oroll minus select * from nroll;**

*OR*

**select * from oroll where roll not in(select roll from nroll);**


```
SQL> select * from oroll minus select * from nroll;

      ROLL NAME       YEA
---------- ---------- ---
	 3 Madhav     SE
	 4 Govind     TE

```

```
declare
  c_roll oroll.roll%type;
  c_name oroll.name%type;
  c_year oroll.year%type;
  cursor c_temp is select * from oroll minus select * from nroll;
begin
  open c_temp;
    loop
      fetch c_temp into c_roll,c_name,c_year;
      exit when c_temp%notfound;
      insert into nroll values(c_roll,c_name,c_year);
      dbms_output.put_line(c_roll ||' '|| c_name ||' '|| c_year);
    end loop;
  close c_temp;
end;
/

```

> Output

```
3 Madhav SE
4 Govind TE

PL/SQL procedure successfully completed.

```

```
SQL> select * from nroll;

      ROLL NAME       YEA
---------- ---------- ---
	 1 Shree      TE
	 2 Krishna    BE
	 3 Madhav     SE
	 4 Govind     TE

```
