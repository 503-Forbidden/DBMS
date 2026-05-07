```
use Library
```
``` 
db.createCollection("Books")
db.createCollection("Products")
```
```
db.Books.insertMany([
{ book_id: 1, book_title: "DBMS", author_name: "Elmasri", publish_year: 2018 },
{ book_id: 2, book_title: "OS Concepts", author_name: "Silberschatz",publish_year: 2020
},
{ book_id: 3, book_title: "Algorithms", author_name: "Cormen", publish_year: 2009 },
{ book_id: 4, book_title: "Networking", author_name: "Elmasri", publish_year: 2016 }
])
 ```
```
db.Products.insertMany([
{ product_id: 1, name: "Laptop", price: 55000 },
{ product_id: 2, name: "Mouse", price: 800 },
{ product_id: 3, name: "Monitor", price: 12000 },
{ product_id: 4, name: "Keyboard",price: 1500 }
])
```
```
db.Products.createIndex({ price: 1 })
```
```
db.Books.createIndex({ author_name: 1, publish_year: -1 })
```
```
db.Books.getIndexes()
db.Products.getIndexes()
```
```
db.Products.dropIndex({ price: 1 })
``` 
```
db.Books.aggregate([
{ $group: { _id: "$author_name", total_books: { $sum: 1 } } },
{ $sort: { total_books: -1 } }
])
```
```
db.Products.aggregate([
{ $group: { _id: null, avg_price: { $avg: "$price" } } }
])
```
``` 
db.Products.aggregate([
{ $group: {
_id: null,
max_price: { $max: "$price" },
min_price: { $min: "$price" }
}}
])
```
```
db.Books.aggregate([
{ $match: { publish_year: { $gt: 2015 } } },
{ $count: "books_after_2015" }
])
```
```
db.Books.aggregate([
{ $project: { _id: 0, book_title: 1, author_name: 1 } }
])
```
```
db.Books.aggregate([
{ $sort: { publish_year: -1 } }
])
```
