
# P5

## Unnamed PL/SQL code block: Use of Control structure and Exception handling is mandatory.

## Write a PL/SQL block of code for the following requirements:-

**Schema:**

1. Borrower(Rollin, Name, DateofIssue, NameofBook, Status)
2. Fine(Roll_no,Date,Amt)

- *Accept roll_no & name of book from user.*
- *Check the number of days (from date of issue), if days are between 15 to 30 then fine amount will be Rs 5per day.*
- *If no. of days>30, per day fine will be Rs 50 per day & for days less than 30, Rs. 5 per day.*
- *After submitting the book, status will change from I to R.*
- *If condition of fine is true, then details will be stored into fine table.*

*Let's create tables, again we will be using Oracle's SqlPlus*

> psst: Mysql doesn't support PL/SQL

```
SQL> create table Borrower(
  2  rollin integer,
  3  name varchar(20) not null,
  4  dateofissue date not null,
  5  nameofbook varchar(20) not null,
  6  status varchar(2) default 'I');

Table created.
```

> NOTE: You can refer Borrower table as borrower in Oracle's SqlPlus

```
insert into Borrower values (1,'Shree',TO_DATE('08/09/2020','dd/mm/yyyy'),'CN','I');
insert into Borrower values (2,'Krishna',TO_DATE('20/09/2020','dd/mm/yyyy'),'DBMS','I');
insert into Borrower values (3,'Madhav',TO_DATE('25/10/2020','dd/mm/yyyy'),'ISEE','I');
insert into Borrower values (4,'Mukund',TO_DATE('03/10/2020','dd/mm/yyyy'),'SEPM','I');
insert into Borrower values (5,'Mohan',TO_DATE('27/10/2020','dd/mm/yyyy'),'TOC','I');
insert into Borrower values (1,'Shree',TO_DATE('25/09/2020','dd/mm/yyyy'),'TOC','I');

```

```
SQL> create table fine(
  2  rollno integer,
  3  fine_date date not null,
  4  amt float not null);

Table created.

```

> NOTE: 1-14 : 0 Rs.  15-30: 5 Rs/day.   >30: 50 Rs/day.

```
create or replace procedure finer(r in number, book_name in varchar) as days number;
begin
  select to_number(trunc(sysdate-dateofissue)) into days from Borrower where rollin=r and nameofbook=book_name;
  if days < 15 then
    insert into Fine values (r,sysdate,0);
  elsif days > 15 and days < 30 then
    insert into Fine values (r,sysdate,0);
    update fine set amt = amt + (days*5) where rollno=r;
  else
    days := days-30;
    insert into Fine values (r,sysdate,0);
    update fine set amt = amt + (days*50)+75 where rollno=r;
  end if;
  update borrower set status='R' where rollin=r and nameofbook=book_name;
end;
/
```


> NOTE: sysdate is an inbuilt-function which gives you current date of your system


```
SQL> execute finer(1,'CN');
SQL> execute finer(1,'TOC');
SQL> execute finer(2,'DBMS');

PL/SQL procedure successfully completed.
```

```
SQL> select * from fine;

    ROLLNO FINE_DATE	    AMT
---------- --------- ----------
	 1 08-OCT-20	     75
	 1 08-OCT-20	      0
	 2 08-OCT-20	     90

```

```
SQL> select * from borrower;

    ROLLIN NAME 		DATEOFISS NAMEOFBOOK	       ST
---------- -------------------- --------- -------------------- --
	 1 Shree		08-SEP-20 CN		       R
	 2 Krishna		20-SEP-20 DBMS		       R
	 3 Madhav		25-OCT-20 ISEE		       I
	 4 Mukund		03-OCT-20 SEPM		       I
	 5 Mohan		27-OCT-20 TOC		       I
	 1 Shree		25-SEP-20 TOC		       R

6 rows selected.

```
