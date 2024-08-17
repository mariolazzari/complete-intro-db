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

### MongoDB with Docker

```sh
docker run --name mongo -dit -p 27017:27017 --rm mongo
docker exec -it mongo mongosh
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


