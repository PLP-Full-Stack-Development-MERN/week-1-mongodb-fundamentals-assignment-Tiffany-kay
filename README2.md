// MongoDB Fundamentals Assignment

// 1. Connect to MongoDB (Make sure MongoDB is running locally)

// 2. Create Database and Collection
db = connect("mongodb://localhost:27017/library");
db.createCollection("books");

// 3. Insert Sample Book Data
db.books.insertMany([
    { title: "The Great Gatsby", author: "Fitzgerald", year: 1925 },
    { title: "Mockingbird", author: "Harper Lee", year: 1960 },
    { title: "The Road", author: "McCarthy", year: 2006 },
    { title: "1984", author: "Orwell", year: 1949 },
    { title: "Catcher in the Rye", author: "Salinger", year: 1951 }
]);

// 4. Retrieve Data
// Retrieve all books
db.books.find().pretty();

// Query books by a specific author
db.books.find({ author: "Orwell" }).pretty();

// Find books published after 2000
db.books.find({ year: { $gt: 2000 } }).pretty();

// 5. Update Data
// Update the year of a specific book
db.books.updateOne({ title: "The Road" }, { $set: { year: 2007 } });

// Add a new field called rating to all books and set a default value
db.books.updateMany({}, { $set: { rating: 4.5 } });

// 6. Delete Data
// Delete a book by its title
db.books.deleteOne({ title: "The Great Gatsby" });

// Remove all books by a particular author
db.books.deleteMany({ author: "Salinger" });

// 7. Aggregation Pipeline
// Find the total number of books per author
db.books.aggregate([
    { $group: { _id: "$author", totalBooks: { $sum: 1 } } }
]);

// Calculate the average published year of all books
db.books.aggregate([
    { $group: { _id: null, avgYear: { $avg: "$year" } } }
]);

// Identify the top-rated book
db.books.find().sort({ rating: -1 }).limit(1);

// 8. Indexing
// Create an index on the author field
db.books.createIndex({ author: 1 });


