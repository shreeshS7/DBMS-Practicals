
# P7

## Write a Stored Procedure namely proc_Grade for the categorization of student. If marks scored by students in examination is <=1500 and marks>=990 then student will be placed in distinction category if marks scored are between 989 and900 category is first class, if marks 899 and 825 category is Higher Second Class

## Write a PL/SQL block for using procedure created with above requirement.

- Stud_Marks(roll,name, total_marks)
- Result(rollno,Name, Class)

*Let's create both the tables*

```
SQL> create table stud_marks(
  2  rollno integer primary key,
  3  name varchar(20) not null,
  4  total_marks integer not null);

Table created.

```

```
insert into stud_marks values (1,'Shree',1500);
insert into stud_marks values (2,'Krishna',1000);
insert into stud_marks values (3,'Govind',920);
insert into stud_marks values (4,'Hari',850);
insert into stud_marks values (5,'Madhav',990);

```


```
SQL> create table result(
  2  roll integer references stud_marks,
  3  Name varchar(20) not null,
  4  class varchar(20) not null);

Table created.

```

> NOTE : Here we will use Cursor, Loop and if-else


```
declare
  c_roll stud_marks.rollno%type;
  c_name stud_marks.name%type;
  c_marks stud_marks.total_marks%type;
  cursor c_temp is select * from stud_marks;
begin
  open c_temp;
    loop
      fetch c_temp into c_roll,c_name,c_marks;
      exit when c_temp%notfound;
      if c_marks <= 1500 and c_marks>=990 then
        insert into result values(c_roll,c_name,'Distinction');
      elsif c_marks <= 989 and c_marks >= 900 then
        insert into result values(c_roll,c_name,'First Class');
      elsif c_marks <= 899 and c_marks >= 825 then
        insert into result values(c_roll,c_name,'Second Class');
      end if;
      dbms_output.put_line(c_roll ||' '|| c_name ||' '|| c_marks);
    end loop;
  close c_temp;
end;
/

```

> OUTPUT


```
1 Shree 1500
2 Krishna 1000
3 Govind 920
4 Hari 850
5 Madhav 990

PL/SQL procedure successfully completed.

```


```
SQL> select * from result;

      ROLL NAME 		CLASS
---------- -------------------- --------------------
	 1 Shree		Distinction
	 2 Krishna		Distinction
	 3 Govind		First Class
	 4 Hari 		Second Class
	 5 Madhav		Distinction

```
