
# P2

## Design and Develop MongoDB Queries using CRUD operations. (Use CRUD operations, SAVE method, logical operators)


For CRUD Operations refer [**Basic CRUD Operations**](https://shreeshs7.github.io/DBMS-Practicals/Group-B/P1/#basic-crud-operation) **From Practical 1**


*Let's create a collection (table) first, in case you don't have*

> db.createCollection('students');

> INSERT some Documents (rows)

```
> db.students.insert(
... [
... { name : 'Shree',
... roll : 3248,
... year : 'TE' },
...
... { name : 'Krishna',
... roll : 3249,
... year : 'TE' },
...
... { name : 'Govind',
... roll : 4202,
... year : 'BE' }
... ]
... );
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

**Save Method**

> save method replaces the whole document (row)


> db.COLLECTION_NAME.save({_id:ObjectId(),NEW_DATA})

*First let's find id for documents*

```
> db.students.find().pretty()
{
	"_id" : ObjectId("5f805507ace1fed098ac0b1f"),
	"name" : "Shree",
	"roll" : 3248,
	"year" : "TE"
}
{
	"_id" : ObjectId("5f805507ace1fed098ac0b20"),
	"name" : "Krishna",
	"roll" : 3249,
	"year" : "TE"
}
{
	"_id" : ObjectId("5f805507ace1fed098ac0b21"),
	"name" : "Govind",
	"roll" : 4202,
	"year" : "BE"
}

```

> Now copy id for 'Shree'

```
> db.students.save(
... {"_id" : ObjectId("5f805507ace1fed098ac0b1f"),
... name : 'Vishnu',
... roll : 3299,
... year : 'TE'}
... );
WriteResult({ "nMatched" : 1, "nUpserted" : 0, "nModified" : 1 })

```

```
> db.students.find().pretty();
{
	"_id" : ObjectId("5f805507ace1fed098ac0b1f"),
	"name" : "Vishnu",
	"roll" : 3299,
	"year" : "TE"
}
{
	"_id" : ObjectId("5f805507ace1fed098ac0b20"),
	"name" : "Krishna",
	"roll" : 3249,
	"year" : "TE"
}
{
	"_id" : ObjectId("5f805507ace1fed098ac0b21"),
	"name" : "Govind",
	"roll" : 4202,
	"year" : "BE"
}

```


**Logical Operators**

**AND**

> db.mycol.find(
	{
	$and: [{key1: value1}, {key2:value2}]
	}
	).pretty()


```
> db.students.find(
... {
... $and : [{name : 'Vishnu'}, {roll : 3299}]
... }
... ).pretty();

```

> OUTPUT


```
{
	"_id" : ObjectId("5f805507ace1fed098ac0b1f"),
	"name" : "Vishnu",
	"roll" : 3299,
	"year" : "TE"
}

```

> In MySQL:  select * from students where name='Vishnu' and roll=3299;


**OR**

>db . mycol . find (
	{
	$or : [
	{ key1 : value1 }, { key2 : value2 }
	]
	}
	). pretty ()


```
> db.students.find(
... {
... $or : [{roll : 3299}, {roll : 3249}]
... }
... ).pretty();

```

> OUTPUT

```
{
	"_id" : ObjectId("5f805507ace1fed098ac0b1f"),
	"name" : "Vishnu",
	"roll" : 3299,
	"year" : "TE"
}
{
	"_id" : ObjectId("5f805507ace1fed098ac0b20"),
	"name" : "Krishna",
	"roll" : 3249,
	"year" : "TE"
}

```
 > In MySQL :  select * from students where roll=3299 or roll=3249;
