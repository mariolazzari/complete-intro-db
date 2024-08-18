# Complete intro to DataBase

## Terminology

- *Database*: repository of data of different types:
  - NoSQL
  - SQL
  - Grapg
  - Key/Value
- *Query*: request sent to Database
  - Create
  - Read
  - Update
  - Delete
- *Schema*: shape of data
  - SQL: strict 
  - NoSQL: schema-less
  *Transaction*: collection of operations treated as a single logical operation.
- *ACID*:
  - Atomicity: transactions cannot be divided (one atomic transaction)
  - Consistency: data must garantee consistency between them via referential integrity
  - Isoltation: cuncurrent transactions should not interfere with each others
  - Durability: changes made by a committed transaction must not be lost
- **:
   
## NoSQL

Databse that does not use SQL, aka non relational database.
- Schema less
- Dynamic scripting
- Collections intead of tables
- Documents instead of records
  
### MongoDB with Docker

```sh
docker run --name mongo -dit -p 27017:27017 --rm mongo
docker exec -it mongo mongosh
```

#### Show all databases

```sh
show dbs;
```

#### Create new database (group of collections)

If not present, *use* will create the new database and switch to it.

```sh
use adoptions;
```

#### Create new collection

*db* will indicate current database. 

*insertOne*: add one new record to collection. If collection does not exist, it will be created.

```js
db.pets.insertOne({name: "Luna", type:"dog", breed: "Havanese", age: 8})

// result
{
  acknowledged: true,
  insertedId: ObjectId('66c09a8f126d4237b491b588')
}
```

#### Count documents

```js
db.pets.count();
```

#### Help

```js
help
```

#### Database statistics

```js
db.stats();

// result
{
  db: 'adoptions',
  collections: Long('1'),
  views: Long('0'),
  objects: Long('1'),
  avgObjSize: 80,
  dataSize: 80,
  storageSize: 20480,
  indexes: Long('1'),
  indexSize: 20480,
  totalSize: 40960,
  scaleFactor: Long('1'),
  fsUsedSize: 9672499200,
  fsTotalSize: 62671097856,
  ok: 1
}
```

#### Find one document

```js
db.pets.findOne();

// result
{
  _id: ObjectId('66c09a8f126d4237b491b588'),
  name: 'Luna',
  type: 'dog',
  breed: 'Havanese',
  age: 8
}

// filtering by type dog
db.pets.find({type: "dog"})
[
  {
    _id: ObjectId('66c09a8f126d4237b491b588'),
    name: 'Luna',
    type: 'dog',
    breed: 'Havanese',
    age: 8
  }
]

// filtering by tyoe cat
db.pets.find({type: "dog"});
// empty

```

#### Find all documents: return a collection

```js
// find all dogs 
db.pets.find({type: "dog"});
[
  {
    _id: ObjectId('66c09a8f126d4237b491b588'),
    name: 'Luna',
    type: 'dog',
    breed: 'Havanese',
    age: 8
  }
]
```


```js
// bucket
db.pets.aggregate([
  {
    $bucket: {
      groupBy: "$age",
      boundaries: [0, 3, 9, 15],
      default: "16+",
      output: {
        count: { $sum: 1 }
      }
    }
  }
])
```

#### InsertMany

```js

// add 10.000 pets to collection
db.pets.insertMany(
  Array.from({ length: 10000 }).map((_, index) => ({
    name: [
      "Luna",
      "Fido",
      "Fluffy",
      "Carina",
      "Spot",
      "Beethoven",
      "Baxter",
      "Dug",
      "Zero",
      "Santa's Little Helper",
      "Snoopy",
    ][index % 9],
    type: ["dog", "cat", "bird", "reptile"][index % 4],
    age: (index % 18) + 1,
    breed: [
      "Havanese",
      "Bichon Frise",
      "Beagle",
      "Cockatoo",
      "African Gray",
      "Tabby",
      "Iguana",
    ][index % 7],
    index: index,
  }))
);
```

## SQL

### PostgreSQL with Docker

```sh
docker run --name=postgres -e POSTGRES_PASSWORD=password -p 5432:5432 -d --rm postgres
docker exec -it -u postgres postgres psql
```

## Key-Value

### Redis with Docker

```sh
docker run -dit --rm --name=redis -p 6379:6379 redis
docker exec -it redis redis-cli
```

## Graph


