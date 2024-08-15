# Complete intro to DataBase

## Terminology

## NoSQL

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

## Key-Value

## Graph


