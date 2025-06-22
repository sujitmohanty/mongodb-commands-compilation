# 📘 MongoDB Commands Compilation

## Digital Library + User Management System

## 1️⃣ Database + Collection Setup

```mongodb
use libraryApp

db.createCollection("books")

db.createCollection("users")

db.createCollection("logs")


show collections

```

## 2️⃣ Insert Sample Data

```mongodb
db.books.insertMany([
  { title: "MongoDB Basics", author: "Jane Doe", tags: ["database", "nosql"], year: 2022, stock: 5 },
  { title: "Mastering NoSQL", author: "John Smith", tags: ["nosql"], year: 2021, stock: 3 },
  { title: "Data Science 101", author: "Jane Doe", tags: ["data", "science"], year: 2020, stock: 4 }
])


db.users.insertMany([
  { username: "librarian1", role: "librarian" },
  { username: "reader1", role: "reader" }
])

```

## 3️⃣ Create Indexes

```mongodb
db.books.createIndex({ title: 1 })

db.books.createIndex({ author: 1, year: -1 })

db.books.createIndex({ tags: 1 })

db.books.createIndex({ description: "text" })

db.books.getIndexes()

```

## 4️⃣ Create Users + Roles

```mongodb
use admin

db.createUser({
user: "siteAdmin",
pwd: "securePass",
roles: [{ role: "userAdminAnyDatabase", db: "admin" }]
})

db.auth("siteAdmin", "securePass")

use libraryApp

db.createUser({
user: "librarian",
pwd: "libPass",
roles: ["readWrite"]
})

db.createUser({
user: "reader",
pwd: "readPass",
roles: ["read"]
})

db.getUser("librarian")

```

## 5️⃣ CRUD Operations

```mongodb
db.books.updateOne({ title: "MongoDB Basics" }, { $set: { stock: 6 } })

db.books.updateOne({ title: "Mastering NoSQL" }, { $push: { tags: "advanced" } })

db.books.deleteOne({ title: "Data Science 101" })

db.books.find({ author: "Jane Doe" }).pretty()


db.books.find({ $or: [ { stock: { $lt: 5 } }, { tags: "advanced" } ] }).pretty()
```

## 6️⃣ Aggregation Queries

```mongodb
db.books.aggregate([
  { $group: { _id: "$author", totalBooks: { $sum: 1 } } }
])


db.books.aggregate([
  { $unwind: "$tags" },
  { $group: { _id: "$tags", count: { $sum: 1 } } }
])


db.books.aggregate([
  { $group: { _id: null, avgStock: { $avg: "$stock" } } }
])

```

## 7️⃣ Backup & Restore

```mongodb
# Backup
mongodump -u siteAdmin -p securePass --authenticationDatabase admin -d libraryApp -o

# Restore
mongorestore -u siteAdmin -p securePass --authenticationDatabase admin backups/
```

## 8️⃣ Performance / Profiling

```mongodb
db.setProfilingLevel(2)

db.books.find({ stock: { $gt: 4 } }).explain("executionStats")


db.system.profile.find().pretty()
```
