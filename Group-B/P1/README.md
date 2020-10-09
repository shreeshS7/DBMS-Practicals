
# P1

## BASIC CRUD OPERATION

> Fire-up your terminal and type mongo (for Ubuntu)


> show dbs;     -- To check databases we have

```
> show dbs;
Shreesh  0.000GB
admin    0.000GB
config   0.000GB
local    0.000GB

```

**Create Database**

>  To create a Database in MongoDB is to use that Database

> use practical;

```
> use practical;
switched to db practical

```

**Drop Database**

> db.dropDatabase();

```
db.dropDatabase();
{ "ok" : 1 }

```

> NOTE: Here db refers to current database


## Collection (Table)

> Again create database practical because we previously dropped it.

**Create Collection**

> db.createCollection('Collection_name')

```
> db.createCollection('students')
{ "ok" : 1 }

```

```
> show collections;
students

```

> REMEMBER: db refers to current database which is 'practical' in our case

**Drop Collection**

> db.Collection_name.drop();

```
> db.students.drop();
true

```

**INSERT Document (Row) in Collection (Table)**

*Again create a students collection since we previously dropped it.*

> db.Collection_name.insert()  -- We insert in JSON format

```
> db.students.insert(
... { name : 'Shree',
... roll : 3248,
... year : 'TE'}
... );
WriteResult({ "nInserted" : 1 })

```

> For multiple Documents (rows)

```
> db.students.insert(
... [
... { name : 'Krishna',
... roll : 3249,
... year : 'TE'},
...
... { name : 'Govind',
... roll : 3250,
... year : 'TE'},
...
... { name : 'Madhav',
... roll : 4202,
... year : 'BE'}
... ]);


BulkWriteResult({
	"writeErrors" : [ ],
	"writeConcernErrors" : [ ],
	"nInserted" : 3,
	"nUpserted" : 0,
	"nMatched" : 0,
	"nModified" : 0,
	"nRemoved" : 0,
	"upserted" : [ ]
})

```


**SEARCH Document (Row) from Collection (Table)**

> db.Collection_name.find()

*OR*

> db.Collection_name,find().pretty()   -- outputs in JSON format

```
> db.students.find()
{ "_id" : ObjectId("5f8027cc7aa414c4cfcab291"), "name" : "Shree", "roll" : 3248, "year" : "TE" }
{ "_id" : ObjectId("5f8028d57aa414c4cfcab292"), "name" : "Krishna", "roll" : 3249, "year" : "TE" }
{ "_id" : ObjectId("5f8028d57aa414c4cfcab293"), "name" : "Govind", "roll" : 3250, "year" : "TE" }
{ "_id" : ObjectId("5f8028d57aa414c4cfcab294"), "name" : "Madhav", "roll" : 4202, "year" : "BE" }

```

```
> db.students.find().pretty()
{
	"_id" : ObjectId("5f8027cc7aa414c4cfcab291"),
	"name" : "Shree",
	"roll" : 3248,
	"year" : "TE"
}
{
	"_id" : ObjectId("5f8028d57aa414c4cfcab292"),
	"name" : "Krishna",
	"roll" : 3249,
	"year" : "TE"
}
{
	"_id" : ObjectId("5f8028d57aa414c4cfcab293"),
	"name" : "Govind",
	"roll" : 3250,
	"year" : "TE"
}
{
	"_id" : ObjectId("5f8028d57aa414c4cfcab294"),
	"name" : "Madhav",
	"roll" : 4202,
	"year" : "BE"
}

```

> I prefer using pretty() function.

*To find particular row*

> db.Collection_name.find({select});

```
> db.students.find({name : 'Krishna'}).pretty()
{
	"_id" : ObjectId("5f8028d57aa414c4cfcab292"),
	"name" : "Krishna",
	"roll" : 3249,
	"year" : "TE"
}

```

**UPDATE Document (Row) from Collection (Table)**

> db.Collection_name.update({select},{ $set : {update}});

```
> db.students.update(
... { name : 'Shree'},
... { $set : { 'year' : 'BE' }}
... );
WriteResult({ "nMatched" : 1, "nUpserted" : 0, "nModified" : 1 })

```

> In MySQL : update students set year='BE' where name='Shree';


```
> db.students.find({name : 'Shree'}).pretty()
{
	"_id" : ObjectId("5f8027cc7aa414c4cfcab291"),
	"name" : "Shree",
	"roll" : 3248,
	"year" : "BE"
}

```

**DELETE Document (Row) from Collection (Table)**

> db.Collection_name.remove({select})

```
> db.students.remove({ name : 'Shree' });
WriteResult({ "nRemoved" : 1 })

```

```
{
	"_id" : ObjectId("5f8028d57aa414c4cfcab292"),
	"name" : "Krishna",
	"roll" : 3249,
	"year" : "TE"
}
{
	"_id" : ObjectId("5f8028d57aa414c4cfcab293"),
	"name" : "Govind",
	"roll" : 3250,
	"year" : "TE"
}
{
	"_id" : ObjectId("5f8028d57aa414c4cfcab294"),
	"name" : "Madhav",
	"roll" : 4202,
	"year" : "BE"
}

```


**Truncate Collection (Table)**

> db.students,remove({})

```
> db.students.remove({})
WriteResult({ "nRemoved" : 3 })

```
