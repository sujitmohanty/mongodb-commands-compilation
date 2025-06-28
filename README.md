# 📘 MongoDB Commands Compilation

## Digital Library + User Management System

---

## 1️⃣ Database + Collection Setup

```mongodb
use libraryApp

db.createCollection("books")
db.createCollection("users")
db.createCollection("logs")

show collections
```

---

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

---

## 3️⃣ Create Indexes

```mongodb
db.books.createIndex({ title: 1 })
db.books.createIndex({ author: 1, year: -1 })
db.books.createIndex({ tags: 1 })
db.books.createIndex({ description: "text" })
db.books.getIndexes()
```

---

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

---

## 5️⃣ CRUD Operations

```mongodb
db.books.updateOne({ title: "MongoDB Basics" }, { $set: { stock: 6 } })
db.books.updateOne({ title: "Mastering NoSQL" }, { $push: { tags: "advanced" } })
db.books.updateMany({ stock: { $lt: 5 } }, { $set: { status: "low-stock" } })
db.books.deleteOne({ title: "Data Science 101" })
db.books.find({ author: "Jane Doe" }).pretty()
db.books.find({ $or: [ { stock: { $lt: 5 } }, { tags: "advanced" } ] }).pretty()

// Unset a field
db.books.updateOne({ title: "MongoDB Basics" }, { $unset: { stock: "" } })

// Rename a field
db.books.updateOne({ title: "Advanced NoSQL" }, { $rename: { year: "published" } })

// Add current date
db.books.updateOne({ title: "Advanced NoSQL" }, { $currentDate: { lastModified: true } })

// $each with $push
db.books.updateOne(
  { title: "Advanced NoSQL" },
  { $push: { tags: { $each: ["backend", "distributed"] } } }
)
```

---

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

---

## 7️⃣ Backup & Restore

```bash
mongodump -u siteAdmin -p securePass --authenticationDatabase admin -d libraryApp -o ./backups
mongorestore -u siteAdmin -p securePass --authenticationDatabase admin backups/
```

---

## 8️⃣ Advanced User & Role Management

```mongodb
db.grantRolesToUser("reader", [ { role: "readWrite", db: "libraryApp" } ])
db.getUser("reader")
db.revokeRolesFromUser("reader", [ { role: "readWrite", db: "libraryApp" } ])
db.changeUserPassword("reader", "newSecurePass")
db.getRole("read", { showPrivileges: true })
```

---

## 9️⃣ Advanced Indexes

```mongodb
db.books.createIndex({ title: 1 }, { unique: true })
db.books.createIndex({ optionalField: 1 }, { sparse: true })
db.logs.createIndex({ createdAt: 1 }, { expireAfterSeconds: 3600 })
db.books.createIndex({ author: 1, year: -1 })
db.books.createIndex(
  { title: "text", description: "text" },
  { weights: { title: 10, description: 2 } }
)
db.books.createIndex({ year: 1 }, { background: true })
db.books.createIndex({ description: "text" }, { default_language: "english", language_override: "lang" })
```

---

## 🔟 Advanced Backup & Restore

```bash
mongodump -u siteAdmin -p securePass --authenticationDatabase admin -d libraryApp --out ./library-dump --dumpDbUsersAndRoles
mongorestore -u siteAdmin -p securePass --authenticationDatabase admin --drop ./library-dump/libraryApp
mongodump -u siteAdmin -p securePass --authenticationDatabase admin -d libraryApp -c books -q '{"year": {"$gt": 2020}}' --out ./selective-dump
mongodump --repair
mongorestore -u siteAdmin -p securePass --authenticationDatabase admin --filter '{"year": {"$gt": 2020}}' ./selective-dump
mongorestore -u siteAdmin -p securePass --authenticationDatabase admin --noIndexRestore ./library-dump/libraryApp
```

---

## 1️⃣1️⃣ Profiling

```mongodb
db.setProfilingLevel(1, { slowms: 100 })
db.setProfilingLevel(2)
db.books.find({ stock: { $gt: 5 } })
db.system.profile.find().pretty()
```

---

## 1️⃣2️⃣ Query Enhancements

```mongodb
db.books.find().limit(3).skip(2)
db.books.find({}, { title: 1, _id: 0 })
db.books.find({}, { title: 1, _id: 0 }).sort({ title: -1 })
db.books.find({}, { title: 1, year: 1 }).sort({ title: 1, year: -1 })
db.books.find({ author: "Jane Doe" }, { title: 1, _id: 0 })
```

---

## 1️⃣3️⃣ Extra Data Modeling, Special Queries, Utilities

```mongodb
// Capped collection
use libraryApp
db.createCollection("logsCapped", { capped: true, size: 6142800, max: 10000 })
db.logsCapped.drop()

// findOneAndReplace
db.books.findOneAndReplace(
  { title: "MongoDB Basics" },
  { title: "MongoDB Basics Revised", author: "Jane Doe", tags: ["database"], year: 2022, stock: 6 }
)

// replaceOne
db.books.replaceOne(
  { title: "Mastering NoSQL" },
  { title: "Advanced NoSQL", author: "John Smith", tags: ["nosql", "advanced"], year: 2021, stock: 5 }
)

// Regex-based queries
db.users.insertOne({ username: "reader2", role: "reader", phone: "0701234567" })
db.users.find({ phone: /070/ })
db.users.find({ phone: /070$/ })
db.users.find({ phone: /123/ })
db.users.find({ phone: /70(.*)67$/ })

// User with roles on multiple DBs
db.createUser({
  user: "multiDBUser",
  pwd: "multiPass",
  roles: [
    { role: "read", db: "libraryApp" },
    { role: "read", db: "logsDB" }
  ]
})
```

---

## 📝 Example Document with Data Types

```mongodb
db.samples.insertOne({
  name: "Example",
  age: 30,
  isActive: true,
  rating: 4.5,
  createdAt: new Date(),
  tags: ["demo", "test"],
  address: { city: "Hof", zip: "95028" },
  binaryData: new BinData(0, "SGVsbG8gd29ybGQ="),
  note: /test/i
})
```

---

## 📝 Shell Login Example

```bash
mongo -u siteAdmin -p securePass --authenticationDatabase admin
```

## 📝 Phonebook App

```javascript
function populatePhonebook(areaCode, quantity) {
  for (var i = 0; i < quantity; i++) {
    var phoneNumberLength = 3 + ((Math.random() * 6) << 0);
    var phoneNumber =
      1 + ((Math.random() * Math.pow(10, phoneNumberLength)) << 0);
    phoneNumberLength = 1 + Math.floor(Math.log(phoneNumber) / Math.log(10));
    if (phoneNumberLength < 3) continue;

    var num = areaCode * Math.pow(10, phoneNumberLength) + phoneNumber;

    db.phones.insertOne({
      _id: num,
      components: {
        areaCode: areaCode,
        phoneNumber: phoneNumber,
      },
      display: areaCode + "/" + phoneNumber,
    });
  }
}
```

```javascript
load("phonebook.js");
populatePhonebook(9281, 10);
db.phones.find().pretty();
```

### Phone search queries

```mongodb
db.phones.createIndex({ display: 1 }, { unique: true })
db.phones.find({ display: /070/ })
db.phones.find({ display: /070$/ })
db.phones.find({ display: /\/201/ })
db.phones.find({ display: /\/[246]00/ })
db.phones.find({ display: /\/20(.*)13$/ })
```
