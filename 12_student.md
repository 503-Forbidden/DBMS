```bash
use School
```

```bash
db.createCollection("Students")
```

```bash
db.Students.insertMany([
{
  student_id: 1,
  name: "Alice",
  age: 20,
  gender: "Female",
  marks: {
    math: 92,
    science: 88,
    english: 85
  }
},
{
  student_id: 2,
  name: "Bob",
  age: 19,
  gender: "Male",
  marks: {
    math: 65,
    science: 70,
    english: 78
  }
},
{
  student_id: 3,
  name: "Carol",
  age: 21,
  gender: "Female",
  marks: {
    math: 95,
    science: 91,
    english: 82
  }
},
{
  student_id: 4,
  name: "Dave",
  age: 22,
  gender: "Male",
  marks: {
    math: 78,
    science: 84,
    english: 89
  }
},
{
  student_id: 5,
  name: "Eve",
  age: 20,
  gender: "Female",
  marks: {
    math: 55,
    science: 60,
    english: 72
  }
}
])
```

```bash
db.Students.find({ gender: "Male" }).pretty()
```

```bash
db.Students.find({
  "marks.math": { $gt: 90 }
})
```

```bash
db.Students.find({
  age: { $gte: 20 }
})
```

```bash
db.Students.find({
  "marks.english": {
    $gte: 80,
    $lte: 90
  }
})
```

```bash
db.Students.countDocuments({
  gender: "Female"
})
```

```bash
db.Students.find(
  {},
  {
    name: 1,
    "marks.science": 1,
    _id: 0
  }
)
.sort({
  "marks.science": -1
})
.limit(1)
```

```bash
db.Students.updateOne(
  { name: "Bob" },
  { $set: { "marks.math": 75 } }
)
```

```bash
db.Students.deleteMany({
  "marks.math": { $lt: 70 }
})
```

```bash
db.Students.aggregate([
  {
    $group: {
      _id: null,
      avg_science: {
        $avg: "$marks.science"
      }
    }
  }
])
```

```bash
db.Students.countDocuments({
  $or: [
    { "marks.math": { $gt: 80 } },
    { "marks.science": { $gt: 80 } },
    { "marks.english": { $gt: 80 } }
  ]
})
```
