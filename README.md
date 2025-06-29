# 📘 MongoDB Commands Compilation

## 1. 📦 Installation and Setup

1. `sudo systemctl start mongod`  
   _Start the MongoDB service_
2. `sudo systemctl stop mongod`  
   _Stop the MongoDB service_
3. `sudo systemctl status mongod`  
   _Check MongoDB service status_
4. `sudo systemctl restart mongod`  
   _Restart the MongoDB service_
5. `sudo systemctl enable mongod`  
   _Enable MongoDB to start on boot_

## 2. 🗃️ Database Operations (DDL)

6. `use DATABASE_NAME`  
   _Select or create a new database_
7. `db`  
   _Show the current database_
8. `show dbs`  
   _List all databases_
9. `db.dropDatabase()`  
   _Drop the current database_

## 3. 📂 Collection Operations

10. `db.createCollection("mycol", { capped: true, size: 6142800, max: 10000 })`  
    _Create a capped collection_
11. `db.COLLECTION_NAME.drop()`  
    _Drop a collection_

## 4. 🧾 Insert Documents (DML)

12. `db.COLLECTION_NAME.insertOne(document)`  
    _Insert a single document_
13. `db.COLLECTION_NAME.insertMany([doc1, doc2, ...])`  
    _Insert multiple documents_
14. `db.COLLECTION_NAME.replaceOne(filter, document)`  
    _Replace a document completely_

## 5. 🔍 Query Documents

15. `db.COLLECTION_NAME.find()`  
    _Find all documents_
16. `db.COLLECTION_NAME.find().pretty()`  
    _Find and pretty print output_
17. `db.COLLECTION_NAME.find({key: value})`  
    _Find documents matching a key_
18. `db.COLLECTION_NAME.find({key: {$lt: value}})`  
    _Less than condition_
19. `db.COLLECTION_NAME.find({key: {$lte: value}})`  
    _Less than or equal_
20. `db.COLLECTION_NAME.find({key: {$gt: value}})`  
    _Greater than condition_
21. `db.COLLECTION_NAME.find({key: {$gte: value}})`  
    _Greater than or equal_
22. `db.COLLECTION_NAME.find({key: {$ne: value}})`  
    _Not equal condition_
23. `db.COLLECTION_NAME.find({key1: val1, key2: val2})`  
    _AND condition_
24. `db.COLLECTION_NAME.find({$or: [{key1: val1}, {key2: val2}]})`  
    _OR condition_
25. `db.COLLECTION_NAME.find({}, {field1: 1, field2: 1, _id: 0})`  
    _Projection query_
26. `db.COLLECTION_NAME.find().limit(N)`  
    _Limit results_
27. `db.COLLECTION_NAME.find().skip(N)`  
    _Skip first N documents_
28. `db.COLLECTION_NAME.find().sort({field: 1})`  
    _Sort ascending (1), descending (-1)_

## 6. ✏️ Update Documents

29. `db.COLLECTION_NAME.update(query, updateObj)`  
    _Update single document (Mongo v3)_
30. `db.COLLECTION_NAME.update(query, updateObj, {multi: true})`  
    _Update multiple documents (Mongo v3)_
31. `db.COLLECTION_NAME.updateOne(query, updateObj)`  
    _Update one (Mongo v6)_
32. `db.COLLECTION_NAME.updateMany(query, updateObj)`  
    _Update many (Mongo v6)_
33. `db.COLLECTION_NAME.findOneAndUpdate(filter, update)`  
    _Update one and return pre-update doc_

## 7. 🔁 Replace Documents

34. `db.COLLECTION_NAME.findOneAndReplace(filter, replacement)`  
    _Replace a document_

## 8. ❌ Delete Documents

35. `db.COLLECTION_NAME.deleteOne(filter)`  
    _Delete one document_
36. `db.COLLECTION_NAME.deleteMany(filter)`  
    _Delete multiple documents_

## 9. 🔐 User & Role Management

37. `db.createUser({...})`  
    _Create a new user with roles_
38. `mongo -u username -p password database`  
    _Authenticate as user_
39. `db.getUser("username")`  
    _View user info_
40. `db.getRole("role", {showPrivileges:true})`  
    _View role privileges_
41. `db.grantRolesToUser("user", [{role: "role", db: "db"}])`  
    _Grant a role to a user_
42. `db.revokeRolesFromUser("user", [{role: "role", db: "db"}])`  
    _Revoke role from user_
43. `db.changeUserPassword("username", "newPassword")`  
    _Change user password_

## 10. 📑 Indexes

44. `db.COLLECTION_NAME.ensureIndex({field: 1})`  
    _Create ascending index (deprecated)_
45. `db.COLLECTION_NAME.createIndex({field: 1}, {options})`  
    _Create index with options_
46. `db.COLLECTION_NAME.getIndexes()`  
    _List all indexes_

## 11. 🔎 Explain Plan & Profiling

47. `db.COLLECTION_NAME.find(query).explain("executionStats")`  
    _Analyze query performance_
48. `db.setProfilingLevel(2)`  
    _Enable full profiling_
49. `db.system.profile.find()`  
    _Read profiling results_

## 12. 📜 Text Search with Regex (Phonebook Examples)

50. `db.phones.find({display:/070/})`  
    _Contains sequence_
51. `db.phones.find({display:/070$/})`  
    _Ends with sequence_
52. `db.phones.find({display:/^070/})`  
    _Starts with sequence_
53. `db.phones.find({display:/\/[246]00/})`  
    _Starts with digit sets_
54. `db.phones.find({display:/\/20(.*)13$/})`  
    _Start and end pattern_

## 13. 📤 Backup & Restore

55. `mongodump --db mydb --collection mycol --out path`  
    _Backup a collection_
56. `mongorestore --db mydb --collection mycol path`  
    _Restore from backup_
57. `mongodump [options]`  
    _General format for backup_
58. `mongorestore [options]`  
    _General format for restore_

---

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

---

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

```mongodb
use libraryApp
```
