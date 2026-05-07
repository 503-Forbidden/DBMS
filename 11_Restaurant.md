```bash
use Restaurants
```

```bash
db.createCollection("REST1")
```

```bash
db.REST1.insertMany([
{
  restaurant_id: 3001,
  name: "Spice Garden",
  address: {
    building: "12",
    street: "MG Road",
    city: "Pune",
    zipcode: "411001"
  },
  cuisine_type: "Indian",
  score: 85
},
{
  restaurant_id: 3002,
  name: "The Burger Barn",
  address: {
    building: "45",
    street: "FC Road",
    city: "Pune",
    zipcode: "411004"
  },
  cuisine_type: "American",
  score: 92
},
{
  restaurant_id: 3003,
  name: "Noodle House",
  address: {
    building: "7",
    street: "Camp Road",
    city: "Pune",
    zipcode: "411001"
  },
  cuisine_type: "Chinese",
  score: 78
},
{
  restaurant_id: 3004,
  name: "Curry Palace",
  address: {
    building: "23",
    street: "Baner Road",
    city: "Pune",
    zipcode: "411045"
  },
  cuisine_type: "Indian",
  score: 88
}
])
```

```bash
db.REST1.find().pretty()
```

```bash
db.REST1.find(
 {},
 {
   _id: 0,
   restaurant_id: 1,
   name: 1,
   "address.city": 1,
   "address.zipcode": 1
 }
)
```

```bash
db.REST1.find(
 { score: { $gt: 80, $lt: 100 } },
 { name: 1, score: 1, _id: 0 }
)
```

```bash
db.REST1.updateOne(
 { restaurant_id: 3001 },
 { $set: { score: 90 } }
)
```

```bash
db.REST1.updateMany(
 { cuisine_type: "Indian" },
 { $set: { cuisine_type: "Indian_Zatka" } }
)
```

```bash
db.REST1.deleteOne(
 { restaurant_id: 3003 }
)
```

```bash
db.REST1.deleteMany(
 { score: { $lt: 85 } }
)
```
