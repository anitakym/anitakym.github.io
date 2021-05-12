---
title: database开源学习之complete-intro-to-databases
date: 2021-04-12 20:37:54
tags:
---
## 网站指路
https://btholt.github.io/complete-intro-to-databases/
(这种开源资源，可以过一遍之后，当成search的参考资料来用)
## Welcome
1. Introduction
2. Installation Notes
3. Terminology
## NoSQL
1. NoSQL
mongodb是基于文档对象模型的，曾经有段时间因为丢数据的问题，饱受争议，但是现在是相对稳定的啦
2. MongoDB
```
docker run --name test-mongo -dit -p 27017:27017 --rm mongo:4.4.1
docker exec -it test-mongo mongo

show dbs
use adoption
db.pets.insertOne({name: "Luna", type: "dog", breed: "Havanese", age: 8})
db.pets.help()
db.pets.findOne()
db.pets.count()
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

3. Querying MongoDB
mongodb compass,左下角，点击 _MONGOSH BETA 也能进入shell模式
<pre>
$gt - greater than
$gte - greater than or equal to
$lt - less than
$lte - less than or equal to
$eq - equals (usually not necessary)
$ne - not equals
$in - has the value in the array (MongoDB can store arrays and objects too!)
$nin - does not have the value in the array
</pre>
```
# findone
db.pets.findOne()
db.pets.findOne({ index: 1337 });
# find
db.pets.find({ type: "dog" });
it
it
# count , limit , and toArray
db.pets.count({ type: "dog" }); // probably pretty big number
db.pets.find({ type: "dog" }).limit(40);
it; // after this the cursor will end
db.pets.find({ type: "dog" }).limit(40).toArray();
# query operators
db.pets.count({ type: "cat", age: { $gt: 12 } });
db.pets.find({
  type: { $ne: "dog" },
  name: "Fido",
});
# logical operators
db.pets.find({
  type: "bird",
  $and: [{ age: { $gte: 4 } }, { age: { $lte: 8 } }],
});
# special operators , like $type $exists
# sorts 1:ascending -1: descending
db.pets.find({ type: "dog" }).sort({ age: -1 });
# projections
db.pets.find({ type: "dog" }, { name: 1, breed: 1 });
db.pets.find({ type: "dog" }, { name: 1, breed: 1, _id: 0 });
db.pets.find({ type: "dog" }, { name: true, breed: true, _id: false }); // note that true and false work too
db.pets.find({ type: "dog" }, { _id: 0 });
```

4. Updating MongoDB
- insert,insertOne,insertMany
- delete deleteMany deleteOne / update updateMany/updateOne

5. Indexes in MongoDB
6. Aggregation
7. Write a Node.js app with MongoDB
8. MongoDB Ops

## SQL
1. Intro to SQL Database
2. PostgreSQL
3. Querying PostgreSQL
4. Complex SQL Queries
5. JSON in PostgreSQL
6. Indexes in PostgreSQL
7. Node.js App with PostgreSQL
8. Hasura
9. PostgreSQL Ops

## Graph
1. Graph Databases
2. 12Neo4j
3. Neo4j Browser
4. Complex Neo4j Queries
5. Indexes in Neo4j
6. Node.js App with Neo4j
7. Neo4j Ops
## Key-Value Store
1. Key-Value Store
2. Redis
3. Redis Command Options
4. Redis Data Types
5. More Redis Concepts
6. Node.js App with Redis
7. Redis Ops
## Conclusion
1. Conclusion