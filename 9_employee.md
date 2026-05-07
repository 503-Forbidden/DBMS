```
use Employee
```
```
db.createCollection("emp1")
```
```
db.emp1.insertMany([
{ eno: 1, ename: "Nilesh", address: "Nashik", sal: 12000 },
{ eno: 2, ename: "Priya", address: "Pune", sal: 8000 },
{ eno: 3, ename: "Rahul", address: "Mumbai", sal: 25000 },
{ eno: 4, ename: "Sneha", address: "Nagpur", sal: 3500 },
{ eno: 5, ename: "Manish", address: "Satara", sal: 18000 }
])
```

```
db.emp1.find().pretty()
```

```
db.emp1.insertOne({
_id: ObjectId("507f1f77bcf86cd799439011"),
eno: 6, ename: "Aditya", address: "Kolhapur", sal: 15000
})
```
```
db.emp1.find({ sal: { $gt: 5000 } }).pretty()
```
```
db.emp1.find({ sal: { $lt: 15000 } }).pretty()
```
```
db.emp1.find({ sal: { $gt: 10000, $lt: 20000 } }).pretty()
```
```
db.emp1.updateMany(
{},
[{ $set: { sal: { $multiply: ["$sal", 1.10] } } }]
)
```
```
db.emp1.deleteMany({ sal: { $lt: 5000 } })
```
```
db.emp1.renameCollection("employee1")
```
```
db.employee1.find({ ename: { $regex: /^n/i } }).pretty()
```
```
db.employee1.find({}, { ename: 1, _id: 0 }).sort({ ename: 1 })
```
