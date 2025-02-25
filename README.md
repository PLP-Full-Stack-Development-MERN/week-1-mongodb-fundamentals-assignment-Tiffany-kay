# MongoDB Fundamentals Assignment

## Setup MongoDB

1. **Install MongoDB** locally or create a **free cluster on MongoDB Atlas**.
2. **Start the MongoDB server** locally or connect to the MongoDB Atlas cluster.
3. **Verify the installation and connection** using:
   ```sh
   mongo --version
   ```

## Database and Collection Creation

1. Open the MongoDB shell and run:
   ```sh
   use library
   db.createCollection("books")
   ```

## Insert Data

Add at least five book records:
```sh
db.books.insertMany([
    { title: "The Great Gatsby", author: "Fitzgerald", year: 1925 },
    { title: "Mockingbird", author: "Harper Lee", year: 1960 },
    { title: "The Road", author: "McCarthy", year: 2006 },
    { title: "1984", author: "Orwell", year: 1949 },
    { title: "Catcher in the Rye", author: "Salinger", year: 1951 }
])
```

## Retrieve Data

Retrieve all books:
```sh
db.books.find().pretty()
```

Query books by a specific author:
```sh
db.books.find({ author: "Orwell" }).pretty()
```

Find books published after 2000:
```sh
db.books.find({ year: { $gt: 2000 } }).pretty()
```

## Update Data

Update the year of a specific book:
```sh
db.books.updateOne({ title: "The Road" }, { $set: { year: 2007 } })
```

Add a new field called `rating` to all books with a default value:
```sh
db.books.updateMany({}, { $set: { rating: 4.5 } })
```

## Delete Data

Delete a book by its title:
```sh
db.books.deleteOne({ title: "The Great Gatsby" })
```

Remove all books by a particular author:
```sh
db.books.deleteMany({ author: "Salinger" })
```

## Aggregation Pipeline

Find the total number of books per author:
```sh
db.books.aggregate([
    { $group: { _id: "$author", totalBooks: { $sum: 1 } } }
])
```

Calculate the average published year of all books:
```sh
db.books.aggregate([
    { $group: { _id: null, avgYear: { $avg: "$year" } } }
])
```

Identify the top-rated book:
```sh
db.books.find().sort({ rating: -1 }).limit(1)
```

## Indexing

Create an index on the `author` field to improve search performance:
```sh
db.books.createIndex({ author: 1 })
```

### **Why Use Indexing?**
- Indexing speeds up queries by allowing MongoDB to quickly locate documents.
- It is particularly useful when searching large datasets.

## Testing

1. Use the **MongoDB shell or Compass** to verify the inserted and updated records.
2. Ensure all queries return the expected results.

