# Complete intro to DataBase

## Terminology

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

´´´sh
docker run -dit --rm --name=redis -p 6379:6379 redis
docker exec -it redis redis-cli
```

## Graph


