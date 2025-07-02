# 📘 MongoDB Commands Compilation

0. Importing a CSV

```bash
.\mongoimport --db testDB --collection customers --type csv --headerline --file "D:\Users\Sujit\Downloads\test.csv"
```

1. Start MongoDB service

```bash
sudo systemctl start mongod
```

2. Stop MongoDB service

```bash
sudo systemctl stop mongod
```

3. Check MongoDB service status

```bash
sudo systemctl status mongod
```

4. Restart MongoDB service

```bash
sudo systemctl restart mongod
```

5. Enable MongoDB on boot

```bash
sudo systemctl enable mongod
```

6. Select or create database

```mongodb
use DATABASE_NAME
```

7. Show current database

```mongodb
db
```

8. List all databases

```mongodb
show dbs
```

9. Drop current database

```mongodb
db.dropDatabase()
```

10. Create capped collection

```mongodb
db.createCollection("mycol", { capped: true, size: 6142800, max: 10000 })
```

11. Drop collection

```mongodb
db.COLLECTION_NAME.drop()
```

12. Insert one document

```mongodb
db.COLLECTION_NAME.insertOne(document)
```

13. Insert many documents

```mongodb
db.COLLECTION_NAME.insertMany([doc1, doc2, ...])
```

14. Replace document

```mongodb
db.COLLECTION_NAME.replaceOne(filter, document)
```

15. Find all documents

```mongodb
db.COLLECTION_NAME.find()
```

16. Pretty print find result

```mongodb
db.COLLECTION_NAME.find().pretty()
```

17. Find with condition

```mongodb
db.COLLECTION_NAME.find({key: value})
```

18. Find less than

```mongodb
db.COLLECTION_NAME.find({key: {$lt: value}})
```

19. Find less than or equal

```mongodb
db.COLLECTION_NAME.find({key: {$lte: value}})
```

20. Find greater than

```mongodb
db.COLLECTION_NAME.find({key: {$gt: value}})
```

21. Find greater than or equal

```mongodb
db.COLLECTION_NAME.find({key: {$gte: value}})
```

22. Find not equal

```mongodb
db.COLLECTION_NAME.find({key: {$ne: value}})
```

23. Find with AND condition

```mongodb
db.COLLECTION_NAME.find({key1: val1, key2: val2})
```

24. Find with OR condition

```mongodb
db.COLLECTION_NAME.find({$or: [{key1: val1}, {key2: val2}]})
```

25. Projection query

```mongodb
db.COLLECTION_NAME.find({}, {field1: 1, field2: 1, _id: 0})
```

26. Limit result count

```mongodb
db.COLLECTION_NAME.find().limit(N)
```

27. Skip documents

```mongodb
db.COLLECTION_NAME.find().skip(N)
```

28. Sort result

```mongodb
db.COLLECTION_NAME.find().sort({field: 1})
```

29. Update one document (v3)

```mongodb
db.COLLECTION_NAME.update(query, updateObj)
```

30. Update many documents (v3)

```mongodb
db.COLLECTION_NAME.update(query, updateObj, {multi: true})
```

31. Update one document (v6)

```mongodb
db.COLLECTION_NAME.updateOne(query, updateObj)
```

32. Update many documents (v6)

```mongodb
db.COLLECTION_NAME.updateMany(query, updateObj)
```

33. Find one and update

```mongodb
db.COLLECTION_NAME.findOneAndUpdate(filter, update)
```

34. Find one and replace

```mongodb
db.COLLECTION_NAME.findOneAndReplace(filter, replacement)
```

35. Delete one document

```mongodb
db.COLLECTION_NAME.deleteOne(filter)
```

36. Delete many documents

```mongodb
db.COLLECTION_NAME.deleteMany(filter)
```

37. Create user

```mongodb
db.createUser({...})
```

38. Authenticate user

```mongodb
mongo -u username -p password database
```

39. Get user info

```mongodb
db.getUser("username")
```

40. Get role privileges

```mongodb
db.getRole("role", {showPrivileges:true})
```

41. Grant role to user

```mongodb
db.grantRolesToUser("user", [{role: "role", db: "db"}])
```

42. Revoke role from user

```mongodb
db.revokeRolesFromUser("user", [{role: "role", db: "db"}])
```

43. Change user password

```mongodb
db.changeUserPassword("username", "newPassword")
```

44. Create index (deprecated)

```mongodb
db.COLLECTION_NAME.ensureIndex({field: 1})
```

45. Create index with options

```mongodb
db.COLLECTION_NAME.createIndex({field: 1}, {options})
```

46. List all indexes

```mongodb
db.COLLECTION_NAME.getIndexes()
```

47. Explain query performance

```mongodb
db.COLLECTION_NAME.find(query).explain("executionStats")
```

48. Enable profiling

```mongodb
db.setProfilingLevel(2)
```

49. Read profiling results

```mongodb
db.system.profile.find()
```

50. Regex - contains sequence

```mongodb
db.phones.find({display:/070/})
```

51. Regex - ends with sequence

```mongodb
db.phones.find({display:/070$/})
```

52. Regex - starts with sequence

```mongodb
db.phones.find({display:/^070/})
```

53. Regex - starts with digit sets

```mongodb
db.phones.find({display:/\/\[246\]00/})
```

54. Regex - start and end match

```mongodb
db.phones.find({display:/\/20(.*)13$/})
```

55. mongodump basic

```mongodb
mongodump --db mydb --collection mycol --out path
```

56. mongorestore basic

```mongodb
mongorestore --db mydb --collection mycol path
```

57. mongodump with options

```mongodb
mongodump [options]
```

58. mongorestore with options

```mongodb
mongorestore [options]
```

59. JavaScript function: insertCustomer

```mongodb
function insertCustomer(...) {...}
```

60. Load JS file

```mongodb
load("insertCustomer.js")
```

61. PHP CSV import script

```mongodb
loadCountryIPv4.php
```

---

# 📘 Digital Library + User Management System

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

# 📘 Phonebook App

```javascript
function populatePhonebook(areaCode, quantity) {
  const inserted = new Set();
  let attempts = 0;

  while (inserted.size < quantity && attempts < quantity * 10) {
    attempts++;

    // Generate random 6-digit local number (000000–999999)
    const local = Math.floor(100000 + Math.random() * 900000);
    const display = `${areaCode}/${local}`;
    const id = parseInt(`${areaCode}${local}`); // Create numeric ID like 70200123

    if (inserted.has(id)) continue;

    try {
      db.phones.insertOne({
        _id: id,
        components: {
          areaCode: areaCode,
          localNumber: local,
        },
        display: display, // Example: "070/201013"
      });
      inserted.add(id);
    } catch (e) {
      if (e.code === 11000) continue; // Duplicate, try again
      else throw e;
    }
  }

  print(`✅ Inserted ${inserted.size} phone numbers for area code ${areaCode}`);
}
```

# 📞 MongoDB Phonebook Index & Regex Queries

```bash
mongosh
```

## 📦 Switch Database

```mongodb
use phonebookDB
```

## 📦 Create Index

Ensure fast searches and uniqueness on the `display` field:

```mongodb
db.phones.createIndex({ display: 1 }, { unique: true });
```

---

## 🔍 Regex Queries on `display`

### 1. Match any display value containing `"070"`

```mongodb
db.phones.find({ display: /070/ });
```

### 2. Match display values ending with `"070"`

```mongodb
db.phones.find({ display: /070$/ });
```

### 3. Match local numbers starting with `"201"` (after slash)

```mongodb
db.phones.find({ display: /\/201/ });
```

### 4. Match local numbers ending in `"200"`, `"400"`, or `"600"`

```mongodb
db.phones.find({ display: /\/[246]00/ });
```

### 5. Match numbers starting with `"20"` and ending with `"13"`

```mongodb
db.phones.find({ display: /\/20(.*)13$/ });
```

---

# 📞 Customer Support Ticketing System (MongoDB Shell Script)

This project demonstrates how to build a basic **Customer Support Ticketing System** using only the MongoDB shell. It showcases insertions, queries, updates, regex, user management, indexing, and backups.

---

## 🗂️ 1. Setup Database and Collections

```mongodb
use supportApp;

db.createCollection("tickets");
db.createCollection("users");
```

---

## 👥 2. Insert Sample Users

```mongodb
db.users.insertMany([
  { username: "agent1", role: "agent", email: "agent1@example.com" },
  { username: "cust1", role: "customer", email: "cust1@example.com" }
]);
```

---

## 🎟️ 3. Insert Sample Tickets

```mongodb
db.tickets.insertMany([
  {
    customerId: "cust1",
    issue: "App crashes on login",
    status: "open",
    createdAt: new Date(),
    priority: 3,
    tags: ["crash", "login"]
  },
  {
    customerId: "cust1",
    issue: "Cannot reset password",
    status: "open",
    createdAt: new Date(),
    priority: 2,
    tags: ["password", "support"]
  }
]);
```

---

## 🔍 4. Basic Queries

```mongodb
db.tickets.find().pretty();
db.tickets.find({ status: "open" });
db.tickets.find({ priority: { $gte: 2 } });
```

---

## 📊 5. Pagination, Projection, and Sorting

```mongodb
db.tickets.find({}, { issue: 1, _id: 0 }).sort({ priority: -1 }).skip(0).limit(5);
```

---

## 🧠 6. Compound and Conditional Queries

```mongodb
db.tickets.find({
  $or: [
    { status: "open" },
    { tags: "password" }
  ]
});
```

---

## 🔧 7. Update Tickets

```mongodb
db.tickets.updateOne(
  { issue: "App crashes on login" },
  { $set: { status: "in-progress", updatedAt: new Date() } }
);

db.tickets.updateOne(
  { issue: "App crashes on login" },
  { $push: { tags: "urgent" } }
);
```

---

## 🔁 8. Replace Ticket

```mongodb
db.tickets.replaceOne(
  { issue: "Cannot reset password" },
  {
    customerId: "cust1",
    issue: "Password reset fails",
    status: "open",
    createdAt: new Date(),
    priority: 3,
    tags: ["password"]
  }
);
```

---

## ❌ 9. Delete Tickets

```mongodb
db.tickets.deleteMany({ priority: { $lt: 2 } });
```

---

## 🔐 10. User Authentication Setup

```mongodb
use admin;
db.createUser({
  user: "supportAdmin",
  pwd: "securePass",
  roles: [{ role: "userAdminAnyDatabase", db: "admin" }]
});
db.auth("supportAdmin", "securePass");

use supportApp;
db.createUser({
  user: "agent1",
  pwd: "agentPass",
  roles: ["readWrite"]
});
db.createUser({
  user: "cust1",
  pwd: "custPass",
  roles: ["read"]
});
```

---

## 🔎 11. Create Indexes

```mongodb
db.tickets.createIndex({ status: 1 });
db.tickets.createIndex({ customerId: 1 });
db.tickets.createIndex({ issue: "text" });
db.tickets.getIndexes();
```

---

## 🔤 12. Regex Search Examples

```mongodb
db.tickets.find({ issue: /password/i });
db.tickets.find({ issue: /^App/ });
db.tickets.find({ issue: /login$/ });
```

---

## 🛠️ 13. JavaScript Function for Test Data

```mongodb
function insertTicket(customerId, issue, priority = 2) {
  db.tickets.insertOne({
    customerId: customerId,
    issue: issue,
    status: "open",
    createdAt: new Date(),
    priority: priority,
    tags: []
  });
}

insertTicket("cust1", "App freezes intermittently", 4);
```

---

## 💾 14. Backup and Restore (Shell Commands)

> These are external shell commands, not part of the script itself.

```bash
mongodump -u supportAdmin -p securePass --authenticationDatabase admin -d supportApp -o ./backup
mongorestore -u supportAdmin -p securePass --authenticationDatabase admin ./backup
```

---

## 📈 15. Enable Profiling

```mongodb
db.setProfilingLevel(2);
db.system.profile.find().pretty();
```

---
